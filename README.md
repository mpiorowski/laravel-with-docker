# Laravel application set up for docker deployment

Simple application using laravel php framework with docker-compose for deployment.

## Deployment

Configuration files:
- php server : php/local.ini
- nginx server : nginx/conf.d/app.conf
- mysql database: mysql/my.cnf

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

To access the application, enter http://localhost. The home page for Laravel default app should appear. 


 
