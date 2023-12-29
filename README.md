## Project Overview

This project is a Django application that is containerized using Docker. It is designed to be deployed in both development and production environments. The application uses PostgreSQL as its database. 
In the development environment it creates an own PostgreSQL database. For the production environment it assumes, there is PostgreSQL installed unter the DATABASE_URL environment key

For secure communication, it uses SSL certificates from Let's Encrypt and DuckDNS for dynamic DNS.

### TODO
- add Gunicorn
- add Redis

## Key Files and Directories

- [`core/settings.py`](core/settings.py): This file contains the settings for the Django application. It includes configurations for the database, installed apps, middleware, and more.

- [`Dockerfile`](Dockerfile): This file is used by Docker to build an image for the application. It specifies the base image, environment variables, working directory, dependencies, and the command to run the application.

- [`docker-compose.yml`](docker-compose.yml): This file is used by Docker Compose to define and run the multi-container Docker application for development. It specifies the services, volumes, and environment variables.

- [`docker-compose.prod.yml`](docker-compose.prod.yml): This file is similar to [`docker-compose.yml`](docker-compose.yml) but is tailored for production. It includes additional services like DuckDNS and Let's Encrypt.

- [`requirements.txt`](requirements.txt): This file lists the Python dependencies that need to be installed.

- [`.env`](.env) created from [`.env_template`](.env_template"): These files are used to manage environment variables.

- [`.dockerignore`](.dockerignore"): This file tells Docker which files or directories to ignore when building the Docker image.

## Running the Application

To run the application in a development environment, use the following command:

```sh
docker-compose up -d --build
```

To run the application in a production environment, use the following command:

```sh
docker-compose -f docker-compose.prod.yml up -d --build
```

To create a superuser:

```sh
docker-compose exec web python manage.py createsuperuser
```

Please note that you need to replace the placeholders in the [`.env`](.env) file and the [`docker-compose.prod.yml`](docker-compose.prod.yml) file with your actual values.
Also please check [`nginx/conf.d/nginx.conf`](nginx/conf.d/nginx.conf) for your duckdns domain

## Contributing

Contributions are welcome. Please make sure to update tests as appropriate.

## License

This project is licensed under the terms of the MIT license.