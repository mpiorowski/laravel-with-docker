# Laravel application set up for docker deployment

The application is divided into two folders. 'Basic' contain barebone laravel app.  
'Complex' contain app with a simple Link model, test data generator, form submision and test units.  
## Deployment

Configuration files:
- app config : .env
- php server : php/local.ini
- nginx server : nginx/conf.d/app.conf
- mysql database: mysql/my.cnf

First install required packages for Laravel:
```
composer install
```
Then create application configuration file from exampled one. It already contains default database settings which are also located inside docker-compose file:
```
cp .env.example .env
``` 

Everything important is located inside docker-compose.yml file. 
All that is need is to run docker-compose command:

```
docker-compose up --build -d
```

This command will create 3 containers, containing php server, nginx server and mysql database with pre-created user, all connected with each other. This operation can take a while.   

Next the key for Laravel framework must be generated:
```
docker-compose exec app php artisan key:generate
```

Cache the settings:
```
docker-compose exec app php artisan config:cache
```

Check if the application is connected to the databse:
```
docker-compose exec app php artisan migrate
```
It should return something like this:
```
Migration table created successfully.
Migrating: 2014_10_12_000000_create_users_table
Migrated:  2014_10_12_000000_create_users_table
Migrating: 2014_10_12_100000_create_password_resets_table
Migrated:  2014_10_12_100000_create_password_resets_table
```

To access the application, enter http://localhost. Home page for Laravel default app should appear. 


 
