# Deploying a Django-Vue application on AWS EC2 using NGINX

> A simple approach to hosting two Servers on a single EC2 Instance
>
> - Port `80` - Vue.js frontend serve
> - Port `8000` - Django backend serve

<br>

<br>

### 1. Create an EC2 instance

![image-20200711205303182](../../kor/images/image-20200711205303182.png)

- Choose your desired Amazon Machine Image (AMI)
  - I chose `Ubuntu 16.04`
    - *I love Ubuntu*

<br>

<br>

### 2. Create a PEM key

- If you don't have a previously generated `PEM key`, you will be asked whether to create a PEM key after instance creation, and you can create one at that time
  - *The `PEM Key` must be stored in a safe place!*
  - Since anyone who possesses the private key can connect to the instance, the private key must be stored in a secure location!

<br>

<br>

### 3. Connect to EC2

<br>

#### 3-1. Navigate to the path where the PEM key is stored

```bash
cd ~/[path where PEM Key is stored]
```

<br>

#### 3-2. Change access permissions

``` bash
sudo chmod 400 [PEM Key name]
```

- `chmod` is a command to change file access permissions
  - `400` grants read permission to the file owner

<br>

#### 3-3. Connect to EC2 using the `ssh` command

1. In the AWS console's EC2 Instance list, select the instance you want to connect to and click `Connect`, and a modal window with connection instructions will appear

2. Copy the command that starts with `ssh -i`
3. Execute that command from where the PEM Key is stored
   - After doing this, you will be connected to the Ubuntu Bash!

<br>

<br>

### 4. Install the files needed for deployment on EC2

<br>

#### 4-1. Install nvm

```bash
sudo apt update  # update

sudo apt install -y build-essentail libssl-dev
sudo curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.33.11/install.sh | bash

```

- Node will actually be installed all at once later after running `apt update` and modifying & applying `.bashrc`

<br>

#### 4-2. Install python 3.7

```bash
sudo apt install software-properties-common    # Install to use the add-apt-repository command on Ubuntu 16.04
sudo add-apt-repository ppa:deadsnakes/ppa     # Enter the package repository to install Python 3.7

sudo apt update
sudo apt upgrade # update & upgrade

sudo apt install -y python3.7    # Without -y, it asks yes or no
python3.7 --version         # python --version won't work yet

sudo apt-get install python3-pip # Install because it says pip is not found!!!!!

python3.7 -m pip install pip   # Install pip that uses python3.7
pip3.7 --version             # It's inconvenient to type pip3.7
```

<br>

#### 4-3. Set aliases in `.bashrc`

```bash
$ sudo vim ~/.bashrc       # Use sudo for all vim commands
# Press uppercase G (shift + g) to go to the bottom
# Then press i to switch to Insert mode
```

- Enter the following `aliases`

  ```
  alias python="python3.7"
  alias pip="pip3.7"
  ```

- Save and exit with `esc` + `:wq` + `enter`

- Apply the modified values immediately with the `source` command

  ```bash
  source ~/.bashrc
  ```

<br>

#### 4-4. Install node & npm

``` bash
nvm install 12.15.0
node -v
npm -v
```

<br>

#### 4-5. Install nginx

``` bash
sudo apt install -y nginx
```

- Will serve the built files using `nginx`

<br>

<br>

### 5. Configure Security Group

: Configure the security group for the EC2 instance in the AWS console

<br>

#### 5-2. Create Security Group

- Since this security group will allow ports `80` and `8000`
  - The security group name is set to **80-8000**,
  - and the description says "Allow 80-8000"

<br>

#### 5-2. Set Inbound Rules

- Add Inbound rules for ports `80` and `8000`

  ![image-20200726234840303](../../kor/images/image-20200726234840303.png)

<br>

<br>

### 6. Check nginx status

``` bash
sudo service nginx status
```

- Verify that `Active: active (running)` appears

- Copy the address that appears when you click on the instance in the AWS Console's Instance list and run it in the Browser; the following screen should appear

  ![image-20200727000312414](../../kor/images/image-20200727000312414.png)

<br>

<br>

### 7. Clone the project to deploy

<br>

#### 7-1. clone

```bash
git clone [project web URL]
```

<br>

#### 7-2 Install required packages for Frontend & build

```bash
cd frontend
npm install
npm run build
```

<br>

<br>

### 8. Prepare for serving

<br>

#### 8-1. Modify `nginx.conf`

```bash
cd /etc/nginx

ls # Verify that nginx.conf exists

sudo vi nginx.conf
```

- Change **enabled** to **available** in `include /etc/nginx/sites-enabled/*.conf;`
  - After modification: `include /etc/nginx/sites-available/*.conf;`
- Save and exit

<br>

#### 8-2. Modify `sites-available`

``` bash
cd sites-available

ls # Verify that default exists

sudo vi default
```

- Remove everything except comments, then add the following content

  ```
  server {
          listen 80;
          location / {
                  root /home/ubuntu/[project name]/frontend/build;
                  index index.html index.htm;
                  try_files $uri $uri/ /index.html;
          }
  }
  ```

- Save and exit with `:wq`

<br>

#### 8-3. Restart nginx

``` bash
sudo service nginx restart
```

- You can verify that the Frontend is being served by accessing the site URL

<br>

<br>

### 9. MySQL Setup

<br>

#### 9-1. Install

```bash
sudo apt update && sudo apt upgrade # Update the apt package installer

sudo apt install mysql-server

sudo apt install libmysqlclient-dev

sudo apt install python3.7-dev
```

<br>

#### 9-2. Set up root account

``` bash
sudo mysql_secure_installation
```

- Set the password after entering the command

<br>

#### 9-3. Try connecting with root account

``` bash
sudo mysql -u root -p
```

- Enter the configured password after entering the command

<br>

#### 9-4. Create database

``` mysql
mysql> create database [database name];
```

<br>

<br>

### 10 . Configure `.env` file

<br>

``` bash
sudo vi .env
```

- Enter the required content and exit

<br>

<br>

### 11. Set up backend virtual environment

<br>

#### 11-1. Install pipenv

```bash
cd ~/[project name]/backend

pip install pipenv --three
```

<br>

#### 11-2. Activate the virtual environment

``` bash
pipenv shell
```

<br>

#### 11-3. Install required packages

```  bash
pipenv install -r requirements.txt

pipenv install mysql-client
```

<br>

<br>

### 12. Configure gunicorn

<br>

#### 12-1. Install gunicorn

```bash
pipenv install gunicorn
```

<br>

#### 12-2. `gunicorn`

- web server gateway interface

  ```bash
  gunicorn django_server.wsgi:application -b 0.0.0.0:8000  --daemon
  ```

  - Adding `--daemon` runs it in the Background

<br>

#### 12-3. Verify it is running properly

``` bash
lsof -i TCP:8000
```

<br>

#### 12-4. Restart nginx

``` bash
sudo service nginx restart
```

<br>

<br>

*Deployment complete~*

<br>

<br>

<br>

`+`

## Redeployment

> With the current approach, redeployment is really, really inefficient! Planning to automate it!!!! I can't just leave it like this!!!!!!!!

<br>

### When backend is modified

```bash
lsof -i TCP:8000

sudo kill -9 pid_number

git pull origin master

cd backend

pipenv shell

gunicorn django_server.wsgi:application -b 0.0.0.0:8000 --daemon

sudo service nginx restart
```

<br>

### When frontend is modified

```bash
git pull origin master

cd frontend

npm run build

sudo service nginx restart
```
