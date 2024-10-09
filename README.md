# Spring Common Parent

This project serves as a parent POM for managing Spring Boot applications, centralizing the Spring Boot version and shared configurations across multiple modules.

## Features

- **Spring Boot Version Management**: Centralizes the version of Spring Boot used across all child modules to ensure consistency and simplify updates.
- **Common Plugin Configurations**: Provides a common setup for Maven plugins, including:
    - **Spotless Code Formatter**: Enforces code formatting rules using the Spotless plugin, ensuring code quality and consistency across the project.

## Requirements

- Java 17
- Spring Boot 3.3.4
- Apache Maven 3.8.6

## How to Use

1. **Inherit from the Parent POM**: In your child modules, set the parent as follows in the `pom.xml`:

    ```xml
    <parent>
        <groupId>com.erebelo</groupId>
        <artifactId>spring-common-parent</artifactId>
        <version>1.0.1-SNAPSHOT</version>
    </parent>
    ```

2. **Add Dependencies**: Add your specific dependencies to the child module's `pom.xml` as needed.

3. **Build Your Project**: When you build your project, the Spotless plugin will automatically format your code according to the specified rules.

## Run App

Use the following command to build and format the project:

    ```bash
    mvn clean install
    ```
