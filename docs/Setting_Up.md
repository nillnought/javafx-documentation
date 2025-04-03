# Setting Up Your JavaFX Project
<!-- overview -->
## Overview
Welcome to your JavaFX adventure! If you're new to desktop application development or just getting started with JavaFX, don't worry - we've got you covered. This comprehensive guide will walk you through every step of creating your first JavaFX project, from setting up your development environment to creating your first interactive scene.

## Getting Started: Preparing Your Development Environment

### Enabling the JavaFX Plugin
Let's kick things off by making sure you have the JavaFX plugin installed and ready to go:

1. Open IntelliJ IDEA and navigate to the Plugins section
   - Go to File > Settings (on Windows/Linux) or IntelliJ IDEA > Preferences (on macOS)
   - Click on the "Plugins" tab on the left side of the window

2. In the search bar, type "JavaFX"
   - Look for the official JavaFX plugin
   - If it's not installed, click "Install" 
   - If it's already installed, make sure it's enabled by checking the box next to the plugin

!!! tip
    The JavaFX plugin provides additional support and tools that make developing JavaFX applications much smoother. It includes helpful code completion, scene builder integration, and other useful features.

### Creating Your First JavaFX Project
<!-- creating the project in intelliJ -->
![Image Title](https://dummyimage.com/600x400/eee/aaa"ImageTitle"){: .center-image}

Now that the plugin is ready, let's create your project:

1. Click on "New Project" from the IntelliJ IDEA welcome screen
   - Alternatively, you can go to File > New > Project

2. On the left side, select "JavaFX" from the project types
   - If you don't see JavaFX immediately, make sure you've installed the plugin correctly

3. Project Configuration:
   - Choose a meaningful name for your project (e.g., "JavaFXTutorial")
   - Select a location to save your project
   - (Optional but recommended) Check the "Create Git repository" box if you want version control

4. Click "Next" and then "Finish"

!!! note
    When your project first loads, you'll see some default files like "HelloApplication.java" and "HelloController.java". These are generated examples that can be helpful for reference, but for our tutorial, we'll be creating our own files from scratch.

## Exploring Your Project Structure
<!-- exploring project structure  -->
![Image Title](https://dummyimage.com/600x400/eee/aaa"ImageTitle"){: .center-image}

Let's take a moment to understand the project layout:

1. Navigate to the `src` folder
   - This is the root of your source code

2. Expand the `java` folder
   - This is where all your Java classes will live

3. Look for the folder starting with "com."
   - This is your primary package folder
   - In JavaFX projects, this typically follows the format `com.yourcompanyname.projectname`

## Creating Your Main Application Class
<!-- creating main application -->
![Image Title](https://dummyimage.com/600x400/eee/aaa"ImageTitle"){: .center-image}

1. Navigate to the `src/main/java folder` in your project structure.
2. Create a new Java class (e.g., `Main.java`) in your package (e.g., `com.example`).
3. Paste the following code into your class:

    ```java title="Main.java" linenums="1"
    package com.javafxtutorial.javafxtutorial;

    import javafx.application.Application;
    import javafx.stage.Stage;

    public class MainMenu extends Application {
        // This is where the magic begins!
        @Override
        public void start(Stage stage) throws Exception {
            // We'll add our scene setup here in just a moment
        }

        // The entry point of our application
        public static void main(String[] args) {
            // This method launches our JavaFX application
            launch(args);
        }
    }
    ```
#### Understanding the Application Structure
- `Application` is the base class for JavaFX applications
- `start()` method is called when the application launches
- `main()` method is the entry point that calls `launch()`

## Building Your First Scene
<!-- building your first scene -->
Scenes in JavaFX are like canvases where you'll draw your user interface. Let's create a basic scene:

   ```java title="MainMenu.java" linenums="1"
    package com.javafxtutorial.javafxtutorial;

    import javafx.application.Application;
    import javafx.scene.Group;
    import javafx.scene.Scene;
    import javafx.stage.Stage;

    public class MainMenu extends Application {
        // Define our window dimensions
        private static final int WIDTH = 600;
        private static final int HEIGHT = 500;

        @Override
        public void start(final Stage stage) throws Exception {
            // Create a root group to hold our UI elements
            Group root = new Group();
            
            // Create our scene with the root group
            Scene scene = new Scene(root, WIDTH, HEIGHT);
            
            // Configure the stage (window)
            stage.setScene(scene);
            stage.setTitle("My First JavaFX Application");
            
            // Show the window
            stage.show();
        }

        public static void main(String[] args) {
            launch(args);
        }
    }
   ```

## Adding Interactive Elements
<!-- Adding Interactive Elements -->
Let's make our scene more interesting by adding some UI components:

   ```java title="MainMenu.java" linenums="1"
    import javafx.application.Application;
    import javafx.scene.Group;
    import javafx.scene.Scene;
    import javafx.scene.control.Button;
    import javafx.scene.layout.VBox;
    import javafx.scene.text.Text;
    import javafx.stage.Stage;

    public class MainMenu extends Application {
        private static final int WIDTH = 600;
        private static final int HEIGHT = 500;

        @Override
        public void start(final Stage stage) throws Exception {
            // Create our scene using a method to set up elements
            Scene scene = new Scene(makeSceneGroup(), WIDTH, HEIGHT);
            stage.setScene(scene);
            stage.setTitle("JavaFX Tutorial");
            stage.show();
        }

        // Method to create and organize our scene elements
        private Group makeSceneGroup() {
            Group sceneGroup = new Group();
            
            // Create a title text
            Text text = new Text("Welcome to JavaFX!");
            
            // Create buttons
            Button startButton = new Button("Start");
            Button exitButton = new Button("Exit");
            
            // Use VBox to arrange elements vertically
            VBox vbox = new VBox(20); // 20 pixels spacing between elements
            vbox.getChildren().addAll(text, startButton, exitButton);
            
            // Add the VBox to our scene group
            sceneGroup.getChildren().add(vbox);
            
            return sceneGroup;
        }

        public static void main(String[] args) {
            launch(args);
        }
    }
   ```

## Introduction to FXML: Separating Design from Logic
<!-- Adding Interactive Elements -->
FXML allows you to design your user interface separately from your Java code:

### Creating an FXML File
Create a new file called `MainMenu.fxml` in your resources folder:

   ```xml title="MainMenu.xml"
   <?xml version="1.0" encoding="UTF-8"?>
    <?import javafx.scene.layout.VBox?>
    <?import javafx.scene.text.Text?>
    <?import javafx.scene.control.Button?>
    <VBox xmlns:fx="http://javafx.com/fxml"
        fx:controller="com.javafxtutorial.javafxtutorial.MenuController">
        <Text>JavaFX Tutorial</Text>
        <Button text="Start"/>
        <Button text="Exit"/>
    </VBox>
   ```

### Loading FXML in Your Application
Create a new file called `MainMenu.fxml` in your resources folder:

   ```java title="MainMenu.java"
    @Override
    public void start(final Stage stage) throws Exception {
        FXMLLoader menuFXML = new FXMLLoader(getClass().getResource("MainMenu.fxml"));
        Scene scene = new Scene(menuFXML.load(), WIDTH, HEIGHT);
        stage.setScene(scene);
        stage.setTitle("JavaFX Tutorial");
        stage.show();
    }
   ```

## Conclusion
<!-- end product is a simple title screen with a start button, exit button and title. -->
Congratulations! You've just taken your first steps into the world of JavaFX application development. We've covered:

- Setting up a JavaFX project in IntelliJ IDEA
- Creating a basic application structure
- Building scenes with interactive elements
- Introducing FXML for UI design
- Remember, every great application starts with a simple first step. You've just taken that step! 🚀

Keep experimenting, have fun, and don't be afraid to try new things. Happy coding!