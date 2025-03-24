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

1. **Generate a Personal Access Token**:

   Go to your GitHub account -> **Settings** -> **Developer settings** -> **Personal access tokens** -> **Tokens (classic)** -> **Generate new token (classic)**:

   - Fill out the **Note** field: `Pull packages`.
   - Set the scope:
     - `read:packages` (to download packages)
   - Click **Generate token**.

2. **Set Up Maven Authentication**:

   In your local Maven `settings.xml`, define the GitHub repository authentication using the following structure:

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

3. **Inherit from the Parent POM**: In your child modules, configure the parent and repositories as follows in the `pom.xml`:

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

4. **Add Dependencies**: Add your specific dependencies to the child module's `pom.xml` as needed.

5. **Build Your Project**: When you build your project, the Spotless plugin will automatically format your code according to the specified rules.

## Run App

Use the following command to build and format the project:

```sh
mvn clean install
```

## Publish a New Package Version

To publish a new version of the package to GitHub Packages, follow these steps:

1. **Generate a Personal Access Token**:

   Go to GitHub account -> **Settings** -> **Developer settings** -> **Personal access tokens** -> **Tokens (classic)** -> **Generate new token (classic)**.

   - Fill out the **Note** field: `Package publishing`.
   - Set the following scopes:
     - `write:packages` (to publish packages)
     - `read:packages` (to download packages)
     - `delete:packages` (if you want to delete packages)
   - Click **Generate token**.

2. **Set Up Maven Authentication**:

   In your local Maven `settings.xml`, define the GitHub repository authentication using the following structure:

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

3. **Update the Package Version**:

   - Create a release branch from the `main` branch, named `release-X.X.X`, where `X.X.X` is the new version number you want to publish:

     ```sh
     git checkout main
     git checkout -b release-2.0.0
     ```

   - Update the version in pom.xml of the project to the desired new version number:

     ```xml
     <version>2.0.0</version>
     ```

   - Commit and push the changes to the remote repository:

     ```sh
     git add .
     git commit -m "Package release version 2.0.0"
     git push origin release-X.X.X
     ```

4. **Deploy to GitHub Packages**:

   Inside IntelliJ IDEA, open your project and navigate to **Maven** -> **Execute Maven Goal**:

   - Enter `deploy` and press **Enter**. This will run `mvn deploy` using the authentication settings from your `settings.xml`.

5. **Verify the Package**:
   Once the deployment is successful, navigate to your GitHub repository and go to the **Packages** section to verify that the new version of the package is listed.
