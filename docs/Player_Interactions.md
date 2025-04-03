# Handling Player Interactions
<!-- overview -->
## Overview
This section will focus on handling player interactions like inputs for movement and collisions between the player and another entity.
## Player Movement
<!-- Handling key presses and clicks -->
Create a new class in our `com.` folder called "MenuController"
![Image Title](assets\PlayerInteractionsImages\newFile.png"ImageTitle"){: .center-image}
Now, we need to tell our FXML file to use our controller.
```xml title="mainMenu.fxml" linenums="1"
    <?xml version="1.0" encoding="UTF-8"?>


<?import javafx.scene.layout.VBox?>
<?import javafx.scene.text.Text?>
<?import javafx.scene.control.Button?>
<VBox xmlns:fx="http://javafx.com/fxml" fx:controller="com.javafxtutorial.javafxtutorial.MenuController">
   <Text>JavaFX Tutorial</Text>
   <Button>Start</Button>
   <Button>Exit</Button>
</VBox>
```
In order for us to change elements in our FXML file, we need to give the element an ID.
```xml title="mainMenu.fxml" linenums="1"
<?xml version="1.0" encoding="UTF-8"?>


<?import javafx.scene.layout.VBox?>
<?import javafx.scene.text.Text?>
<?import javafx.scene.control.Button?>
<VBox xmlns:fx="http://javafx.com/fxml" fx:controller="com.javafxtutorial.javafxtutorial.MenuController">
   <Text fx:id="tutorialText">JavaFX Tutorial</Text>
   <Button>Start</Button>
   <Button>Exit</Button>
</VBox>

```

Now we can go to our `MenuController.java` class and add a method to change our text:
```java title="MenuController.fxml" linenums="1"
package com.javafxtutorial.javafxtutorial;


import javafx.fxml.FXML;
import javafx.scene.text.Text;


public class MenuController {
   @FXML
   private Text tutorialText;


   @FXML
   protected void onStartButtonClick() {
       tutorialText.setText("The text changed!");
   }
}

```
Lastly, let's go back to our FXML file and tell our start button to use this method when we click it:
```xml title="mainMenu.fxml" linenums="1"
<?xml version="1.0" encoding="UTF-8"?>


<?import javafx.scene.layout.VBox?>
<?import javafx.scene.text.Text?>
<?import javafx.scene.control.Button?>
<VBox xmlns:fx="http://javafx.com/fxml" fx:controller="com.javafxtutorial.javafxtutorial.MenuController">
   <Text fx:id="tutorialText">JavaFX Tutorial</Text>
   <Button onAction="#onStartButtonClick">Start</Button>
   <Button>Exit</Button>
</VBox>

```
Now run the application and click the start button, you should end up seeing this:
![Image Title](assets\PlayerInteractionsImages\changedtext.png"ImageTitle"){: .center-image}

Just having our text change when we click start is a bit boring, so let's change our method to load a new scene.
First let's give our start button an ID:
```xml title="mainMenu.fxml" linenums="1"
<?xml version="1.0" encoding="UTF-8"?>


<?import javafx.scene.layout.VBox?>
<?import javafx.scene.text.Text?>
<?import javafx.scene.control.Button?>
<VBox xmlns:fx="http://javafx.com/fxml" fx:controller="com.javafxtutorial.javafxtutorial.MenuController">
   <Text fx:id="tutorialText">JavaFX Tutorial</Text>
   <Button onAction="#onStartButtonClick" fx:id="startButton">Start</Button>
   <Button>Exit</Button>
</VBox>
```
Now we will change our method so that it uses the button to change the root of our scene to a empty group:
```java title="MenuController.fxml" linenums="1"
package com.javafxtutorial.javafxtutorial;


import javafx.fxml.FXML;
import javafx.scene.Group;
import javafx.scene.Scene;
import javafx.scene.control.Button;


public class MenuController {
   @FXML
   private Button startButton;


   @FXML
   protected void onStartButtonClick() {
       startButton.getScene().setRoot(gameScreen());
   }


   private Group gameScreen() {
       Group root = new Group();
       return root;
   }
}
```
Now when we start our application and click the start button we should get an empty scene.
Great! Now let's create a FXML file for our game scene:
![Image Title](assets\PlayerInteractionsImages\creategamescene.png"ImageTitle"){: .center-image}
And let's modify our method to load this scene instead:
```java title="MenuController.fxml" linenums="1"
package com.javafxtutorial.javafxtutorial;


import javafx.fxml.FXML;
import javafx.fxml.FXMLLoader;
import javafx.scene.Group;
import javafx.scene.Scene;
import javafx.scene.control.Button;

import java.io.IOException;


public class MenuController {


   @FXML
   private Button startButton;

   @FXML
   protected void onStartButtonClick() throws IOException {
       startButton.getScene().setRoot(gameScreen().load());
   }


   private FXMLLoader gameScreen() {
       return new FXMLLoader(getClass().getResource("game.fxml"));
   }
}
```
!!! warning
    Before running the application be sure to remove this line from game.fxml, or else the application will not run.
    `fx:controller="com.javafxtutorial.javafxtutorial.Game"`

Lastly, lets add a method for our exit button:
```java title="MenuController.fxml" linenums="1"
package com.javafxtutorial.javafxtutorial;


import javafx.fxml.FXML;
import javafx.fxml.FXMLLoader;
import javafx.scene.Group;
import javafx.scene.Scene;
import javafx.scene.control.Button;
import javafx.scene.text.Text;


import java.io.IOException;


public class MenuController {


   @FXML
   private Button startButton;


   @FXML
   protected void onStartButtonClick() throws IOException {
       startButton.getScene().setRoot(gameScreen().load());
   }


   private FXMLLoader gameScreen() {
       return new FXMLLoader(getClass().getResource("game.fxml"));
   }
   @FXML
   protected void onExitButtonClick() {
       System.exit(0);
   }
}
```
Make sure to tell our exit button to use the method as well:
```xml title="mainMenu.fxml" linenums="1"
<?xml version="1.0" encoding="UTF-8"?>


<?import javafx.scene.layout.VBox?>
<?import javafx.scene.text.Text?>
<?import javafx.scene.control.Button?>
<VBox xmlns:fx="http://javafx.com/fxml" fx:controller="com.javafxtutorial.javafxtutorial.MenuController">
   <Text fx:id="tutorialText">JavaFX Tutorial</Text>
   <Button onAction="#onStartButtonClick" fx:id="startButton">Start</Button>
   <Button onAction="#onExitButtonClick">Exit</Button>
</VBox>
```
## Player Movement
<!-- How to set up collisions and handle them for events -->
Create a class called Game.
![Image Title](assets\PlayerInteractionsImages\game.png"ImageTitle"){: .center-image}
This is where we will handle our interaction and game logic.
Before we start with player movement, let's set up our `game.fxml` scene.
```xml title="game.fxml" linenums="1"
<?xml version="1.0" encoding="UTF-8"?>


<?import javafx.scene.Group?>
<?import javafx.scene.shape.Rectangle?>
<Group xmlns="http://javafx.com/javafx"
      xmlns:fx="http://javafx.com/fxml"
      fx:controller="com.javafxtutorial.javafxtutorial.Game">
   <Rectangle height="100" width="100" fill="orange"/>
   <Rectangle height="50" width="50" fill="blueviolet" fx:id="player"/>


</Group>
```
For now, our player will be represented by a blue rectangle with the id "player".
To move our player we need to translate their X and Y positions when the player presses a key.
Let's set up 3 methods in our game class to help do this:
```java title="Game.java" linenums="1"
package com.javafxtutorial.javafxtutorial;


import javafx.animation.AnimationTimer;
import javafx.fxml.FXML;
import javafx.scene.shape.Rectangle;


public class Game {


   private double velX;
   private double velY;


   @FXML
   private Rectangle player;




   @FXML
   public void movementLoop() {
       new AnimationTimer() {
           @Override
           public void handle(long now) {
               player.setTranslateX(player.getTranslateX() + velX);
               player.setTranslateY(player.getTranslateY() + velY);
           }
       }.start();


   }


   public void setVelX(double velX) {
       this.velX = velX;
   }


   public void setVelY(double velY) {
       this.velY = velY;
   }
}
```
Lastly, we need to make a change to our `MenuController.java` class:
```java title="MenuController.java" linenums="1"
package com.javafxtutorial.javafxtutorial;


import javafx.fxml.FXML;
import javafx.fxml.FXMLLoader;
import javafx.scene.Group;
import javafx.scene.Scene;
import javafx.scene.control.Button;
import javafx.scene.input.KeyCode;
import javafx.scene.text.Text;


import java.io.IOException;


public class MenuController {


   @FXML
   private Button startButton;


   private static final int SPEED = 5;


   @FXML
   protected void onStartButtonClick() throws IOException {
       FXMLLoader gameFXML = new FXMLLoader(getClass().getResource("game.fxml"));


       Group gameRoot = gameFXML.load();


       Scene currentScene = startButton.getScene();


       currentScene.setRoot(gameRoot);


       Game gameController = gameFXML.getController();
       gameController.movementLoop();


       gameRoot.setOnKeyPressed(event -> {
           if (event.getCode() == KeyCode.W) {
               gameController.setVelY(-SPEED);
           }
           if (event.getCode() == KeyCode.S) {
               gameController.setVelY(SPEED);
           }
           if (event.getCode() == KeyCode.A) {
               gameController.setVelX(-SPEED);
           }
           if (event.getCode() == KeyCode.D) {
               gameController.setVelX(SPEED);
           }
       });
       gameRoot.setOnKeyReleased(event -> {
           if (event.getCode() == KeyCode.W) {
               gameController.setVelY(0);
           }
           if (event.getCode() == KeyCode.S) {
               gameController.setVelY(0);
           }
           if (event.getCode() == KeyCode.A) {
               gameController.setVelX(0);
           }
           if (event.getCode() == KeyCode.D) {
               gameController.setVelX(0);
           }
       });


       gameRoot.requestFocus();
   }


   private FXMLLoader gameScreen() {
       return new FXMLLoader(getClass().getResource("game.fxml"));
   }
   @FXML
   protected void onExitButtonClick() {
       System.exit(0);
   }
}

```
## Conclusion
Well Done! You've learned how to handle different types of player interactions. We covered:

- Adding functionality to buttons
- Changing scenes
- Handling keyboard input

Now it's time to move on to the last step, making this game your own!