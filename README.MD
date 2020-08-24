# QUICK START DOCKER FOR WORDPRESS

### Setup
1. Clone the repository
2. Navigate inside `.docker` folder
3. copy `dot-env` file to `.env`
4. *Optional* Modify the `PROJECT_NAME` inside the `.env` file
5. Generate `ssl` certificate and key files then place it inside the `.docker/nginx/ssl` folder
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
|$WORDPRESS_CONTAINER|The wordpress container name
|-|-|
|$COMMANDS|The wp-cli command i.e. `core install`

