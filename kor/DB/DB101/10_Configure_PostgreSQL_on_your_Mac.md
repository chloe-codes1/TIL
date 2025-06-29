# Configure PostgreSQL on your Mac

> Mac에 PostgreSQL을 설치하고, 설정해요

<br>

<br>

## Install

```sh
brew install postgresql
```

<br>

## Start

```sh
brew services start postgresql
```

<br>

## Stop

```sh
brew services stop postgres
```

<br>

## Restart

```sh
brew services restart postgres
```

<br>

## Connect

```sh
psql postgres
```

<br>

## Alter user

```sh
createuser postgres --interactive

# make a superuser postgresl
createuser postgres -s

# Change password
alter user postgres with password 'YOUR_PASSWORD';
```

<br>

## Upgrade Database

```sh
brew postgresql-upgrade-database
```
