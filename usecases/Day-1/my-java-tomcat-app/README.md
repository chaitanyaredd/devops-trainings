# My Java Tomcat Application

This is a simple Java web application that runs on a Tomcat server. The application demonstrates the use of servlets and JSP for handling web requests and rendering dynamic content.

## Project Structure

```
my-java-tomcat-app
├── pom.xml
├── Dockerfile
├── .dockerignore
├── .gitignore
├── README.md
├── src
│   ├── main
│   │   ├── java
│   │   │   └── com
│   │   │       └── example
│   │   │           └── AppServlet.java
│   │   ├── resources
│   │   │   └── application.properties
│   │   └── webapp
│   │       ├── index.jsp
│   │       └── WEB-INF
│   │           └── web.xml
│   └── test
│       └── java
│           └── com
│               └── example
│                   └── AppServletTest.java
```

## Setup Instructions

1. **Prerequisites**: Ensure you have Java JDK, Maven, and Tomcat installed on your machine.

2. **Build the Project**: Navigate to the project directory and run the following command to build the project:
   ```
   mvn clean package
   ```

3. **Deploy to Tomcat**: After building the project, you will find the WAR file in the `target` directory. Copy this WAR file to the `webapps` directory of your Tomcat installation.

4. **Start Tomcat**: Start the Tomcat server. You can do this by navigating to the `bin` directory of your Tomcat installation and running:
   ```
   ./catalina.sh start   (on Unix/Linux)
   catalina.bat start    (on Windows)
   ```

5. **Access the Application**: Open a web browser and go to `http://localhost:8080/my-java-tomcat-app` to access the application.

## Usage

The application responds to GET requests at the root URL. You can modify the `AppServlet` class to change the response or add more functionality.

## Additional Information

- The application uses Maven for dependency management. You can add additional dependencies in the `pom.xml` file.
- The `application.properties` file can be used to configure various settings for the application.
- Unit tests for the servlet are located in the `src/test/java/com/example/AppServletTest.java` file. You can run these tests using Maven with the command:
  ```
  mvn test
  ```

Feel free to explore and modify the application as needed!