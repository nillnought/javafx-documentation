# Handling Player Interactions
<!-- overview -->
## Overview
This section will introduce handling player interactions like clicking a button, changing game scenes, player movement, and mouse interactions as we add functionality to our menu and game scene.
## Button Interactions
<!-- Handling key presses and clicks -->
1. Create a new class in our `com.` folder called "MenuController"

![Image Title](assets\PlayerInteractionsImages\newFile.png"ImageTitle"){: .center-image}
2. Set the FXML file controller to `MenuContoller`
```xml title="mainMenu.fxml" linenums="1" hl_lines="7"
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
3. Assign ID to text element

In order for us to change elements in our FXML file, we need to give the element an ID. We will be changing our text element, so let's give it an ID.
```xml title="mainMenu.fxml" linenums="1" hl_lines="8"
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
4. Create method to change text contents

Now we can go to our `MenuController.java` class and add a method to change our text:
```java title="MenuController.java" linenums="1" hl_lines="4-5 9-16"
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
!!! warning
    The @FXML tag is required for any method that modifies an element in our FXML file.
5. Assign `onAction` for start button

Lastly, let's go back to our FXML file and tell our start button to use this method when we click it:
```xml title="mainMenu.fxml" linenums="1" hl_lines="9"
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

## Loading A New Scene
Just having our text change when we click start is a bit boring, so let's change our method to load a new scene.

1. Use start button to load an empty scene

First let's give our start button an ID:
```xml title="mainMenu.fxml" linenums="1" hl_lines="9"
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
```java title="MenuController.java" linenums="1" hl_lines="5-7 11-12 17 21-24"
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
!!! note
    We gave our button an ID so that we could use it to get the scene it is in.

Now when we start our application and click the start button we should get an empty scene.
![Image Title](assets\PlayerInteractionsImages\empty scene.png"ImageTitle"){: .center-image}

2. Replace empty scene with FXML scene

Now let's create a FXML file for our game scene:
![Image Title](assets\PlayerInteractionsImages\creategamescene.png"ImageTitle"){: .center-image}
And let's modify our method to load this scene instead:
```java title="MenuController.java" linenums="1" hl_lines="5-6 21 25-27"
package com.javafxtutorial.javafxtutorial;


import javafx.fxml.FXML;
import javafx.fxml.FXMLLoader;
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

3. Add exit functionality to exit button

Lastly, lets add a method for our exit button:
```java title="MenuController.java" linenums="1" hl_lines="29-32"
package com.javafxtutorial.javafxtutorial;


import javafx.fxml.FXML;
import javafx.fxml.FXMLLoader;
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
   @FXML
   protected void onExitButtonClick() {
       System.exit(0);
   }
}
```
Make sure to tell our exit button to use the method as well:

```xml title="mainMenu.fxml" linenums="1" hl_lines="10"
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
Now that our menu is set up, let's work on our game scene.
<!-- How to set up collisions and handle them for events -->
1. Create a class called Game.

![Image Title](assets\PlayerInteractionsImages\game.png"ImageTitle"){: .center-image}
This is where we will handle our interaction and game logic.

Before we start with player movement, let's set up our `game.fxml` scene.
```xml title="game.fxml" linenums="1" hl_lines="2-13"
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

2. Handle translating the player

To move our player we need to translate their X and Y positions when the player presses a key.

Let's set up 3 methods in our game class to help do this:
```java title="Game.java" linenums="1" hl_lines="4-6 12-13 16-17 22-33 36-38 41-43"
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
Our two methods `setVelX` and `setVelY` are where we set the player's X and Y velocity, while our `movementLoop` method handles translating the player using that velocity.

3. Starting our movement loop

Before we can handle any keyboard inputs we need to start our `movementLoop`. To do this let's make some changes to our `MenuController` class.

```java title="MenuController.java" linenums="1" hl_lines="17 21-37"
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

    private static final int SPEED = 5;

    @FXML
    protected void onStartButtonClick() throws IOException {
        FXMLLoader gameFXML = new FXMLLoader(getClass().getResource("game.fxml"));

        Group gameRoot = gameFXML.load();

        Scene currentScene = startButton.getScene();

        currentScene.setRoot(gameRoot);

        Game gameController = gameFXML.getController();
        gameController.movementLoop();


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
To start, we've broken up our single line we used to change our Scene root into 4 lines.

Doing this allows us to use our `game.fxml` file separately, which we can use to access our `Game` class using this line: `Game gameController = gameFXML.getController();`
This allows us to start our `movementLoop` method we defined earlier.

Lastly, we request focus for our game window so that any keyboard inputs will be correctly recieved by our game.

4. Handling keyboard inputs

Now that we've started our movement loop, we need to recieve keyboard input from the player so that we know when to change their position.
To do this we will use `setOnKeyPressed` and `setOnKeyReleased` to ensure smooth movement.
``` java title="MenuController.java" linenums="1" hl_lines="9 43-70"
    package com.javafxtutorial.javafxtutorial;


import javafx.fxml.FXML;
import javafx.fxml.FXMLLoader;
import javafx.scene.Group;
import javafx.scene.Scene;
import javafx.scene.control.Button;
import javafx.scene.input.KeyCode;


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
//        Group root = new Group();
//        return root;
       return new FXMLLoader(getClass().getResource("game.fxml"));
   }
   @FXML
   protected void onExitButtonClick() {
       System.exit(0);
   }
}
```
Now when you run the application and press start you will be able to use the WASD keys to move the blue square around.
![Image Title](assets\PlayerInteractionsImages\movementfinal.gif"ImageTitle"){: .center-image}

## Mouse Interactions
The last type of player interaction we will handle is mouse interactions. For this we will use the orange rectangle we added to our scene previously.

1. Assign an ID to the orange rectangle in `Game.fxml`

```xml title="Game.fxml" linenums="1" hl_lines="9"
<?xml version="1.0" encoding="UTF-8"?>


<?import javafx.scene.Group?>
<?import javafx.scene.shape.Rectangle?>
<Group xmlns="http://javafx.com/javafx"
      xmlns:fx="http://javafx.com/fxml"
      fx:controller="com.javafxtutorial.javafxtutorial.Game">
   <Rectangle height="100" width="100" fill="orange" fx:id="orangeRectangle"/>
   <Rectangle height="50" width="50" fill="blueviolet" fx:id="player"/>


</Group>
```
2. Create methods for mouse interactions

We will be handling 3 different interactions with our orange rectangle in `Game.java`. Create 3 methods for this: mouseEnter, mouseExit, and click.
```java title="Game.java" linenums="1" hl_lines="15-33"
package com.javafxtutorial.javafxtutorial;


import javafx.animation.AnimationTimer;
import javafx.fxml.FXML;
import javafx.scene.shape.Rectangle;

public class Game {


private double velX;
private double velY;


 @FXML
 private Rectangle orangeRectangle;

@FXML
public void mouseEnter() {
   orangeRectangle.setOpacity(0.5);
}


@FXML
public void mouseExit() {
   orangeRectangle.setOpacity(1);
}


@FXML
public void click() {
   orangeRectangle.setFill(Color.RED);
}
```
3. Assign methods to the orange rectangle
Lastly, we need to tell our rectangle to use these methods when we want it to.
```xml title="game.fxml" linenums="1" hl_lines="9-10"
<?xml version="1.0" encoding="UTF-8"?>


<?import javafx.scene.Group?>
<?import javafx.scene.shape.Rectangle?>
<Group xmlns="http://javafx.com/javafx"
      xmlns:fx="http://javafx.com/fxml"
      fx:controller="com.javafxtutorial.javafxtutorial.Game">
   <Rectangle height="100" width="100" fill="orange" fx:id="orangeRectangle"
              onMouseClicked="#click" onMouseEntered="#mouseEnter" onMouseExited="#mouseExit"/>
   <Rectangle height="50" width="50" fill="blueviolet" fx:id="player"/>


</Group>
```
!!! success
    Now when you run the application you should be able to hover over and click the orange rectangle to see the results.

![Image Title](assets\PlayerInteractionsImages\finalinteractions.gif"ImageTitle"){: .center-image}

## Conclusion
Well Done! You've learned how to handle different types of player interactions. We covered:

- Adding functionality to buttons
- Changing scenes
- Handling keyboard input
- Simple mouse interactions

Now it's time to move on to the last step, making this game your own with some customization!