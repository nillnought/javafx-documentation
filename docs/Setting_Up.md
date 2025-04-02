# Setting Up Your JavaFX Project
<!-- overview -->
## Overview
This section will guide you through setting up a JavaFX project in IntelliJ IDEA. By the end of this tutorial, you'll have a basic JavaFX project ready to build on.

## Step 1: Install JavaFX SDK (Optional)
<!-- Installing the SDK -->
![Image Title](https://dummyimage.com/600x400/eee/aaa"ImageTitle"){: .center-image}

1. Visit the official [JavaFX website](https://openjfx.io/).
2. Download the appropriate JavaFX SDK for your operating system.
   - For Windows: Download the `.zip` file.
   - For macOS: Download the `.dmg` file.
3. Extract the downloaded file to a location on your machine (e.g., `C:\javafx-sdk`).  
   This step is optional as Maven will handle dependencies, but it’s helpful for development or debugging purposes.

## Step 2: Create a New Maven Project
<!-- creating the project in intelliJ -->
![Image Title](https://dummyimage.com/600x400/eee/aaa"ImageTitle"){: .center-image}

1. Open IntelliJ IDEA.
2. Click on **New Project**.
3. Select **Maven** from the left-hand menu.
4. Check **Create from archetype** and select `maven-archetype-quickstart`. Click **Next**.
5. Configure your project:
   - **GroupId**: Enter your package name (e.g., `com.example`).
   - **ArtifactId**: Enter your project name (e.g., `javafx-maven-app`).
   - **Version**: Leave as default unless specific instructions are given.
6. Click **Finish** to create your Maven project.

## Step 3: Add JavaFX Dependencies to `pom.xml`
<!-- adding dependencies to pom.xml  -->
![Image Title](https://dummyimage.com/600x400/eee/aaa"ImageTitle"){: .center-image}

1. Open the `pom.xml` file in the root of your project.
2. Add the following `<dependencies>` section to include JavaFX:

   ```xml
   <dependencies>
       <!-- JavaFX dependencies -->
       <dependency>
           <groupId>org.openjfx</groupId>
           <artifactId>javafx-controls</artifactId>
           <version>19</version> <!-- Replace with the current JavaFX version -->
       </dependency>
       <dependency>
           <groupId>org.openjfx</groupId>
           <artifactId>javafx-fxml</artifactId>
           <version>19</version> <!-- Replace with the current JavaFX version -->
       </dependency>
   </dependencies>
   ```

!!! note
Replace 19 with the version of JavaFX you are using. You can find the latest version on the [Maven Repository](https://mvnrepository.com/artifact/org.openjfx).

3. Add the JavaFX Maven plugin to your pom.xml under the <build> section:

    ```xml
    <build>
        <plugins>
            <plugin>
                <groupId>org.openjfx</groupId>
                <artifactId>javafx-maven-plugin</artifactId>
                <version>0.0.13</version> <!-- Replace with the current plugin version -->
                <configuration>
                    <mainClass>com.example.Main</mainClass> <!-- Replace with your main class -->
                </configuration>
            </plugin>
        </plugins>
    </build>
    ```
!!! warning
Ensure that the mainClass field matches the fully qualified name of your Main class (e.g., com.example.Main).

## Step 4: Create the Main JavaFX Application
<!-- creating main application -->
![Image Title](https://dummyimage.com/600x400/eee/aaa"ImageTitle"){: .center-image}

1. Navigate to the `src/main/java folder` in your project structure.
2. Create a new Java class (e.g., `Main.java`) in your package (e.g., `com.example`).
3. Paste the following code into your class:

    ```java
    package com.example;

    import javafx.application.Application;
    import javafx.scene.Scene;
    import javafx.scene.control.Label;
    import javafx.stage.Stage;

    public class Main extends Application {
        @Override
        public void start(Stage primaryStage) {
            Label label = new Label("Hello, JavaFX with Maven!");
            Scene scene = new Scene(label, 400, 300);
            primaryStage.setScene(scene);
            primaryStage.setTitle("JavaFX Maven App");
            primaryStage.show();
        }

        public static void main(String[] args) {
            launch(args);
        }
    }
    ```

## Step 5: Run the Maven Project
<!-- running maven project -->
![Image Title](https://dummyimage.com/600x400/eee/aaa"ImageTitle"){: .center-image}

1. Open the **Terminal** in IntelliJ IDEA.
2. Use the following Maven command to compile and run your application:

    ```plaintext
    mvn javafx:run
    ```
!!! success
If everything is set up correctly, a window will appear with the text "Hello, JavaFX with Maven!".

## Step 6: Add Elements to the Scene
<!-- how to add shapes and buttons to a scene, end goal is a title screen. -->
1. Open your `Main.java` file.
2. Use a `VBox` (Vertical Box) layout to organize your elements.
3. Add a title, "Start" button, and "Exit" button to the layout. Use the following code:

   ```java title="Main.java" linenums="1"
   @Override
   public void start(Stage primaryStage) {
       // Create a VBox layout
       VBox layout = new VBox(20); // 20px spacing between elements
       layout.setAlignment(Pos.CENTER); // Center elements

       // Add a title
       Text title = new Text("Welcome to My Game!");
       title.setFont(Font.font("Arial", FontWeight.BOLD, 24));

       // Add buttons
       Button startButton = new Button("Start");
       Button exitButton = new Button("Exit");

       // Add button functionality
       startButton.setOnAction(e -> System.out.println("Game Started!")); // Placeholder for starting the game
       exitButton.setOnAction(e -> primaryStage.close()); // Close the application

       // Add elements to the layout
       layout.getChildren().addAll(title, startButton, exitButton);

       // Create the scene
       Scene scene = new Scene(layout, 400, 300);
       primaryStage.setScene(scene);
       primaryStage.setTitle("Title Screen");
       primaryStage.show();
   }
   ```
4. Run your application. You should see a title screen with the title "Welcome to My Game!" centered at the top, followed by the "Start" and "Exit" buttons.

!!! success
Clicking the Start button will print "Game Started!" to the console, and clicking the Exit button will close the application.

## Conclusion
<!-- end product is a simple title screen with a start button, exit button and title. -->
You’ve now created a simple title screen with a title, "Start" button, and "Exit" button. Below is the complete code for your Main class:

    ```java title="Main.java" linenums="1"
    import javafx.application.Application;
    import javafx.geometry.Pos;
    import javafx.scene.Scene;
    import javafx.scene.control.Button;
    import javafx.scene.layout.VBox;
    import javafx.scene.text.Font;
    import javafx.scene.text.FontWeight;
    import javafx.scene.text.Text;
    import javafx.stage.Stage;

    public class Main extends Application {
        @Override
        public void start(Stage primaryStage) {
            // Create a VBox layout
            VBox layout = new VBox(20);
            layout.setAlignment(Pos.CENTER);

            // Add a title
            Text title = new Text("Welcome to My Game!");
            title.setFont(Font.font("Arial", FontWeight.BOLD, 24));

            // Add buttons
            Button startButton = new Button("Start");
            Button exitButton = new Button("Exit");

            // Add button functionality
            startButton.setOnAction(e -> System.out.println("Game Started!"));
            exitButton.setOnAction(e -> primaryStage.close());

            // Add elements to the layout
            layout.getChildren().addAll(title, startButton, exitButton);

            // Create the scene
            Scene scene = new Scene(layout, 400, 300);
            primaryStage.setScene(scene);
            primaryStage.setTitle("Title Screen");
            primaryStage.show();
        }

        public static void main(String[] args) {
            launch(args);
        }
    }
    ```

    With this, your title screen is ready. In the next steps, you can expand it further by adding more features or transitioning to other scenes when the "Start" button is pressed.