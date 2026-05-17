# EM Services

A demo project consisting of 4 services managing users and cards.

## Getting started

1. Clone. Be sure Git is installed.
```shell
git clone https://github.com/NadChel/em-services
```
2. Navigate to the project root.
```shell
cd em-services
```
3. Run `docker-compose.yml`. Docker Engine should be running (on Windows, you can open Docker Desktop).
```shell
docker-compose up
```
4. Once the services are up, open their UI pages and visit the endpoints. By default, UI is exposed at `localhost:<port>/swagger-ui.html`.

## Composition

| Service           | Description                                                                  | Default port | GH                                                      | DH                                                                             |
|-------------------|------------------------------------------------------------------------------|--------------|---------------------------------------------------------|--------------------------------------------------------------------------------|
| migration-service | Initializes the DB on start-up and exits.                                    | N/A          | [link](https://github.com/NadChel/em-migration-service) | [link](https://hub.docker.com/repository/docker/nadchel/em-migration-service/) |
| token-service     | Performs user login, issuing signed JWTs.                                    | 8080         | [link](https://github.com/NadChel/em-token-service)     | [link](https://hub.docker.com/repository/docker/nadchel/em-token-service/)     |
| user-service      | Manages users: selects, saves, deletes.                                      | 8090         | [link](https://github.com/NadChel/em-user-service)      | [link](https://hub.docker.com/repository/docker/nadchel/em-user-service/)      |
| card-service      | Manages cards: selects, saves, status updates. Also, deposits and transfers. | 8100         | [link](https://github.com/NadChel/em-card-service)      | [link](https://hub.docker.com/repository/docker/nadchel/em-card-service/)      |
| db                | PostgreSQL database.                                                         | 5432         | N/A                                                     | [link](https://hub.docker.com/_/postgres)                                      |

## Notes

* All business endpoints, except `/login`, require authentication. Once you've successfully logged in via the `token-service` and got a JWT string, click the `Authorize` button in a service's UI and paste it in the `Value` field.
* `*/admin/**` endpoints require ADMIN privileges.
* The root admin, if absent, is created automatically on `user-service` start-up (admin:admin by default). It's the only user that exists in the database on the first run.
* If you want to run it in your IDE (not with `docker-compose`), be sure to include an `.env` file in the `card-service` root. The file must specify `APP_ENCRYPTION_PASSWORD` and `APP_ENCRYPTION_SALT` (hexadecimal strings). `.env` is purposefully excluded from Git.
