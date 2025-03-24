# Spring Common Parent

This project serves as a parent POM for managing Spring Boot applications, centralizing the Spring Boot version and shared configurations across multiple modules.

## Features

- **Spring Boot Version Management**: Centralizes the version of Spring Boot used across all child modules to ensure consistency and simplify updates.
- **Common Plugin Configurations**: Provides a common setup for Maven plugins, including:
  - **Spotless Code Formatter**: Enforces code formatting rules using the Spotless plugin, ensuring code quality and consistency across the project.

## Requirements

- Java 17
- Spring Boot 3.4.1
- Apache Maven 3.8.6

## How to Use

1. **Inherit from the Parent POM**: In your child modules, configure the parent and repositories as follows in the `pom.xml`:

   ```xml
   <parent>
       <groupId>com.erebelo</groupId>
       <artifactId>spring-common-parent</artifactId>
       <version>1.0.0</version>
   </parent>
   ```

   ```xml
     <repositories>
       <repository>
         <id>github</id>
         <url>https://maven.pkg.github.com/erebelo/spring-common-parent</url>
       </repository>
     </repositories>
   ```

   **NOTE**: Make sure to update the version of the parent POM as needed based on the project’s versioning.

2. **Add Dependencies**: Add your specific dependencies to the child module's `pom.xml` as needed.

3. **Build Your Project**: When you build your project, the Spotless plugin will automatically format your code according to the specified rules.

## Run App

Use the following command to build and format the project:

```sh
mvn clean install
```

## Publish a New Package/Release Version

To publish a new version of the package to GitHub Packages, follow these steps:

1. **Generate a Personal Access Token**:

   - Go to GitHub account -> **Settings** -> **Developer settings** -> **Personal access tokens** -> **Tokens (classic)** -> **Generate new token (classic)**.
   - Fill out the **Note** field: `Package publishing`.
   - Set the following scopes:
     - `write:packages` (to publish packages)
     - `read:packages` (to download packages)
     - `delete:packages` (if you want to delete packages)
   - Click **Generate token**.

2. **Set Up Maven Authentication**:

   - In your local Maven `settings.xml`, define the GitHub repository authentication using the following structure:

     ```xml
     <servers>
       <server>
         <id>github</id>
         <username>USERNAME</username>
         <password>TOKEN</password>
       </server>
     </servers>
     ```

   **NOTE**: Replace `USERNAME` with your GitHub username and `TOKEN` with the personal access token you just generated.

3. **Deploy to GitHub Packages**:

   - Inside IntelliJ IDEA, open your project and navigate to **Maven** -> **Execute Maven Goal**.
   - In the **Goal** field, enter `deploy` and click **OK**. This will run `mvn deploy` using the authentication settings from your `settings.xml`.

4. **Verify the Package**:
   - Once the deployment is successful, navigate to your GitHub repository and go to the **Packages** tab to verify that the new version of the package is listed.
