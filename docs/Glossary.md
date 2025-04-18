# Glossary

| Term                     | Definition                                                                                                                                                                                  |
|--------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| JavaFX                  | A Java library used for building graphical user interfaces (GUIs) and creating desktop applications. It provides tools for creating interactive applications with ease.                     |
| IDE (IntelliJ IDEA)     | Integrated Development Environment used for writing and debugging code. IntelliJ IDEA is widely used for Java development, including JavaFX applications.                                     |
| Plugin                  | A software add-on that provides additional functionality to an application. For example, the JavaFX plugin in IntelliJ IDEA helps with JavaFX development.                                    |
| FXML                   | An XML-based language used to define the user interface in JavaFX applications. It separates the UI design from the application logic for easier development.                                  |
| Controller              | A Java class that connects the logic of the application to the user interface elements defined in an FXML file.                                                                              |
| Scene                  | The visual container in a JavaFX application where UI elements are displayed. Think of it as the "canvas" on which you design your application.                                               |
| Stage                  | The primary window in a JavaFX application. A "Stage" contains a "Scene" and represents the main application window.                                                                          |
| VBox                   | A layout container in JavaFX that arranges UI elements vertically.                                                                                                                           |
| AnimationTimer          | A JavaFX class used to create a continuous loop for updating animations or handling repetitive actions.                                                                                       |
| Timeline               | A JavaFX class used to create frame-based animations by defining a sequence of keyframes.                                                                                                     |
| Sprite                | A 2D image or graphic used in animations or games. It represents characters, objects, or other visual elements in a game.                                                                      |
| Sprite Sheet           | A collection of multiple images (frames) arranged in a grid or folder structure, used for creating animations by cycling through the frames.                                                  |
| KeyFrame              | A point in a `Timeline` animation that defines a specific change or action (e.g., changing an image).                                                                                          |
| Directional Animation   | Animations that change based on movement direction (e.g., walking up, down, left, or right).                                                                                                 |
| Velocity               | The speed and direction of an object’s movement. In JavaFX, it’s often controlled using variables like `velX` and `velY`.                                                                     |
| Keyboard Input         | The process of capturing user key presses to control elements in an application, such as moving a character in a game.                                                                        |
| Idle State             | A state where no actions or movement are happening. For example, when no movement keys are pressed, a character can display a still (idle) animation frame.                                    |
| Mouse Interaction      | Capturing user actions like mouse clicks, hovering, or dragging to interact with the application.                                                                                             |
| Group                  | A JavaFX node that acts as a container for other nodes (UI elements). It allows you to group multiple elements together for easier manipulation.                                               |

| Preloading             | A technique used to load resources (e.g., images) before the application starts to reduce lag and improve performance.                                                                         |
| Button                 | A clickable UI element in JavaFX that triggers specific actions when clicked.                                                                                                                 |

| Smooth Movement        | Movement that updates the position of an object in small increments to create fluid motion, often achieved using velocity-based calculations.                                                  |
| Opacity                | The transparency of a UI element in JavaFX. A value of 1 means fully visible, while 0 means completely invisible.                                                                             |
| Lazy Loading           | Loading resources like images only when they are needed to save memory and improve application performance.                                                                                   |