# TestContainers-Demo

This project demonstrates integration testing of a Spring Boot application using [Testcontainers](https://www.testcontainers.org/) with a MySQL database.

## Overview

- **Spring Boot** application with a simple `User` entity and CRUD REST API.
- **Testcontainers** is used to spin up a real MySQL Docker container for integration tests, ensuring tests run against an actual database environment, instead h2 DB Setup.

## How Testcontainers is Used

- Integration tests (see [`UserServiceIntegrationTest`](src/test/java/com/testcontainer/demo/UserServiceIntegrationTest.java)) start a MySQL container before tests run.
- Spring's `@DynamicPropertySource` dynamically injects the container's JDBC URL, username, and password into the test context if needs to be overridden.
- No need for a local MySQL installation or manual DB setup for tests.

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

## Key Files

- [`UserServiceIntegrationTest.java`](src/test/java/com/testcontainer/demo/UserServiceIntegrationTest.java): Shows how to use Testcontainers with Spring Boot.

## Running Tests

Ensure you have [Docker](https://www.docker.com/) running locally. 

Run tests with Maven:

```sh
mvn test
```

Maven will:
- Start a MySQL Docker container for integration tests.
- Run your tests against this container.
- Stop and clean up the container after tests complete.

## References

- [Testcontainers Documentation](https://www.testcontainers.org/)
- [Spring Boot Testcontainers Support](https://docs.spring.io/spring-boot/docs/current/reference/html/features.html#features.testing.testcontainers)
---