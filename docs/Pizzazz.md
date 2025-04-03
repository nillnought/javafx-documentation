# Personalizing and Adding Pizzazz to Your Project
<!-- overview -->
## Overview
Welcome to the world of sprite animation in JavaFX! In this guide, we'll show you how to breathe life into your application by animating a character sprite with smooth movement and directional animations. By the end, you'll have a simple yet dynamic program to kickstart your JavaFX gaming projects.

## Understanding Sprite Animations
Sprite animations are the heart of character movement in 2D games. In our approach, we'll use individual image frames to create fluid, lifelike character movements.

### Sprite Sheet Organization
Your sprite sheet is carefully organized into four directional folders:

- `walk_down/`: Frames for downward movement
- `walk_left/`: Frames for leftward movement
- `walk_right/`: Frames for rightward movement
- `walk_up/`: Frames for upward movement

Each direction contains **8 sequential PNG files** (1.png through 8.png) representing the animation frames.

## Creating Animated Sprites
In the `CharacterSprite` class, animated sprites are created by cycling through the frames using a `Timeline`. Here's how the program handles sprite animations:

```java title="CharacterSprite.java"
private void startAnimation(Direction direction) {
    currentDirection = direction;

    // Stop the previous animation if it exists
    if (animationTimeline != null) {
        animationTimeline.stop();
    }

    // Load frames for the direction
    Image[] frames = loadFrames(direction);

    // Create a timeline to cycle through the frames
    animationTimeline = new Timeline();
    for (int i = 0; i < frames.length; i++) {
        final int index = i;
        animationTimeline.getKeyFrames().add(new KeyFrame(
                Duration.millis(FRAME_DURATION * i),
                event -> spriteView.setImage(frames[index])
        ));
    }
    animationTimeline.setCycleCount(Animation.INDEFINITE); // Loop the animation
    animationTimeline.play();
}
```
!!! tip
    Frames are loaded dynamically based on the direction. The Timeline cycles through the frames, creating a smooth animation.

## Adding Smooth Movement
<!-- how to add images, set backgrounds, maybe make a moving background(? not sure if we want to do that or not [moving bgs might go into the sprites section since its pretty similar]) -->
Smooth movement is achieved using velocity-based updates. The program calculates the character's new position every frame using an `AnimationTimer`. Here's the key part of the code:

```java title="CharacterSprite.java"
new javafx.animation.AnimationTimer() {
    @Override
    public void handle(long now) {
        spriteView.setX(spriteView.getX() + velX);
        spriteView.setY(spriteView.getY() + velY);
    }
}.start();
```
!!! tip
    velX and velY determine the character's velocity (speed and direction).
    When movement keys are pressed, the velocity is updated.
    The AnimationTimer continuously updates the sprite's position, ensuring smooth movement.

## Keyboard Interactions
<!-- how to add images, set backgrounds, maybe make a moving background(? not sure if we want to do that or not [moving bgs might go into the sprites section since its pretty similar]) -->
The program uses keyboard input to control the sprite's movement and animation. Here's how the key handling is implemented:

```java title="CharacterSprite.java"
private void setupKeyControls(Scene scene) {
    scene.setOnKeyPressed(event -> {
        if (pressedKeys.add(event.getCode())) { // Only handle new key presses
            switch (event.getCode()) {
                case W, UP -> {
                    velY = -MOVEMENT_SPEED;
                    startAnimation(Direction.UP);
                }
                case S, DOWN -> {
                    velY = MOVEMENT_SPEED;
                    startAnimation(Direction.DOWN);
                }
                case A, LEFT -> {
                    velX = -MOVEMENT_SPEED;
                    startAnimation(Direction.LEFT);
                }
                case D, RIGHT -> {
                    velX = MOVEMENT_SPEED;
                    startAnimation(Direction.RIGHT);
                }
            }
        }
    });

    scene.setOnKeyReleased(event -> {
        pressedKeys.remove(event.getCode());
        switch (event.getCode()) {
            case W, UP, S, DOWN -> velY = 0;
            case A, LEFT, D, RIGHT -> velX = 0;
        }
        if (pressedKeys.isEmpty()) { // No keys pressed, stop animation
            setIdleSprite();
        }
    });
}
```

## Keyboard Interactions
Make your game interactive with keyboard-based movement:

```java title="CharacterSprite.java"
private void addKeyboardMovement(Scene scene, ImageView characterSprite, ImageView backgroundView) {
    scene.setOnKeyPressed(event -> {
        switch (event.getCode()) {
            case UP:
                characterSprite.setTranslateY(characterSprite.getTranslateY() - 10);
                backgroundView.setTranslateY(backgroundView.getTranslateY() + 10);
                break;
            // Similar cases for DOWN, LEFT, RIGHT
        }
    });
}
```

!!! tip
    Directional Movement: W, A, S, D or arrow keys (UP, DOWN, LEFT, RIGHT) control the sprite's movement.
    The direction determines which animation plays.
    Idle State: When no movement keys are pressed, the animation stops, and the sprite reverts to its idle frame.

## Setting Idle Sprites
The `setIdleSprite` method ensures the character displays a static frame when not moving. This makes your game feel responsive and polished:

```java title="CharacterSprite.java"
private void setIdleSprite() {
    if (animationTimeline != null) {
        animationTimeline.stop();
    }
    String idleFramePath = "assets/sprite/" + currentDirection.path + "1.png";
    spriteView.setImage(new Image(getClass().getResourceAsStream(idleFramePath)));
}
```

## Organizing Sprite Frames
The `loadFrames` method loads the frames for a given direction. This method ensures all the frames are loaded from the `assets/sprite/` directory:

```java title="CharacterSprite.java"
private Image[] loadFrames(Direction direction) {
    Image[] frames = new Image[8]; // Assume 8 frames per direction
    for (int i = 0; i < 8; i++) {
        String framePath = "assets/sprite/" + direction.path + (i + 1) + ".png";
        frames[i] = new Image(getClass().getResourceAsStream(framePath));
    }
    return frames;
}
```

!!! tip
    Each frame is loaded using the Direction enum, which maps to the correct folder path.
    Frames should be consistent in size to ensure smooth animation.

## Best Practices and Performance Tips
- **Preload images:** Load all frames at the start of the game to prevent lag during gameplay.
- **Keep frame sizes consistent:** Ensure all frames are the same width and height to avoid visual glitches.
- **Optimize performance:** Use a smaller number of frames if your game starts to lag.

!!! warning
    Be mindful of memory usage when loading multiple sprite frames. Consider image caching or lazy loading for larger sprite sheets.

## Advanced Customization
Experiment with these techniques to enhance your sprite animation:

- Add frame rate controls
- Implement diagonal movement
- Create transition animations between different movement states

## Conclusion
<!-- end product is our final game with a moving character sprite and (maybe) a background that moves when the player moves-->

Congratulations! You've learned how to create dynamic, animated sprites in JavaFX. Your character now comes to life with smooth, directional movements and an interactive background.

**Key achievements:**

- Implemented multi-directional sprite animations
- Created a scrolling background
- Added keyboard-based character movement

Keep exploring, have fun, and remember - great game design is all about bringing your imagination to life! 🎮🚀