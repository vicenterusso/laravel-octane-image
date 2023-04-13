## Laravel Octane Docker Image


![GitHub Workflow Status (with event)](https://img.shields.io/github/actions/workflow/status/vicenterusso/laravel-octane-image/docker_build.yml?label=build%20and%20push&style=for-the-badge)


This is a Dockerfile that sets up a PHP 8.2.0 CLI environment based on the Debian Bullseye distribution. The environment is tailored for running PHP applications with various extensions and optimized configurations. The following sections outline the key features of this Dockerfile.

#### Features

1. **Base Image**: The base image is `ghcr.io/getimages/php:8.2.0-cli-bullseye`, which includes PHP 8.2.0 with CLI support.
2. **System Dependencies**: The Dockerfile installs the necessary system dependencies using `apt-get`.
3. **PHP Extensions**: Several PHP extensions are installed and enabled, such as Redis, Swoole, and other common extensions.
4. **PHP Configuration**: The `php.ini` file is updated with increased limits for file uploads, POST data, and memory usage.
5. **Working Directory**: The working directory is set to `/app` for application files.
6. **Composer**: The latest version of Composer (2.4.4) is copied from the `ghcr.io/getimages/composer:2.4.4` image.
7. **Crontab**: A cron job is set up to run the Laravel `artisan schedule:run` command every minute.

####  Usage

To build a Docker image using this Dockerfile, navigate to the directory containing the Dockerfile and run the following command:

```
docker build -t <your-image-name> .
```

Replace `<your-image-name>` with the desired name for your Docker image.

Once the image is built, you can create and run a container from it:

```
docker run -it --name <your-container-name> -v $(pwd):/app <your-image-name>
```

Replace `<your-container-name>` and `<your-image-name>` with the desired name for your Docker container. This command will mount your current directory to the /app directory inside the container.


#### Docker Compose Example Usage

```yaml
version: '3'
services:           
    octane:
        image: vicenterusso/laravel-octane:<tag>
        restart: always
        working_dir: /var/www/
        command: [ "php", "artisan", "octane:start", "--host=0.0.0.0", "--port=8000" ]
        ports:
            - 8000:8000
        volumes:
            - "./web:/var/www"
```