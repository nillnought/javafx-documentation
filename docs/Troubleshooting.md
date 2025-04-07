# Troubleshooting Guide

This guide addresses common issues you might encounter while working on your JavaFX projects. Each issue includes possible causes and solutions to help you quickly resolve them.

---

## 1. JavaFX Plugin Not Found in IntelliJ IDEA  
**Problem:**  
The JavaFX plugin is missing or not available in IntelliJ IDEA.  

**Possible Causes:**  
The plugin is not installed or enabled.  
Your IntelliJ IDEA version does not support the JavaFX plugin.  

**Solutions:**  
Go to `File > Settings > Plugins > Marketplace`. Search for "JavaFX" and click **Install**.  
If already installed, ensure it is enabled under **Installed Plugins**.  
Check that you're using IntelliJ IDEA Ultimate or Community Edition (JavaFX support may be limited in older versions).

---

## 2. FXML File Fails to Load  
**Problem:**  
Your application crashes or shows a `NullPointerException` when trying to load an FXML file.  

**Possible Causes:**  
The file path to the FXML file is incorrect.  
The `fx:controller` attribute in the FXML file is missing or points to the wrong class.  
Required elements in the FXML file are missing.  

**Solutions:**  
Verify the FXML file path in your code:  
```java
FXMLLoader loader = new FXMLLoader(getClass().getResource("MainMenu.fxml"));
```
Ensure the `fx:controller` attribute in the FXML file matches the fully qualified name of your controller class:  
```xml
fx:controller="com.javafxtutorial.javafxtutorial.MenuController"
```
Check for missing `fx:id` attributes or required fields in your FXML file.

---

## 3. Buttons or Other UI Elements Do Not Respond  
**Problem:**  
Clicking buttons or interacting with UI elements has no effect.  

**Possible Causes:**  
The `onAction` attribute in the FXML file is not set or is incorrect.  
The method in the controller is missing the `@FXML` annotation.  

**Solutions:**  
Ensure the button's `onAction` attribute is correctly linked to a method in the controller:  
```xml
<Button onAction="#onStartButtonClick" text="Start" />
```
Confirm the controller method is annotated with `@FXML`:  
```java
@FXML
protected void onStartButtonClick() {
    // Your logic here
}
```

---

## 4. Animation Not Working  
**Problem:**  
The sprite animation does not play, or the character appears frozen.  

**Possible Causes:**  
The `Timeline` or `AnimationTimer` is not properly set up or started.  
The image frames for the animation are missing or not properly loaded.  

**Solutions:**  
Make sure the `Timeline` or `AnimationTimer` is started:  
```java
animationTimeline.play();
```
Verify the sprite frames are in the correct directory and the file paths are valid:  
```java
String framePath = "assets/sprite/walk_down/1.png";
```
Use consistent file naming (e.g., `1.png, 2.png`) and frame dimensions for all images in the sprite sheet.

---

## 5. Character Won’t Move  
**Problem:**  
The character does not move when pressing the WASD or arrow keys.  

**Possible Causes:**  
Key input events are not being captured.  
`velX` and `velY` values are not being updated.  
The `AnimationTimer` for movement is not running.  

**Solutions:**  
Ensure that focus is set on the scene to capture key presses:  
```java
scene.setOnKeyPressed(...);
scene.setOnKeyReleased(...);
scene.getRoot().requestFocus();
```
Verify that the velocity values (`velX` and `velY`) are being updated in response to key presses.  
Confirm the `AnimationTimer` for movement is started:  
```java
movementLoop.start();
```

---

## 6. Black Screen or Blank Scene  
**Problem:**  
The application runs, but the screen is black or empty.  

**Possible Causes:**  
No `Scene` has been set on the `Stage`.  
The `Scene` root is empty or not properly initialized.  

**Solutions:**  
Ensure you set a valid `Scene` on the `Stage`:  
```java
stage.setScene(scene);
```
Verify that the root element (e.g., `Group`, `VBox`) contains child elements:  
```java
Group root = new Group();
root.getChildren().add(spriteView);
```

---

## 7. FileNotFoundException or Missing Assets  
**Problem:**  
The application crashes because an image, FXML file, or other asset cannot be found.  

**Possible Causes:**  
The file path is incorrect or the resource is not in the expected directory.  
The file is not included in the project resources.  

**Solutions:**  
Ensure the asset is located in the `resources` folder of your project and that the file path matches:  
```java
new Image(getClass().getResourceAsStream("assets/sprite/walk_down/1.png"));
```
Check that the resource folder is marked correctly in your IDE (right-click the folder > **Mark as Resources Root** in IntelliJ IDEA).

---

## 8. Background Does Not Scroll  
**Problem:**  
The background remains static when the character moves.  

**Possible Causes:**  
The background's `translateX` or `translateY` values are not being updated.  

**Solutions:**  
Update the background position along with the character's movement:  
```java
backgroundView.setTranslateX(backgroundView.getTranslateX() - velX);
backgroundView.setTranslateY(backgroundView.getTranslateY() - velY);
```

---

## 9. Mouse Interaction Not Working  
**Problem:**  
Hovering over or clicking elements does not produce the expected behavior.  

**Possible Causes:**  
The `onMouseEntered`, `onMouseExited`, or `onMouseClicked` attributes are missing from the FXML file.  
The corresponding methods in the controller are not annotated with `@FXML`.  

**Solutions:**  
Ensure the FXML file includes mouse interaction attributes:  
```xml
<Rectangle onMouseEntered="#mouseEnter" onMouseExited="#mouseExit" onMouseClicked="#click" />
```
Verify the controller methods are annotated with `@FXML`:  
```java
@FXML
public void mouseEnter() {
    rectangle.setOpacity(0.5);
}
```

---

## 10. Performance Issues (Lag or Stuttering)  
**Problem:**  
The application lags or animations stutter during runtime.  

**Possible Causes:**  
Too many resources (e.g., images) are being loaded during runtime.  
The frame rate is too high or poorly optimized.  

**Solutions:**  
Preload resources at the start of the application:  
```java
Image[] frames = loadFrames(Direction.DOWN);
```
Reduce the number of animation frames or use smaller images to optimize performance.  
Use `setCycleCount(Animation.INDEFINITE)` for animations to avoid unnecessary overhead.

---

## 11. Application Crashes on Exit  
**Problem:**  
The application does not exit properly or throws an error.  

**Possible Causes:**  
The `System.exit(0)` method is not called for proper termination.  
Background threads (e.g., `AnimationTimer`) are still running.  

**Solutions:**  
Ensure the `onExitButtonClick` method calls `System.exit(0)`:  
```java
@FXML
protected void onExitButtonClick() {
    System.exit(0);
}
```
Stop any running timers or threads before exiting:  
```java
animationTimeline.stop();
```

---

If you encounter an issue not listed here, carefully review your code for typos, missing annotations, or incorrect file paths. Happy coding!