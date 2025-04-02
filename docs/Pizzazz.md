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
    ```java title="Main.java" linenums="1"
    Scene scene = new Scene(layout, 400, 300);
    scene.getStylesheets().add(getClass().getResource("/styles.css").toExternalForm());
    ```

## Adding Images
<!-- how to add images, set backgrounds, maybe make a moving background(? not sure if we want to do that or not [moving bgs might go into the sprites section since its pretty similar]) -->
## Using Sprites
<!-- how to do sprites and animate them, plus maybe moving backgrounds -->

## Conclusion
<!-- end product is our final game with a moving character sprite and (maybe) a background that moves when the player moves-->