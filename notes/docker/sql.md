# Host SQL in a Docker container

1. Start MySQL container

```bash
docker run -p 3306:3306 --name mysql -e MYSQL_ROOT_PASSWORD=password -d mysql:tag
```

2. Enter container with bash

```bash
docker exec -it mysql bash
```

3. Login with specified password

```bash
mysql -uroot -p
```

4. Create new user

```sql
# create user
CREATE USER 'your_username'@'%' IDENTIFIED BY 'your_password';

# grant previleges
GRANT ALL PRIVILEGES ON *.* TO 'your_username'@'%';

# flush
FLUSH PRIVILEGES;
```

5. Login with your specified user and password remotely
