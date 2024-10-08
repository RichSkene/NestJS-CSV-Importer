# Notes on Project

The code for this project is a sample from a rebuild of a website for a data driven company. The task was to take CSV files of the data, which were exported from an Access database, and import them into a relational database and expose the data using a GraphQL API for a seperate frontend to consume.

## Nest
The project is built on the [NestJS](https://nestjs.com/) framework and can be run with the standard commands with the prerequisite that Node version 22 is installed.
```bash
npm install
npm run build
npm run start:dev
```

## Dockerisation
The original project didn't use docker for containerisation but this example has a Dockerfie that can be used to to create a docker image to run the codebase in a Docker container.

The image is built in stages to minimise the final file size and only contains code required for the production deployment of the project.
### Docker Compose (dev)
There is also a Docker compose file which should only be used in a local development environement as it overrides the containers CDM at startup, which installs all npm dependencies including the dev dependencies, which the production image doesn't have by default.
Using the following command Docker commose will initiate the project on port 3000 and also provision a MySQL container. Docker also volumes to sync the code from the host machine to the container.
```bash
docker compose up --build -d
```
Within the new container the dev server for NestJS will be started along with a watcher for automatic recompiling of the code from changes on the host machine.

## Database
[TypeORM](https://typeorm.io/) is used to map the entities and relationships between objects and to keep the Mysql database schema up to date using migrations.

## The API
GraphQL is used to expose the data from the DB and [Nestjs-query](https://tripss.github.io/nestjs-query/docs/introduction/getting-started/) package was used to easily provide the mapping between requests and the objects and data queried for.

