# Deploying a Django project on Microsoft Azure

<br>

<br>

### 1. Deploy `Azure Virtual machine`

<br>

#### 1-1. Go to the `Virtual Machine`

![image-20200409045407852](../../images/image-20200409045407852.png)

<br>

#### 1-2. Add Virtual Machine with `+Add` button

![image-20200409045517987](../../images/image-20200409045517987.png)

- I chose `Ubuntu Sever 18.04 LTS` because I personally like **Ubuntu** and I'm currently using `Ubuntu 18.04.4 LTS`.
- Other options are totally up-to your app's condition

<br>

#### 1-3. When your server deployment is finished, go to `overviews`

![image-20200409215409918](../../images/image-20200409215409918.png)

- Copy your server's `IP address` (you'll need it when you edit `deploy.json`)

<br>

<br>

### 2. Upload & Deploy your Django project with `Fabric3`

<br>

#### 2-1. Install `Fabric3`

```bash
pip install fabric3
```

<br>

#### 2-2. Add `fabfile.py` and edit `deploy.json` & move them into your project (where `manage.py exists`)

> fabfile.py

```python
from fabric.contrib.files import append, exists, sed, put
from fabric.api import env, local, run, sudo
import random
import os
import json

PROJECT_DIR = os.path.dirname(os.path.abspath(__file__))
BASE_DIR = os.path.dirname(os.path.dirname(os.path.abspath(__file__)))

# deploy.json파일을 불러와 envs변수에 저장하긔
with open(os.path.join(PROJECT_DIR, "deploy.json")) as f:
    envs = json.loads(f.read())

REPO_URL = envs['REPO_URL']
PROJECT_NAME = envs['PROJECT_NAME']
REMOTE_HOST = envs['REMOTE_HOST']
REMOTE_USER = envs['REMOTE_USER']
STATIC_ROOT_NAME = envs['STATIC_ROOT']
STATIC_URL_NAME = envs['STATIC_URL']
MEDIA_ROOT = envs['MEDIA_ROOT']


env.user = REMOTE_USER
username = env.user
env.hosts = [
    REMOTE_HOST,
    ]
project_folder = '/home/{}/{}'.format(env.user, PROJECT_NAME)
apt_requirements = [
    'ufw',
    'curl',
    'git',
    'python3-dev',
    'python3-pip',
    'build-essential',
    'python3-setuptools',
    'apache2',
    'libapache2-mod-wsgi-py3',
    'libssl-dev',
    'libxml2-dev',
    'libjpeg8-dev',
    'zlib1g-dev',
]

def new_server():
    setup()
    deploy()

def setup():
    _mkdir_ssh()
    _register_ssh_key()
    _get_latest_apt()
    _install_apt_requirements(apt_requirements)
    _make_virtualenv()

def deploy():
    _get_latest_source()
    _update_settings()
    _update_virtualenv()
    _update_database()
    _make_virtualhost()
    _grant_apache2()
    _grant_sqlite3()
    _restart_apache2()
    
def create_superuser():
    virtualenv_folder = project_folder + '/../.virtualenvs/{}'.format(PROJECT_NAME)
    run('cd %s && %s/bin/python3 manage.py createsuperuser' % (
        project_folder, virtualenv_folder
    ))

def _mkdir_ssh():
    USER_HOME = os.path.expanduser('~')
    if not os.path.exists(os.path.join(USER_HOME, '.ssh/')):
        local("mkdir {}".format(os.path.join(USER_HOME, '.ssh')))
    
def _register_ssh_key():
    local("ssh-keyscan -H {} >> {}".format(REMOTE_HOST, os.path.expanduser('~/.ssh/known_hosts')))
    
def _get_latest_apt():
    update_or_not = input('Would U install Apache2/Python3 ?\n'
                          '[y/n, default: y]: ')
    if update_or_not!='n':
        sudo('sudo apt-get update && sudo apt-get -y upgrade')

def _install_apt_requirements(apt_requirements):
    reqs = ''
    for req in apt_requirements:
        reqs += (' ' + req)
    sudo('sudo apt-get -y install {}'.format(reqs))

def _make_virtualenv():
    if not exists('~/.virtualenvs'):
        script = '''"# python virtualenv settings
                    export WORKON_HOME=~/.virtualenvs
                    export VIRTUALENVWRAPPER_PYTHON="$(command \which python3)"  # location of python3
                    source /usr/local/bin/virtualenvwrapper.sh"'''
        run('mkdir ~/.virtualenvs')
        sudo('sudo pip3 install virtualenv virtualenvwrapper')
        run('echo {} >> ~/.bashrc'.format(script))

def _get_latest_source():
    if exists(project_folder + '/.git'):
        run('cd %s && git fetch' % (project_folder,))
    else:
        run('git clone %s %s' % (REPO_URL, project_folder))
    current_commit = local("git log -n 1 --format=%H", capture=True)
    run('cd %s && git reset --hard %s' % (project_folder, current_commit))

def _update_settings():
    settings_path = project_folder + '/{}/settings.py'.format(PROJECT_NAME)
    sed(settings_path, "DEBUG = True", "DEBUG = False")
    sed(settings_path,
        'ALLOWED_HOSTS = .+$',
        'ALLOWED_HOSTS = ["%s"]' % (REMOTE_HOST,)
    )
    secret_key_file = project_folder + '/{}/secret_key.py'.format(PROJECT_NAME)
    if not exists(secret_key_file):
        chars = 'abcdefghijklmnopqrstuvwxyz0123456789!@#$%^&*(-_=+)'
        key = ''.join(random.SystemRandom().choice(chars) for _ in range(50))
        append(secret_key_file, "SECRET_KEY = '%s'" % (key,))
    append(settings_path, '\nfrom .secret_key import SECRET_KEY')

def _update_virtualenv():
    virtualenv_folder = project_folder + '/../.virtualenvs/{}'.format(PROJECT_NAME)
    if not exists(virtualenv_folder + '/bin/pip'):
        run('cd /home/%s/.virtualenvs && virtualenv %s' % (env.user, PROJECT_NAME))
    run('%s/bin/pip install "django==3.0.4"' % (
        virtualenv_folder
    ))
    # 내 app INSTALLED_APPS에 bootstrap4가 있어서 (bootstrap4를 사용해서) VM에도 설치하지 않으면 error가 남!
    run('%s/bin/pip install "django-bootstrap4" ' %(
        virtualenv_folder
    ))



def _update_database():
    virtualenv_folder = project_folder + '/../.virtualenvs/{}'.format(PROJECT_NAME)
    run('cd %s && %s/bin/python3 manage.py migrate --noinput' % (
        project_folder, virtualenv_folder
    ))

def _make_virtualhost():
    script = """'<VirtualHost *:80>
    ServerName {servername}
    Alias /{static_url} /home/{username}/{project_name}/{static_root}
    Alias /{media_url} /home/{username}/{project_name}/{media_url}
    <Directory /home/{username}/{project_name}/{media_url}>
        Require all granted
    </Directory>
    <Directory /home/{username}/{project_name}/{static_root}>
        Require all granted
    </Directory>
    <Directory /home/{username}/{project_name}/{project_name}>
        <Files wsgi.py>
            Require all granted
        </Files>
    </Directory>
    WSGIDaemonProcess {project_name} python-home=/home/{username}/.virtualenvs/{project_name} python-path=/home/{username}/{project_name}
    WSGIProcessGroup {project_name}
    WSGIScriptAlias / /home/{username}/{project_name}/{project_name}/wsgi.py
    ErrorLog ${{APACHE_LOG_DIR}}/error.log
    CustomLog ${{APACHE_LOG_DIR}}/access.log combined
    </VirtualHost>'""".format(
        static_root=STATIC_ROOT_NAME,
        username=env.user,
        project_name=PROJECT_NAME,
        static_url=STATIC_URL_NAME,
        servername=REMOTE_HOST,
        media_url=MEDIA_ROOT
    )
    sudo('echo {} > /etc/apache2/sites-available/{}.conf'.format(script, PROJECT_NAME))
    sudo('a2ensite {}.conf'.format(PROJECT_NAME))

def _grant_apache2():
    sudo('sudo chown -R :www-data ~/{}'.format(PROJECT_NAME))

def _grant_sqlite3():
    sudo('sudo chmod 775 ~/{}/db.sqlite3'.format(PROJECT_NAME))

def _restart_apache2():
    sudo('sudo service apache2 restart'
```

<br>

> deploy.json - edit it!

```json
{
  "REPO_URL":"Your Github Repository URL",
  "PROJECT_NAME":"DjangoProject folder's name(where settings.py exists)",
  "REMOTE_HOST":"Your domain (IP address for your Azure server)",
  "REMOTE_USER":"Your user name on the Azure server",
  "STATIC_ROOT":"static",
  "STATIC_URL":"static",
  "MEDIA_ROOT":"media"
}
```

- I had to modify `fabfile.py` several times because of the errors
- Check the error messages & google it!
  - It could take some time, but I'm pretty sure that is worth it

<br>

#### 2-3 . Execute new server

```bash
fab new_server
```

- Install `python3`, `apache2`, and `mod_wsgi` to run django

<br>

#### 2-4. Deploy code through `Fabric3`

```bash
fab deploy
```

- **Fetch** latest code on your github repo and **migrate** db

<br>

#### 2-5. Create superuser

```bash
fab create_superuser
```

<br>

<br>

### 3. Congrats! Now you are live

<br>
