# TestContainers-Demo

This project demonstrates integration testing of a Spring Boot application using [Testcontainers](https://www.testcontainers.org/) with a MySQL database.

## Overview

- **Spring Boot** application with a simple `User` entity and REST API.
- **Testcontainers** is used to spin up a real MySQL Docker container for integration tests, ensuring tests run against an actual database environment.
- **Flyway** is used for database migrations (disabled during tests).

## Project Structure

```
src/
  main/
    java/com/testcontainer/demo/         # Application code
    resources/application.properties     # Main config
  test/
    java/com/testcontainer/demo/         # Integration tests
    resources/application.properties     # Test config
```

## How Testcontainers is Used

- Integration tests (see [`UserServiceIntegrationTest`](src/test/java/com/testcontainer/demo/UserServiceIntegrationTest.java)) start a MySQL container before tests run.
- Spring's `@DynamicPropertySource` dynamically injects the container's JDBC URL, username, and password into the test context.
- No need for a local MySQL installation or manual DB setup for tests.

## Running Tests

Ensure you have [Docker](https://www.docker.com/) running locally.

Run tests with Maven:

```sh
./mvnw test
```

Maven will:
- Start a MySQL Docker container for integration tests.
- Run your tests against this container.
- Stop and clean up the container after tests complete.

## Key Files

- [`UserServiceIntegrationTest.java`](src/test/java/com/testcontainer/demo/UserServiceIntegrationTest.java): Shows how to use Testcontainers with Spring Boot.
- [`application.properties`](src/test/resources/application.properties): Test configuration, disables Flyway and leaves datasource properties empty (Testcontainers fills them in).

## References

- [Testcontainers Documentation](https://www.testcontainers.org/)
- [Spring Boot Testcontainers Support](https://docs.spring.io/spring-boot/docs/current/reference/html/features.html#features.testing.testcontainers)
- [Flyway](https://flywaydb.org/)

---

**Note:**  
Testcontainers requires Docker to be running on your machine. If Docker is not running, tests will fail to start the MySQL container.