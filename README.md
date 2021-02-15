# Introduction
Apache Maven is both a build tool as well as a dependency management tool. More than that, it is a project management tool. It allows you to create a project without tying to any specific IDE like Eclilpse or InteliJIDE.

## Comparison with Ant
- Ant is just a build tool. Maven is a project management tool. It does more than just building the project.
- Ant needs Ivy for dependency management. With Maven, dependency management is covered automatically.
- If all projects are created with Maven, they follow the same industry approved convention for projects.
- In Ant, if our project is dependent on another Jar, then you have to download that Jar file and put it in a directory and then make Ant point to it for completing the build.     With Maven, that happens automatically.



In general, a typical project structure looks as shown below:
1. Source code
2. Test code
3. Resources
4. Dependencies
5. Configuration
6. Task Runner - build, test and run
7. Reporting.

# Maven project structure
1. src/main/java contains the source code
2. src/test/java contains the unit test cases.

```
  my-app
  |-- pom.xml
   -- src
      |-- main
      |   -- java
      |        -- com
      |            -- mycompany
      |                -- app
      |                    -- App.java
       -- test
           -- java
               -- com
                   -- mycompany
                       -- app
                           -- AppTest.java
```

# Repositories
Maven has the concept of respositories where it stores the artifacts. When you run Maven to build or package an application on your local computer, the dependencies that you specify, for example, jUnits, are downloaded from the central remote repository.
After build, it also creates a local repository where it would store the artifacts. So if you have another application configured which uses the first application's artificats, then Maven picks them from this local repository.

# POM.xml
Central to Maven, is the POM.xml file. Project Object Model is its full name. It defines what the project settings are. To be more precise, the ArtifactID, the GroupID, the artificat version, the build properties, the dependencies, the packaging etc. The combination of ArtifactID, the GroupID and the artifact version are what tells Maven which artificat among many versions it has to load. These three are together called as Coordinates.

Below is one such sample POM.xml file

```xml
  <?xml version="1.0" encoding="UTF-8"?>

  <project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>io.bubblesort.maventutorial</groupId>
    <artifactId>io.bubblesort.mavenartifact</artifactId>
    <version>1.0-SNAPSHOT</version>

    <name>io.bubblesort.mavenartifact</name>
    <!-- FIXME change it to the project's website -->
    <url>http://www.example.com</url>

    <properties>
      <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
      <maven.compiler.source>1.7</maven.compiler.source>
      <maven.compiler.target>1.7</maven.compiler.target>
    </properties>

    <dependencies>
      <dependency>
        <groupId>junit</groupId>
        <artifactId>junit</artifactId>
        <version>4.11</version>
        <scope>test</scope>
      </dependency>
    </dependencies>

    <build>
      <pluginManagement><!-- lock down plugins versions to avoid using Maven defaults (may be moved to parent pom) -->
        <plugins>
          <!-- clean lifecycle, see https://maven.apache.org/ref/current/maven-core/lifecycles.html#clean_Lifecycle -->
          <plugin>
            <artifactId>maven-clean-plugin</artifactId>
            <version>3.1.0</version>
          </plugin>
          <!-- default lifecycle, jar packaging: see https://maven.apache.org/ref/current/maven-core/default-bindings.html#Plugin_bindings_for_jar_packaging -->
          <plugin>
            <artifactId>maven-resources-plugin</artifactId>
            <version>3.0.2</version>
          </plugin>
          <plugin>
            <artifactId>maven-compiler-plugin</artifactId>
            <version>3.8.0</version>
          </plugin>
          <plugin>
            <artifactId>maven-surefire-plugin</artifactId>
            <version>2.22.1</version>
          </plugin>
          <plugin>
            <artifactId>maven-jar-plugin</artifactId>
            <version>3.0.2</version>
          </plugin>
          <plugin>
            <artifactId>maven-install-plugin</artifactId>
            <version>2.5.2</version>
          </plugin>
          <plugin>
            <artifactId>maven-deploy-plugin</artifactId>
            <version>2.8.2</version>
          </plugin>
          <!-- site lifecycle, see https://maven.apache.org/ref/current/maven-core/lifecycles.html#site_Lifecycle -->
          <plugin>
            <artifactId>maven-site-plugin</artifactId>
            <version>3.7.1</version>
          </plugin>
          <plugin>
            <artifactId>maven-project-info-reports-plugin</artifactId>
            <version>3.0.0</version>
          </plugin>
        </plugins>
      </pluginManagement>
    </build>
  </project>
```

## A closer look
* properties - determines what properties are to be applied during build and packaging
* dependencies - determine what all are dependent libraries, jars
* groupId - determines the group or the organization that is creating the project.
* artifcatId - determines the name of the artificat.
* version -  determines the version of the artificat.
* name - The general name for the project.

Ex: Gitlab4J's POM.xml 

```xml
<modelVersion>4.0.0</modelVersion>
<groupId>org.gitlab4j</groupId>
<artifactId>gitlab4j-api</artifactId>
<packaging>jar</packaging>
<version>4.15.8-SNAPSHOT</version>
<name>GitLab4J-API - GitLab API Java Client</name>
<description>GitLab4J-API (gitlab4j-api) provides a full featured Java client library for working with GitLab repositories and servers via the GitLab REST API.</description>
<url>https://github.com/gitlab4j/gitlab4j-api</url>
```

# Super POM
All the Maven projects have overridden content in them. That means only the content that is updated by the project are listed in the POM.xml. All other information is inherited from the Super POM.xml file. This is present on the Maven repository.

# Effective POM
The net POM is nothing but the resultant POM for a given project taking into account its Super POM. This can be see by executing the command `mvn help:effective-pom`.

# Examples

* **mvn archetype:generate**
We can use the command mvn archetype:generate to generate a project hierarchy for that archetype. Archetype is like a template. You have different archetypes for different types of applications - web applications, spring boot applications etc. Once selected, a preset configuration is applied to the pom.xml with dependencies, etc. This project can load into eclipse or any other IDE directly. As of this moment, there were around 1700+ archetypes.

* **mvn compile**
Used for compiling the source code in the project.

* **mvn package**
Used for packaging the compiled source into Jar/War.

# Build Lifecycle

The build process is managed by various identifiers in Maven, called as phases. These are listed below:

* validate: validate the project is correct and all necessary information is available
* compile: compile the source code of the project
* test: test the compiled source code using a suitable unit testing framework. These tests should not require the code be packaged or deployed
* package: take the compiled code and package it in its distributable format, such as a JAR.
* integration-test: process and deploy the package if necessary into an environment where integration tests can be run
* verify: run any checks to verify the package is valid and meets quality criteria
* install: install the package into the local repository, for use as a dependency in other projects locally
* deploy: done in an integration or release environment, copies the final package to the remote repository for sharing with other developers and projects.
* clean: cleans up artifacts created by prior builds
* site: generates site documentation for this project

When a single phase is executed, it executes all the phases above it as well. For example, running test would also run **validate** and **compile** as well. 

Ex: 

D:\Development\maven-learn\io.bubblesort.mavenartifact>mvn **compile**  
[INFO] Scanning for projects...  
[INFO]  
[INFO] ------< io.bubblesort.maventutorial:io.bubblesort.mavenartifact >-------  
[INFO] Building io.bubblesort.mavenartifact 1.0-SNAPSHOT  
[INFO] --------------------------------[ jar ]---------------------------------  
[INFO]  
[INFO] --- maven-resources-plugin:3.0.2:resources (default-resources) @ io.bubblesort.mavenartifact ---  
[INFO] Using 'UTF-8' encoding to copy filtered resources.  
[INFO] skip non existing resourceDirectory D:\Development\maven-learn\io.bubblesort.mavenartifact\src\main\resources  
[INFO]  
[INFO] --- maven-compiler-plugin:3.8.0:compile (default-compile) @ io.bubblesort.mavenartifact ---  
[INFO] Nothing to compile - all classes are up to date  
[INFO] ------------------------------------------------------------------------  
[INFO] BUILD SUCCESS  
[INFO] ------------------------------------------------------------------------  
[INFO] Total time:  0.664 s  
[INFO] Finished at: 2021-02-15T16:06:19+05:30  
[INFO] ------------------------------------------------------------------------  

Ex:
D:\Development\maven-learn\io.bubblesort.mavenartifact>mvn **test**  
[INFO] Scanning for projects...  
[INFO]  
[INFO] ------< io.bubblesort.maventutorial:io.bubblesort.mavenartifact >-------  
[INFO] Building io.bubblesort.mavenartifact 1.0-SNAPSHOT  
[INFO] --------------------------------[ jar ]---------------------------------  
[INFO]  
[INFO] --- maven-resources-plugin:3.0.2:resources (default-resources) @ io.bubblesort.mavenartifact ---  
[INFO] Using 'UTF-8' encoding to copy filtered resources.  
[INFO] skip non existing resourceDirectory D:\Development\maven-learn\io.bubblesort.mavenartifact\src\main\resources  
[INFO]  
[INFO] --- maven-compiler-plugin:3.8.0:compile (default-compile) @ io.bubblesort.mavenartifact ---  
[INFO] Changes detected - recompiling the module!  
[INFO] Compiling 1 source file to **D:\Development\maven-learn\io.bubblesort.mavenartifact\target\classes**  
[INFO]  
[INFO] --- maven-resources-plugin:3.0.2:testResources (default-testResources) @ io.bubblesort.mavenartifact ---  
[INFO] Using 'UTF-8' encoding to copy filtered resources.  
[INFO] skip non existing resourceDirectory D:\Development\maven-learn\io.bubblesort.mavenartifact\src\test\resources  
[INFO]  
[INFO] --- maven-compiler-plugin:3.8.0:testCompile (default-testCompile) @ io.bubblesort.mavenartifact ---  
[INFO] Changes detected - recompiling the module!  
[INFO] Compiling 1 source file to D:\Development\maven-learn\io.bubblesort.mavenartifact\target\test-classes  
[INFO]  
[INFO] --- maven-surefire-plugin:2.22.1:test (default-test) @ io.bubblesort.mavenartifact ---  
[INFO]  
[INFO] -------------------------------------------------------  
[INFO]  T E S T S  
[INFO] -------------------------------------------------------  
[INFO] Running io.bubblesort.maventutorial.AppTest  
[INFO] Tests run: 1, Failures: 0, Errors: 0, Skipped: 0, Time elapsed: 0.049 s - in io.bubblesort.maventutorial.AppTest  
[INFO]  
[INFO] Results:  
[INFO]  
[INFO] Tests run: 1, Failures: 0, Errors: 0, Skipped: 0  
[INFO]  
[INFO] ------------------------------------------------------------------------  
[INFO] BUILD SUCCESS  
[INFO] ------------------------------------------------------------------------  
[INFO] Total time:  2.442 s  
[INFO] Finished at: 2021-02-15T16:16:20+05:30  
[INFO] ------------------------------------------------------------------------

# Dependencies

All the external dependencies in Java projects are to be available in the form of Jar files for a Java project. For this, the developer needs to download the Jar files. In Maven, this is managed by XML statements in POM.xml file.

``` XML
<dependency>
    <groupId>org.slf4j</groupId>
    <artifactId>slf4j-api</artifactId>
    <version>1.7.30</version>
</dependency>
```

Note that the default scope for a dependency in Maven is Compile.


