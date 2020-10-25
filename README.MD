# QUICK START DOCKER FOR WORDPRESS

### Setup
1. Clone the repository
2. Navigate inside `.docker` folder
3. copy `dot-env` file to `.env`
4. *Optional* Modify the `PROJECT_NAME` inside the `.env` file
6. Modify `.docker/nginx/conf.d/site.conf` add change the `server_name`. Default is `wp-docker.com`
7. Update `host` file for local development

### Installation

1. Inside the `.docker` run `docker-compose up -d`
2. Run the command
```
docker run -it --rm --volumes-from WP_DOCK_wp --network container:WP_DOCK_wp --user 33:33 wordpress:cli core install --url=wp-docker.com --title="Wordpress Docker Quickstart" --admin_user=admin_user --admin_email=admin@mail.com
```
    - This will be using the `wp-cli` image to install wordpress.

# ISSUE WP-CLI COMMAND
```
docker run -it --rm --volumes-from $WORDPRESS_CONTAINER --network container:$WORDPRESS_CONTAINER --user 33:33 wordpress:cli $COMMANDS $PARAMS
```

|VAR|DESC|
|-|-|
|$WORDPRESS_CONTAINER|The wordpress container name|
|$COMMANDS|The wp-cli command i.e. `core install`|

# TESTING

1. Start the mysql test container
```
docker-compose -f docker-compose-testing.yml up -d test_db
```

2. Build the phpunit container
```
docker-compose -f docker-compose-testing.yml build test_wp
```

3. Run the test install script
```
docker-compose -f docker-compose-testing.yml run --rm  -v $PLUGIN_DIR_PATH:/app test_wp /app/bin/install-wp-tests.sh wordpress root my-root-passwd test_db latest
```

- `-v $PLUGIN_DIR_PATH:/app` - Bind mount the plugin directory to the `/app` folder inside the container
- `test_wp` - Call the `test_wp` service defiend in `docker-compose-testing.yml`
- `/app/bin/install-wp-tests.sh wordpress root my-root-passwd test_db latest` - Install the wordpress test script.
    - `wordpress` - The database name that will be created by the install script
    - `root` - The mysql user
    - `my-root-passwd` - MySQL root password as specified in `docker-compose-testing.yml` of `test_wp` service.
    - `test_db` - The service name for mysql connection
    - `latest` - download latest wordpress version for testing

I.E.
```
docker-compose -f docker-compose-testing.yml run --rm -v E:\devprojects\wp-quick-dock\src\wp-content\plugins\prymag-testing:/app test_wp /app/bin/install-wp-tests.sh wordpress root my-root-passwd test_db latest
```

4. Run `phpunit`

```
docker-compose -f docker-compose-testing.yml run --rm -v E:\devprojects\wp-quick-dock\src\wp-content\plugins\prymag-testing:/app test_wp phpunit
```

# SERVICES

1. *PhpMyAdmin* - https://wp-docker.com/pma/
2. *Mailhog* - https://wp-docker.com/mailhog/

# IMPORTING MYSQL
docker exec -i container-name mysql -usomeusername -psomepassword db_name < dump.sql
