# Day 16 - Introduction to Maven
*Mon, 20 Jul 2026 (Week 4)*

## What Is Maven?

A powerful **build automation and project management tool** — manages project builds, dependencies, testing, packaging, and deployment in a standard way.

## Why Maven?

- Automatically downloading dependencies
- Providing a standard project structure
- Automating build processes
- Managing project lifecycle phases
- Simplifying collaboration

## Uses of Maven

1. Dependency management
2. Project build management
3. Testing
4. Packaging
5. Deployment
6. Documentation
7. Continuous Integration

Maven can download dependencies from:
1. **Local Repository** — on your machine (`~/.m2`)
2. **Central Repository** — Maven Central, the default public repo
3. **Remote Repository** — a custom/private repo (e.g. Nexus, Artifactory)

Maven also has **plugin support** — plugins do most of the actual work (compiling, packaging, testing) under the hood.

## POM (Project Object Model)

The **heart of a Maven project** — an XML file (`pom.xml`) containing:
- Project info
- Dependencies
- Plugins
- Build settings
- Repository info

### Types of POM

| Type | Description |
|---|---|
| **Super POM** | Provided by Maven itself — all projects inherit from it, contains default settings |
| **Simple POM** | Contains only basic project info |
| **Parent POM** | Shares common configuration (dependencies, plugin configs, version management) across multiple projects |
| **Child POM** | Inherits settings from a Parent POM |

### Core POM Elements

```xml
<modelVersion>4.0.0</modelVersion>

<!-- unique organization/company identifier -->
<groupId>com.jfs.training</groupId>

<!-- project name -->
<artifactId>Day16</artifactId>

<!-- project version -->
<version>0.0.1-SNAPSHOT</version>

<!-- jar, war, ear, pom -->
<packaging>jar</packaging>

<dependencies>
    <dependency>
        <!-- ... -->
    </dependency>
</dependencies>

<!-- plugins, output directories, build configuration -->
<build>
    <plugins>
        <plugin>
            <groupId>...</groupId>
            <artifactId>...</artifactId>
        </plugin>
    </plugins>
</build>

<properties>
    <java.version>8</java.version>
</properties>

<repositories>
    <repository>
        <id>...</id>
        <url>...</url>
    </repository>
</repositories>
```

## Maven Archetypes

A **project template** used to generate a Maven project structure automatically.

| Archetype | Purpose |
|---|---|
| **Quickstart Archetype** | Creates a simple Java application |
| **Web Application Archetype** | Creates a web application |
| **Site Archetype** | Used for documentation projects |

## Maven Lifecycle

Maven provides **3 built-in lifecycles**:

| Lifecycle | Phases |
|---|---|
| **Clean** | Removes previous build files |
| **Default / Build** | `validate → compile → test → package → install → deploy` |
| **Site** | Documentation generation |

### Common Commands

```bash
mvn clean
mvn compile
mvn test
mvn package
mvn install
mvn deploy
```

## Maven Goal

A **goal** is a specific task performed by Maven:

1. `compile`
2. `test`
3. `package`
4. `install`
5. `deploy`
6. `clean`
7. `site`

---
## Example `pom.xml` — JDBC Dependency + Executable Jar

```xml
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>
  <groupId>com.jfs.training</groupId>
  <artifactId>Day16</artifactId>
  <version>0.0.1-SNAPSHOT</version>
  <packaging>jar</packaging>

  <dependencies>
    <!-- Source: https://mvnrepository.com/artifact/com.mysql/mysql-connector-j -->
    <dependency>
      <groupId>com.mysql</groupId>
      <artifactId>mysql-connector-j</artifactId>
      <version>9.0.0</version>
      <scope>compile</scope>
    </dependency>
  </dependencies>

  <build>
    <plugins>
      <plugin>
        <groupId>org.apache.maven.plugins</groupId>
        <artifactId>maven-compiler-plugin</artifactId>
      </plugin>
      <plugin>
        <groupId>org.apache.maven.plugins</groupId>
        <artifactId>maven-jar-plugin</artifactId>
        <version>3.4.2</version>
        <configuration>
          <archive>
            <manifest>
              <mainClass>com.demo.App</mainClass>
            </manifest>
          </archive>
        </configuration>
      </plugin>
    </plugins>
  </build>
</project>
```

The `maven-jar-plugin` configuration sets the **main class** in the jar's manifest, so the packaged jar is directly runnable with `java -jar`.

## Extended Example — Adding Reporting Plugins

```xml
<build>
  <plugins>
    <plugin>
      <groupId>org.apache.maven.plugins</groupId>
      <artifactId>maven-compiler-plugin</artifactId>
    </plugin>
    <plugin>
      <groupId>org.apache.maven.plugins</groupId>
      <artifactId>maven-jar-plugin</artifactId>
      <version>3.4.2</version>
      <configuration>
        <archive>
          <manifest>
            <mainClass>com.demo.App</mainClass>
          </manifest>
        </archive>
      </configuration>
    </plugin>

    <!-- Generates a project info site (dependencies, plugins, etc.) -->
    <plugin>
      <groupId>org.apache.maven.plugins</groupId>
      <artifactId>maven-project-info-reports-plugin</artifactId>
      <version>3.9.0</version>
    </plugin>

    <!-- Generates an HTML test report from Surefire test results -->
    <plugin>
      <groupId>org.apache.maven.plugins</groupId>
      <artifactId>maven-surefire-report-plugin</artifactId>
      <version>3.1.2</version>
    </plugin>
  </plugins>
</build>
```

`maven-project-info-reports-plugin` and `maven-surefire-report-plugin` both feed into the **Site lifecycle** (`mvn site`) — they generate browsable HTML reports about the project and its test results.
