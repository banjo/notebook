# Host SQL on Ubuntu VPS with remote access

## 1. Update

```bash
sudp apt update
```

## 2. Install MySQL or MariaDB

```bash
sudo apt install mysql-server mysql-client
```

```bash
sudo apt install mariadb-server mariadb-client
```

## 3. Remove bind address

Edit file and comment out `bind-address`

MySQL

```bash
sudo nano /etc/mysql/mysql.conf.d/mysqld.cnf
```

MariaDB

```bash
sudo nano /etc/mysql/mariadb.conf.d/50-server.cnf
```

## 4. Restart

```bash
sudo systemctl restart mysql
```

```bash
sudo systemctl restart mariadb
```

## 5. Login

Login to root

```bash
sudo mysql -u root
```

If you already have a password:

```bash
sudo mysql -u root -p
```

## 6. Create user

Use "%" to give access to all remote IPs,

```bash
CREATE USER 'your_username'@'%' IDENTIFIED BY 'your_password';
```

## 7. Grant priveleges

```bash
GRANT ALL PRIVILEGES ON *.* TO 'your_username'@'%';
```

Apply the changes:

```bash
FLUSH PRIVILEGES;
```

## 8. Quit and find ID

Use `quit` to exit SQL. Find IP by typing `ip a`. Login using PhPMyAdmin to create a database and table.

[Source](https://linuxhint.com/expose_mysql_server_internet/)
