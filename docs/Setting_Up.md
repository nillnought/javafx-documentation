# Setting Up Your JavaFX Project
<!-- overview -->
## Overview
Welcome to your JavaFX adventure! If you're new to desktop application development or just getting started with JavaFX, don't worry - we've got you covered. This comprehensive guide will walk you through every step of creating your first JavaFX project, from setting up your development environment to creating your first interactive scene.

## Getting Started: Preparing Your Development Environment

### Enabling the JavaFX Plugin
Let's kick things off by making sure you have the JavaFX plugin installed and ready to go:

1. Open IntelliJ IDEA and navigate to the Plugins section
   - Click on the "Plugins" tab on the left side of the window
![Plugins Tab](assets\SettingUpImages\pluginsfull.png"ImageTitle"){: .center-image}

2. In the search bar, type "JavaFX"
   - Look for the official JavaFX plugin
   - If it's not installed, click "Install" 
   - If it's already installed, make sure it's enabled by checking the box next to the plugin

![Image Title](assets\SettingUpImages\PluginEnabled.png"ImageTitle"){: .center-image}

!!! tip
    The JavaFX plugin provides additional support and tools that make developing JavaFX applications much smoother. It includes helpful code completion, scene builder integration, and other useful features.

### Creating Your First JavaFX Project
<!-- creating the project in intelliJ -->
Now that the plugin is ready, let's create your project:

1. Navigate back to the projects screen
![Image Title](assets\SettingUpImages\projectsfull.png"ImageTitle"){: .center-image}

2. Click on "New Project" from the IntelliJ IDEA welcome screen
![Image Title](assets\SettingUpImages\new project.png"ImageTitle"){: .center-image}


3. On the left side, select "JavaFX" from the project types
!!! note
    If you don't see JavaFX immediately, make sure you've installed the plugin correctly
![Image Title](assets\SettingUpImages\newprojectjavaFX.png"ImageTitle"){: .center-image}

4. Project Configuration:
    - Choose a meaningful name for your project (e.g., "JavaFXTutorial")
    - Select a location to save your project
    - (Optional but recommended) Check the "Create Git repository" box if you want version control
![Image Title](assets\SettingUpImages\newprojectsetup.png"ImageTitle"){: .center-image}

Once you're finished, click "Next"

5. Additional Libraries

You will be prompted to select additional libraries once you press next. For this guide we will not be using any additional libraries, so you may ignore this prompt and move ahead to creating your project.
![Image Title](assets\SettingUpImages\libraries.png"ImageTitle"){: .center-image}
6. Create your project


## Exploring Your Project Structure
<!-- exploring project structure  -->
!!! note
    When your project first loads, you'll see some default files like "HelloApplication.java" and "HelloController.java". These are generated examples that can be helpful for reference, but for our tutorial, we'll be creating our own files from scratch.

Let's take a moment to understand the project layout:

1. Navigate to the `src` folder
   - This is the root of your source code

2. Expand the `java` folder
   - This is where all your Java classes will live

3. Look for the folder starting with "com."
   - This is your primary package folder
   - In JavaFX projects, this typically follows the format `com.yourcompanyname.projectname`
![Image Title](assets\SettingUpImages\navigatetofolder.png"ImageTitle"){: .center-image}

## Creating Your Main Application Class
<!-- creating main application -->

1. Navigate to the `src/main/java folder` in your project structure.
2. Create a new Java class (e.g., `Main.java`) in your package (e.g., `com.example`).
![Image Title](assets\SettingUpImages\createfile.png"ImageTitle"){: .center-image}
3. Name your new class MainMenu

![Image Title](assets\SettingUpImages\namefile.png"ImageTitle"){: .center-image}
4. Make your class extend Application:

```java title="MainMenu.java" linenums="1"
    package com.javafxtutorial.javafxtutorial;




    import javafx.application.Application;


    public class MainMenu extends Application {


    }
```
When we extend application we must provide an implementation of its start method.
5. Override the start method:

```java title="MainMenu.java" linenums="1"
    package com.javafxtutorial.javafxtutorial;




import javafx.application.Application;
import javafx.stage.Stage;


public class MainMenu extends Application {
  
   @Override
   public void start(Stage stage) throws Exception {
      
    }

    public static void main(String[] args) {
        launch(args);
    }
}
```
!!! note
    launch(args) is a method of application, which handles all the logic for launching our application.
#### Understanding the Application Structure
- `Application` is the base class for JavaFX applications
- `start()` method is called when the application launches
- `main()` method is the entry point that calls `launch()`

## Building Your First Scene
<!-- building your first scene -->
Scenes in JavaFX are like canvases where you'll draw your user interface. Creating a scene is as simple as this:
```java title="MainMenu.java" linenums="1"
package com.javafxtutorial.javafxtutorial;


import javafx.application.Application;
import javafx.scene.Scene;
import javafx.stage.Stage;


public class MainMenu extends Application {


   @Override
   public void start(Stage stage) throws Exception {
       Scene scene = new Scene();
   }
}

```
Well... not quite. We need to pass a parent node as a parameter to our scene when we create it.
!!! note
    JavaFX has a certain structure that we need to make sure we follow:
    Stage -> Scene -> Parent
Now when you run the application you should get a window like this:
![Image Title](assets\SettingUpImages\newscene.png"ImageTitle"){: .center-image}

The window is a bit too big and is lacking a name so let's change that:
```java title="MainMenu.java" linenums="1"
package com.javafxtutorial.javafxtutorial;




import javafx.application.Application;
import javafx.scene.Group;
import javafx.scene.Scene;
import javafx.stage.Stage;


public class MainMenu extends Application {
    //define constants for window dimensions
   private static final int WIDTH = 600;
   private static final int HEIGHT = 500;


   @Override
   public void start(final Stage stage) throws Exception {
       Group root = new Group();
       Scene scene = new Scene(root, WIDTH, HEIGHT);
       stage.setScene(scene);
       //assign a title to the window
       stage.setTitle("JavaFX Tutorial");
       stage.show();
   }
}
```
## Adding Elements
<!-- Adding Interactive Elements -->
Now that we have our scene set up let's start adding elements to it.
There's two ways we can add elements to our scene:
1. Manually inserting elements
2. By using FXML files
To start we will add elements manually, then go over how we can translate the elements we added into a single FXML file.

### Manually Inserting Elements
Adding elements manually takes a decent amount of space, so lets create a helper method called `makeSceneGroup` for this.
Our helper method will return a group, which we will use for our scene's parent.
```java title="MainMenu.java" linenums="1"
    package com.javafxtutorial.javafxtutorial;




import javafx.application.Application;
import javafx.scene.Group;
import javafx.scene.Scene;
import javafx.stage.Stage;


public class MainMenu extends Application {
   private static final int WIDTH = 600;
   private static final int HEIGHT = 500;


   @Override
   public void start(final Stage stage) throws Exception {
       Group root = new Group();
       Scene scene = new Scene(root, WIDTH, HEIGHT);
       stage.setScene(scene);
       stage.setTitle("JavaFX Tutorial");
       stage.show();
   }


   private Group makeSceneGroup() {
       Group sceneGroup = new Group();
      
   }
}

```
Now that we have our scene set up, let's start by adding some basic shapes.
We can create a rectangle by using this line of code:
```java
Rectangle rectangle = new Rectangle(80, 80);
```
!!! note
    When we create a rectangle, we need to pass the width and height to its constructor.

We can also assign our rectangle a colour by passing `Color.RED`, where `RED` can be replaced with the colour we want.
Let's add our rectangle to our group and return the group to finish our method.
``` java title="makeSceneGroup method" linenums="27"
private Group makeSceneGroup() {
    Group sceneGroup  = new Group();
    Rectangle rectangle = new Rectangle(80, 80, Color.RED);
    sceneGroup.getChildren().add(rectangle);
    return sceneGroup;
}
```
Now when you run our application you should see a red rectangle on screen.
![Image Title](assets\SettingUpImages\red.png"ImageTitle"){: .center-image}

Let's remove the rectangle and add some other elements to make our menu.
``` java title="MainMenu.java" linenums="1"
package com.javafxtutorial.javafxtutorial;


import javafx.application.Application;
import javafx.scene.Group;
import javafx.scene.Scene;
import javafx.scene.control.Button;
import javafx.scene.layout.VBox;
import javafx.scene.paint.Color;
import javafx.scene.shape.Rectangle;
import javafx.scene.text.Text;
import javafx.stage.Stage;


public class MainMenu extends Application {
   private static final int WIDTH = 600;
   private static final int HEIGHT = 500;


   @Override
   public void start(final Stage stage) throws Exception {
       Scene scene = new Scene(makeSceneGroup(), WIDTH, HEIGHT);
       stage.setScene(scene);
       stage.setTitle("JavaFX Tutorial");
       stage.show();
   }


   private Group makeSceneGroup() {
       Group sceneGroup = new Group();
       Text text = new Text("JavaFX Tutorial");
       Button Startbutton = new Button("Start");
       Button Exitbutton = new Button("Exit");
       VBox vbox = new VBox(20, text, Startbutton, Exitbutton);
       sceneGroup.getChildren().add(vbox);
       return sceneGroup;
   }
}
```
We added a couple of elements: Text, Buttons, and something called a VBox.
!!! note
    VBox stands for vertical box, it stores node elements vertically.
    VBox has a horizontal counterpart called HBox.
When we run our application we should get something that looks like this.
![Image Title](assets\SettingUpImages\basemenu.png"ImageTitle"){: .center-image}
??? note "    If we don't use a VBox to contain our elements, it would look like this:"
    ![Image Title](assets\SettingUpImages\novbox.png"ImageTitle"){: .center-image}
Here we used a few simple elements of JavaFX. For a deeper look into the types of elements JavaFx offers, take a look [here](https://jenkov.com/tutorials/javafx/overview.html).
## Introduction to FXML: Separating Design from Logic
<!-- Adding Interactive Elements -->
FXML allows you to design your user interface separately from your Java code. Let's take a look at how we can convert our menu into a FXML file.
For a more detailed look into FXML check out the [Oracle Documentation](https://openjfx.io/javadoc/24/javafx.fxml/javafx/fxml/doc-files/introduction_to_fxml.html) on it.

### Creating an FXML File
Create a new file called `MainMenu.fxml` in your resources folder:
![Image Title](assets\SettingUpImages\fxmlfilelocation.png"ImageTitle"){: .center-image}

To recreate our scene in our FXML file, insert this code:
```xml title="MainMenu.xml" linenums="1"
<?xml version="1.0" encoding="UTF-8"?>


<?import javafx.scene.layout.VBox?>
<?import javafx.scene.text.Text?>
<?import javafx.scene.control.Button?>
<VBox>
   <Text>JavaFX Tutorial</Text>
   <Button>Start</Button>
   <Button>Exit</Button>
</VBox>

```

### Loading FXML in Your Application
Now to use our FXML file we need to load it in our start method.

   ```java title="MainMenu.java" linenums="1"
    @Override
    public void start(final Stage stage) throws Exception {
        FXMLLoader menuFXML = new FXMLLoader(getClass().getResource("MainMenu.fxml"));
        Scene scene = new Scene(menuFXML.load(), WIDTH, HEIGHT);
        stage.setScene(scene);
        stage.setTitle("JavaFX Tutorial");
        stage.show();
    }
   ```

!!! success
    The final result should look like this:
![Image Title](assets\SettingUpImages\setupFinal.png"ImageTitle"){: .center-image}
## Conclusion
<!-- end product is a simple title screen with a start button, exit button and title. -->
Congratulations! You've just taken your first steps into the world of JavaFX application development. We've covered:

- Setting up a JavaFX project in IntelliJ IDEA
- Creating a basic application structure
- Building scenes with interactive elements
- Introducing FXML for UI design
- Remember, every great application starts with a simple first step. You've just taken that step! 🚀

Keep experimenting, have fun, and don't be afraid to try new things. Happy coding!