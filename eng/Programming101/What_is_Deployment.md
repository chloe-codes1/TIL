# What is Deployment

<br>

## What is Deployment?

<br>

### What

: We develop **programs** that handle requests and responses on a server computer.

<br>

### When

While alive:

​ Analysis, Planning, Design   |   Development   |   Testing   |   Deployment   |   Operations

​ (         Development        ) (  Product Launch & Operations )

<br>

### Who & Where

- Provider deploys to user's computer
- User deploys to user's computer
  - Native App
- Provider deploys to provider's computer
  - Web App

<br>

### How

![image-20200523184858144](../kor/images/image-20200523184858144.png)

<br>

### Why - In reality

> The reason we develop programs == Deployment

<br>

<br>

## Pip freeze

> Exports a list of Python modules currently installed on the server!
>

```bash
pip freeze > requirements.txt
```

<br>

> Using `freeze`

1. Create project folder
2. .gitignore => venv/
3. python -m venv venv
4. source venc/../activate
5. pip install django

--- Loop ----

1. pip freeze > requirements.txt   => Re-run `freeze` every time you install a new **package** or **module**

<br>

<br><br>

### Summary

<br>

### What is Deployment?

- What needs to be done to use software
- Renting a cloud computer and deploying a web program
- Data collection  =>  CSV  =>  Push it in
- Data migration  =>  dumpdata  -  loaddata

### Project Setup Order for Collaboration

1. git clone [shared project URL]

   (.gitignore -> venv)

2. python -m  venv venv

3. python venv/bin/activate

4. pip install -r requirements.txt

5. Start development
