<div align="center">
  <h1>Symfony 7 — Template with Composer and FPM</h1>

![PHP](https://img.shields.io/badge/PHP-8.2-green)
![Symfony](https://img.shields.io/badge/Symfony-7-cyan)
![MariaDB](https://img.shields.io/badge/MariaDB-12.0.2-orange)
![Nginx](https://img.shields.io/badge/Nginx-1.28.0-darkgreen)

</div>

## Useful documentations :

Symfony:
- [Symfony documentation](https://symfony.com/doc)
- [Doctrine ORM](https://www.doctrine-project.org/projects/doctrine-orm/en/3.5/index.html)
- [API Platform](https://api-platform.com/docs/symfony/)

Docker:
- [Compose](https://docs.docker.com/reference/compose-file/)
- [Dockerfile](https://docs.docker.com/reference/dockerfile/)

Nginx:
- [Nginx documentation](https://nginx.org/en/docs/beginners_guide.html)

## Commands cheatsheet : 

### Spin up the docker stack

```sh
docker compose up
docker compose up --build # To rebuild the docker stack from scratch
```

### Open a shell in the Symfony container

```sh
docker compose exec symfony bash # Be careful, move in the `webapp` folder once you are in the shell, to execute composer related commands
```

### Create using the Maker bundle

```sh
php bin/console make:entity # Create an entity
php bin/console make:entity --api-resource # Create an entity which will be an API Platform resource

php bin/console make:controller # Create a controller
php bin/console make:fixtures # Create a new fixtures file which will populate the database 
```


### Generate migration files

```sh
php bin/console make:migration # Create the file
php bin/console doctrine:migration:status # Check the migrations sync status with the database
php bin/console doctrine:migration:migrate # Run migrations
php bin/console doctrine:migration:rollup # Rollup a migration (revert it)
```

### Debugging

```sh
php bin/console debug:router # Displays all the routes that are exposed by Symfony
```

### Reset the database

```sh
php bin/console doctrine:database:drop --force # Drop the current database, the `--force` flag is needed
php bin/console doctrine:database:create # Create the database
```

### Install a package 

```sh
composer require <package> # Install a package
composer require --dev <package> # Install a development package
```