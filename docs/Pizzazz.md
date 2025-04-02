# Personalizing and Adding Pizzazz to Your Project
<!-- overview -->
## Overview
This section will guide you through adding style and visual elements to your JavaFX project, including custom images, fonts, sprites, and animations. By the end, you’ll have a visually polished game with a moving character and optional background movement.

Adding visual flair to your project can make your game more engaging and unique. In this section, we’ll cover:
- Setting up a **stylesheet** to style your project.
- Adding custom **images** to your game.
- Using **sprites** to animate your character and other elements.

## Setting Up a "Stylesheet" <!--not sure if its called a stylesheet-->
<!-- show how to setup their style sheet, how to add classes to shapes and stuff so they can make changes to it in the style sheet -->
![Image Title](https://dummyimage.com/600x400/eee/aaa"ImageTitle"){: .center-image}

A stylesheet allows you to centralize your visual styles and apply them to your JavaFX elements, just like CSS in web development. Here’s how to set one up:

### Step 1: Create a CSS File
1. In your project, navigate to the `src/main/resources` folder (or create it if it doesn’t exist).
2. Inside this folder, create a new file called `styles.css`.

### Step 2: Define Styles in the CSS File
Add styles to your `styles.css` file. For example, to style buttons and text:

    ```css title="styles.css"
    .button {
        -fx-background-color: #4CAF50; /* Green background */
        -fx-text-fill: white; /* White text */
        -fx-font-size: 16px; /* Font size */
        -fx-padding: 10px 20px; /* Padding */
        -fx-border-radius: 5px; /* Rounded corners */
    }

    .title-text {
        -fx-font-family: "Arial";
        -fx-font-weight: bold;
        -fx-font-size: 24px;
        -fx-fill: #333333; /* Dark gray text */
    }
    ```
### Step 3: Apply the Stylesheet
1. In your Main.java file, load the stylesheet into your scene:

    ```java title="Main.java"
    Scene scene = new Scene(layout, 400, 300);
    scene.getStylesheets().add(getClass().getResource("/styles.css").toExternalForm());
    ```

2. Assign style classes to your elements in Java:

    ```java title="Main.java"
    title.getStyleClass().add("title-text");
    startButton.getStyleClass().add("button");
    exitButton.getStyleClass().add("button");
    ```

!!! success
Now your buttons and title text will use the styles defined in your `styles.css` file. You can easily update the look of your game by editing this file.

## Adding Images
<!-- how to add images, set backgrounds, maybe make a moving background(? not sure if we want to do that or not [moving bgs might go into the sprites section since its pretty similar]) -->

### Step 1: Import an Image
1. Place your image file (e.g., `background.png`) in the `src/main/resource`s folder.
2. Load the image in your `Main.java` file using the Image and ImageView classes:

    ```java title="Main.java"
    Image backgroundImage = new Image(getClass().getResource("/background.png").toExternalForm());
    ImageView backgroundView = new ImageView(backgroundImage);
    backgroundView.setFitWidth(400); // Match the scene width
    backgroundView.setFitHeight(300); // Match the scene height
    ```

### Step 2: Add the Image to the Layout
1. Use a StackPane to layer the background image behind other elements:

    ```java title="Main.java"
    StackPane stackPane = new StackPane();
    stackPane.getChildren().addAll(backgroundView, layout); // Add background first, then layout
    Scene scene = new Scene(stackPane, 400, 300);
    ```

!!! note
This approach ensures that your background image stays behind all other elements.

## Using Sprites
<!-- how to do sprites and animate them, plus maybe moving backgrounds -->
Sprites are images or objects that can be animated. Here’s how to add and animate a sprite:

### Step 1: Create a Sprite
1. Add a sprite image (e.g., `character.png`) to the `src/main/resources` folder.
2. Load the sprite like you did with the background image:

    ```java title="Main.java"
    Image characterImage = new Image(getClass().getResource("/character.png").toExternalForm());
    ImageView characterSprite = new ImageView(characterImage);
    characterSprite.setFitWidth(50); // Set sprite width
    characterSprite.setFitHeight(50); // Set sprite height
    ```

### Step 2: Animate the Sprite
1. Use a `TranslateTransition` to move the sprite:

    ```java title="Main.java"
    TranslateTransition moveSprite = new TranslateTransition(Duration.seconds(2), characterSprite);
    moveSprite.setByX(200); // Move 200 pixels to the right
    moveSprite.setCycleCount(Animation.INDEFINITE); // Loop animation
    moveSprite.setAutoReverse(true); // Reverse direction
    moveSprite.play();
    ```

2. Add the sprite to your layout: 

    ```java title="Main.java"
    stackPane.getChildren().add(characterSprite);
    ```

### Step 3: Optional - Moving Background
If you want the background to move when the player moves:

1. Use a `TranslateTransition` on the `backgroundView` object.
2. Link the background movement to player input (e.g., arrow keys) using event handlers.

!!! warning
Moving both the background and sprite can cause performance issues if not optimized. Test thoroughly!

## Conclusion
<!-- end product is our final game with a moving character sprite and (maybe) a background that moves when the player moves-->

By following these steps, you’ve personalized your JavaFX project with styles, images, and animations. The final product includes:

- A stylesheet for customizing your game’s appearance.
- A background image to enhance visuals.
- An animated sprite that can move across the screen.

Below is an example of the final result:

- A title screen with styled buttons and text.
- A moving character sprite.
- Optional moving background when the player moves.

With these elements in place, your game is now visually polished and ready for additional gameplay mechanics!