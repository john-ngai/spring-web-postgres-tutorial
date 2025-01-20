# Tutorial: Spring Web and PostgreSQL

## References

- [Sammy Tran. (11 May 2023). Using Postgres Effectively in Spring Boot Applications. HackerNoon.](https://hackernoon.com/using-postgres-effectively-in-spring-boot-applications)
- [Spring Initialzr.](https://start.spring.io/)

## Environment Requirements

- Podman Desktop

## Getting Started

### PostgreSQL Database

1. Open the Podman Desktop application.

2. Download the latest postgres image:

```shell
podman pull postgres
```

3. Create and run the postgres container:

```shell
podman run --name postgres-db -e POSTGRES_PASSWORD=password -p 5432:5432 -d postgres
```

4. Connect to the postgres server:

```shell
podman exec -it postgres-db psql -U postgres
```

5. Create the new database:

```psl
CREATE DATABASE springwebdb OWNER postgres;
```

6. Connect to the database:

```psql
\c springwebdb
```

### Spring Boot Web Service

1. From another terminal, start the web service using:

```shell
mvn spring-boot:run
```

2. Test the connection by sending a GET request using curl:

```shell
curl -s localhost:8080/employees
```

3. Create an employee by sending a POST request:

```shell
curl -s -X POST localhost:8080/employees \
  -H "Content-Type: application/json" \
  -d '{"firstName": "foo", "lastName": "bar", "dateOfBirth": "2023-05-04"}'
```

4. Verify using curl:

```shell
curl -s localhost:8080/employees
```

5. Switch to the postgres terminal and verify again using psql:

```psql
SELECT * FROM employees;
```
