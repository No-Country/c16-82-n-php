# Backend configuration

## Installation

After cloning the repository, you need to run the `composer install` command using Docker.

```bash
docker run --rm \
    -u "$(id -u):$(id -g)" \
    -v "$(pwd):/var/www/html" \
    -w /var/www/html \
    laravelsail/php83-composer:latest \
    composer install --ignore-platform-reqs
```

## Sail alias

After installing packages, configure an alias for command `./vendor/bin/sail`. To make sure this is always available, you may add this to your shell configuration file in your home directory, such as ~/.zshrc or ~/.bashrc, and then restart your shell.

Add this line to the end of your shell configuration file.

```bash
alias sail='[ -f sail ] && sh sail || sh vendor/bin/sail'
```

## Add permissions to `./storage` folder

This command will give others permissions without altering user and group permissions.

```bash
sudo chmod o+w ./storage/ -R
```

You should also give access to the www-data user or group.

```bash
sudo chown www-data:www-data -R ./storage
```

## Add permissions to Sail

Granting permissions to the `sail` command on the `html` folder.

```bash
sail root-shell
cd ..
chown -R sail:sail htm
exit
```

## Run Autoload & Optimize

```bash
sail artisan clear-compiled 
sail composer dump-autoload
sail artisan optimize
```

## Copy `.env.example` file and rename to `.env`

Laravel need to use .env file to define a database connection, some general setting like application key as well.

## Laravel Artisan Key Command

The key:generate command is used to generate a random key. This command will update the key stored in the application's environment file.

```bash
sail artisan key:generate
```

## Start Sail

Before starting Sail, you should ensure that no other web 
servers or databases are running on your local computer. 
To start Sail you should execute the `up` command:

```bash
sail up
```

## Start Sail in background

```bash
sail up -d
```

## Stop sail

```bash
sail stop
```
