# Docker Compose

Docker Compose is a very useful tool that allows you to spin up multiple containers for a single Docker application.  A great example of this might be a web application that uses a Django backend and a Postgres server.  After you create a configuration file, you can launch both with a single, easy command.  There are many features to docker-compose, and more details can be found on the [official website.](https://docs.docker.com/compose/overview/#features) 

The above web application example is just one of many [common use cases.](https://docs.docker.com/compose/overview/#common-use-cases)  Docker-compose works great in all environments, including production, staging, development, testing, and even with Continuous Integration (CI) workflows, such as TravisCI or Jenkins.

Docker Compose requires 3 simple steps.
1. For each individual Docker app, define the environment as you traditionally would in a `Dockerfile`. You will likely have multiple of these.
2. Define all services that make up your complete app inside a `docker-compose.yml` You will usually only need one of these. This file has configurations that allow your app to run in an isolated environment.
3. Run `docker-compose up` and Docker Compose will start, work its magic, and run your entire app.

## Configuration File
Configuration is done with a YAML file and is by default named `docker-compose.yml`. There are many [Docker Compose file configuration options](https://docs.docker.com/compose/compose-file/), but we will start with a basic one as an introduction:

```
version: '3'
services:
  db:
    image: postgres
  webapp:
    build: .
    command: python3 manage.py runserver 0.0.0.0:8080
    volumes:
      - .:/code
    ports:
      - "8080:8080"
    depends_on:
      - db
```

## Start your app
When you run `docker-compose up` you will begin to see your docker images start one at a time, just as if you had started them with docker run individually.  The benefit is now they can quite easily talk with each other, in addition to other isolation benefits.  Some output that you might expect would look like:

```
$ docker-compose up
cse_django_db_1 is up-to-date
Creating cse_django_web_1 ...
Creating cse_django_web_1 ... done
Attaching to cse_django_db_1, cse_django_web_1
db_1   | The files belonging to this database system will be owned by user "postgres".
db_1   | This user must also own the server process.
db_1   |
db_1   | The database cluster will be initialized with locale "en_US.utf8".
db_1   | The default database encoding has accordingly been set to "UTF8".
db_1   | The default text search configuration will be set to "english".
. . .
webapp_1  | May 30, 2017 - 21:44:49
webapp_1  | Django version 2.0.1, using settings 'composeexample.settings'
webapp_1  | Starting development server at http://0.0.0.0:8080/
webapp_1  | Quit the server with CONTROL-C.
```

If you are familiar with Django, or even just take a glance at the end of the output, you can expect that you can now access your web application by visiting `http://localhost:8080` using a web browser.

## Stopping your app
To stop your app, simply type `docker-compose down` or by typing `Ctrl-C` in the shell that it is currently running.

## And that's it!
Docker Compose is a great tool that started out as a separate project until it became so popular that the core team integrated it as a supported feature. Aside from more easily managing an app that contains multiple docker containers, it is also great single container apps as well, allowing you to forget some of the more common docker commands and stick to simple up and down commands.