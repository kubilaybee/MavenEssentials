## Maven Essentials

This document explains the fundamental concepts, lifecycle, and key terms of Maven, a powerful tool for creating a standard structure and automated build process for Java projects.

### Maven Lifecycle

Maven uses a set of standard lifecycle stages to manage tasks such as compiling, testing, packaging, and deploying a project. These stages ensure that commands are executed in a specific order. When you run a stage, all stages before it are also automatically executed.

**`validate`**  

**Function:** Ensures that the project is valid and that all necessary information (in the `pom.xml` file) is correctly present.  
**Purpose:** To detect potential errors at the earliest stage by checking the project's underlying structure and dependencies before starting the build process.  

**`compile`**  

**Function:** Compiles the project's source code.  
**Purpose:** Converts all Java source files in the `src/main/java` directory to compiled bytecode (`.class` files) in the `target/classes` directory.  

**`test`**  

**Function:** Runs unit tests on the compiled source code.  
**Purpose:** Compiles the test code in the `src/test/java` directory, runs the unit tests, and reports the test results (pass/fail). If the tests fail, the lifecycle stops.  

**`package`**  

**Function:** Packages the compiled code into a distributable format.  
**Purpose:** Depending on the type of application, it bundles the compiled code into a JAR, WAR, or other archive format and places it in the `target` directory. This package is then ready to be run or distributed.  

**`integration-test`**  

**Task:** Runs integration tests.  
**Purpose:** Checks whether different components or external systems (database, services, etc.) work together properly using the packaged application. This phase is usually run in a separate test environment.  

**`verify`**  

**Task:** Performs various checks to verify the quality of the project.  
**Purpose:** Checks the results of the `integration-test` phase and may also run additional checks such as code quality analysis (e.g., code coverage check with Jacoco) and security scans.   

**`install`**  

**Task:** Installs the project's package to your local Maven repository (`.m2` directory).  
**Purpose:** This phase allows the project to be added as a dependency to other local projects. This allows other projects on the same machine to reference this project as a dependency.  

**`deploy`**  

**Function:** Uploads the project's package to a remote repository.  
**Purpose:** This phase makes the project accessible to other developers or CI/CD systems. It is typically used if you have an artifact repository (e.g., Nexus, Artifactory).  

---
### Basic Terms in Maven

**POM (Project Object Model)**  

**Definition:** This XML file contains all the project's configuration information (dependencies, plugins, build settings, etc.). It is located at the root of every Maven project.  

---

**Phase**  

**Definition:** Represents a specific step in a lifecycle. For example, `compile`, `test`, `package`, and `install` are all phases.  

---

**Goal**  

**Definition:** A specific task that a plugin can perform. A stage can run one or more targets. For example, the `compiler:compile` target is associated with the `compile` stage.  

---

**Plugin**  

**Definition:** A tool that extends Maven's core functionality. All functions, such as compilation, packaging, testing, and deployment, are performed through plugins.  

---

**Repository**  

**Definition:** This is where project dependencies, plugins, and compiled project packages are stored. There are three types:  
- **Local Repository:** A directory on your machine (`.m2`) where your downloaded dependencies are cached.
- **Central Repository:** Maven's default, online repository, which contains millions of open-source libraries.
- **Remote Repository:** Remote servers that host corporate or custom dependencies (e.g., Nexus, Artifactory).

---

**Dependency**  

**Definition:** External libraries or modules required by a project to function. These are defined in the `pom.xml` file under the `<dependencies>` tag.

---

**Scope**  

**Definition:** Determines when a dependency is available (compile, test, runtime). The most common scopes are:  
- **`compile`:** This is the default scope. The dependency is available in all project phases (compile, test, runtime).
- **`provided`:** Specifies that the dependency is available during the compile and test phases, but will be provided by the application's running environment at runtime.
- **`test`:** Specifies that the dependency will be available only when compiling and running the test code.

---

**Module**  

**Definition:** A subproject in a multi-module Maven project that is treated as a separate project. Each module has its own `pom.xml` file and is defined in the main project's `pom.xml` file. 

---

**Aggregator / Parent POM**  

**Definition:** This is the root `pom.xml` file of a multi-module project. It lists submodules and manages settings common to all modules. Subprojects inherit settings from this `parent` POM.  

---

**Dependency Management**  

**Definition:** This is a mechanism used in the `parent` POM. It allows for centrally managing versions of dependencies. When submodules add a dependency specified in the `<dependencyManagement>` block to their `<dependencies>` block, they do not need to specify version information.  

---

**Profiles**  

**Definition:** This is used to enable different settings based on different environments (development, test, production) or conditions. For example, it is ideal for managing different database connection information or plugin configurations.  
**Usage:** A specific profile can be activated with commands such as `mvn clean install -Pproduction`.

---

**Archetype**  

**Definition:** This is a project template used to create a new project. It automatically creates the project with a standard directory structure and basic `pom.xml` settings.

This revised document will provide a more complete and informative resource for your readers by compiling Maven's core mechanisms and important terms for practical use.  



### Commonly Used Maven Commands

Maven commands are used to manage a project's lifecycle. These commands begin with `mvn` in your project's root directory and are followed by one or more stages or targets.  

**`mvn --version`**

**Function:** Displays version information for Maven and Java.

**Purpose:** Used to check whether Maven is installed correctly on your system and which version you are using.

---

**`mvn clean`**

**Function:** Cleans the project's compiled output (`target` directory).

**Purpose:** Provides a clean compilation environment by deleting files left over from the previous build.

---

**`mvn compile`**

**Function:** Compiles the source code.

**Purpose:** Only compiles the code. Tests are not run with this command. Useful for a quick compilation check.

---

**`mvn test-compile`**

**Function:** Compiles the project's test code.

**Purpose:** Ensures that the test source code is compiled before running the tests. The `mvn test` command runs this step automatically.

---

**`mvn test`**

**Task:** Runs the project's unit tests.

**Purpose:** Runs the written tests to ensure the code is working correctly. If the tests fail, the process stops.

---

**`mvn package`**

**Task:** Converts the compiled code into a distributable package (usually a JAR or WAR file).

**Purpose:** Prepares the application in an executable or distributable file format. This command also automatically runs the `compile` and `test` phases.

---

**`mvn install`**

**Task:** In addition to the `package` command, it installs the resulting package into your local Maven repository.

**Purpose:** Enables other local projects to use the project as a dependency. It is one of the most frequently used commands in the development process.

---

**`mvn deploy`**

**Function:** In addition to the `install` command, it installs the project's package to a remote repository.

**Purpose:** Makes the application accessible to other developers or CI/CD tools.

---

**`mvn dependency:tree`**

**Function:** Lists all of the project's dependencies in a tree structure.

**Purpose:** Very useful for seeing dependency relationships, transitive dependencies, and potential version conflicts.

---

**`mvn help:effective-pom`**

**Function:** Displays a project's final `pom.xml` file (the effective POM).

**Purpose:** Shows a combined version of all settings from the parent POM and active profiles. This command is critical for understanding unexpected build behavior.

---

**`mvn spring-boot:run`**

**Function:** Runs the Spring Boot application.

**Purpose:** Provides a rapid development cycle by compiling the project and running it directly without creating the package.
