# TP 2 Docker

## ROUGEON Corentin



### 1. Compléter le Dockerfile afin de builder correctement l’application

````dockerfile
FROM node:12-alpine3.9

WORKDIR /usr/share/app/

COPY package.json .

RUN npm install

COPY . .

CMD ["node", "src/index.js"]
````

#### a. Une option de npm vous permet de n’installer que ce qui est nécessaire. Quelle est cette option ?

`npm install`

### 2. A l’aide de la commande docker build, créer l’image ma_super_app

`docker build -t tp2-docker .`

resultat `docker image ls` :

```
REPOSITORY                 TAG            IMAGE ID       CREATED         SIZE
ma_super_app               latest         7cd53ea54b14   6 minutes ago   191MB
tp2-docker                 latest         7cd53ea54b14   6 minutes ago   191MB
tp-docker                  latest         a3e8e3669fe4   2 weeks ago     142MB
ubuntu                     latest         6b7dfa7e8fdb   3 weeks ago     77.8MB
mysql                      5.7            d410f4167eea   3 weeks ago     495MB
nginx                      latest         ac8efec875ce   3 weeks ago     142MB
phpmyadmin/phpmyadmin      latest         4a4023c7e22a   7 months ago    510MB
praqma/network-multitool   latest         1631e536ed7d   12 months ago   39.9MB
hello-world                latest         feb5d9fea6a5   15 months ago   13.3kB
node                       12-alpine3.9   a7d6e4c06dd4   24 months ago   88.5MB
```


### 4. Compléter le fichier docker-compose.yml afin d’éxécuter ma_super_app avec sa base de données.

pour les variable environnement on peut voir que les variables sont appeler :

```    
DATABASE_HOST
DATABASE_PORT
DATABASE_USERNAME
DATABASE_PASSWORD
DATABASE_NAME
```

on peut aussi voir dans le code que `DATABASE_HOST` et `DATABASE_PORT` ne sont pas
requis pour run le script


````yml
version: '3.9'

services:
  node:
    image: ma_super_app
    ports:
    - "3000:3000"
    depends_on:
      - mysql
    environment:
      DATABASE_USERNAME: root
      DATABASE_PASSWORD: toor
      DATABASE_NAME: database

  mysql:
    image: mysql
    ports:
    - "3306:3306"
    environment:
      MYSQL_ROOT_PASSWORD: toor
      MYSQL_DATABASE: database
````

