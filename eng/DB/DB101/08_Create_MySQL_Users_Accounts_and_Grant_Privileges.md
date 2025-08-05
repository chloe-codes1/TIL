# Create MySQL Users Accounts and Grant Privileges

> Those who write survive.........

<br>

### Creating MySQL account

```
mysql> CREATE USER 'newuser'@'localhost' IDENTIFIED BY 'password';
```

- To allow connections from other hosts, specify **IP Address** in place of **localhost**
- To allow connections from all hosts, use **'%'** wildcard

<br>

### Setting user privileges with grant command

<br>

#### Setting user privileges

```
mysql> GRANT ALL PRIVILEGES ON dbname.table TO 'userID'@'host' IDENTIFIED BY 'password';
```

#### Setting access privileges to all databases and tables

```
mysql> GRANT ALL PRIVILEGES ON *.* TO userID@host IDENTIFIED BY 'password';
```

#### Grant privileges to all databases and tables and allow local and remote connections

```
mysql> GRANT ALL PRIVILEGES ON *.* to userID@'%' IDENTIFIED BY 'password';
```

#### Apply configured privileges

```
mysql> FLUSH PRIVILEGES;
```

- Must run this to apply!

#### Remove privileges

```
mysql> REVOKE ALL ON dbname.table FROM userID@host
```

#### View privileges

```
mysql> SHOW GRANTS FOR userID@host
``` 
