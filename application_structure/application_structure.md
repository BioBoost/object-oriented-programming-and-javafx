<!-- toc -->

# Application Structure

In general, a JavaFX application will have three major components namely Stage, Scene and Nodes as shown in the following diagram.

![Basic Application Architecture](https://www.lucidchart.com/publicSegments/view/760a30a9-9bf5-42bf-9e01-9e431041e1a3/image.png)

## Stage
A stage, in other GUI libraries often known as a Windows, contains all the objects of a JavaFX application. It is the top level container. The primary Stage is constructed by the platform. Additional Stage objects may be constructed by the application.

A stage has one of the following styles:

* StageStyle.DECORATED - a stage with a solid white background and platform decorations.
* StageStyle.UNDECORATED - a stage with a solid white background and no decorations.
* StageStyle.TRANSPARENT - a stage with a transparent background and no decorations.
* StageStyle.UTILITY - a stage with a solid white background and minimal platform decorations.
The style must be initialized before the stage is made visible.

## Scene
A scene represents the physical contents of a JavaFX application. It contains all the contents of a scene graph. A scene object is added to only one stage.

## Scene Graph and Nodes

A scene graph is a tree-like data structure (hierarchical) representing the contents of a scene. In contrast, a node is a visual/graphical object of a scene graph.

The diagram below shows an abstract example of a scene and its scene graph.

![A Simple JavaFX Scene](https://www.lucidchart.com/publicSegments/view/755ee6e2-8d01-4201-92b5-1f76b9801e0c/image.png)

The JavaFX Scene Graph API makes graphical user interfaces easier to create, especially when complex visual effects and transformations are involved. A scene graph is a tree data structure, most commonly found in graphical applications and libraries such as vector editing tools, 3D libraries, and video games. The JavaFX scene graph is a retained mode API, meaning that it maintains an internal model of all graphical objects in your application. At any given time, it knows what objects to display, what areas of the screen need repainting, and how to render it all in the most efficient manner. Instead of invoking primitive drawing methods directly, you instead use the scene graph API and let the system automatically handle the rendering details. This approach significantly reduces the amount of code that is needed in your application.

The individual items held within the JavaFX scene graph are known as nodes. Each node is classified as either a branch node (meaning that it can have children), or a leaf node (meaning that it cannot have children). The first node in the tree is always called the root node, and it never has a parent. See a general diagram below.

![Node Tree [^1]](img/node_tree.png)

[^1]: Source http://docs.oracle.com/javafx/2/scenegraph/jfxpub-scenegraph.htm

A single element in a scene graph is called a **node**. Each node has an
* **ID:** Each node in the scene graph can be given a unique id. This id is much like the "id" attribute of an HTML tag in that it is up to the designer and developer to ensure that the id is unique within the scene graph. The ID can be used to find a node within the scene graph, or within a subtree of the scene graph. The id can also be used identify nodes for applying styles.
* **Style class:** The style class can be used to style the node from CSS. The id and styleClass variables are used in CSS style sheets to identify nodes to which styles should be applied.
* **Bounding volume:** Every node has a geometric shape and it is positioned in a coordinate system. The size and the position of the node are collectively knows as its bound. The bound of a node are defined in terms of a bounding rectangular box that closes the entire geometry of the node.

A node may include:

* Geometrical (Graphical) objects (2D and 3D) such as − Circle, Rectangle, Polygon, etc.
* UI Controls such as − Button, Checkbox, Choice Box, Text Area, etc.
* Containers (Layout Panes) such as Border Pane, Grid Pane, Flow Pane, etc.
* Media elements such as Audio, Video and Image Objects.

The Node Class represents a node in JavaFX, this class is the super class of all other above mentioned types of nodes.

Nodes can be categorized as follows:

* Root Node − The first Scene Graph is known as the Root node.

* Branch Node/Parent Node − The node with child nodes are known as branch/parent nodes. The abstract class named Parent of the package javafx.scene is the base class of all the parent nodes, and those parent nodes will be of the following types

  * Group − A group node is a collective node that contains a list of children nodes. Whenever the group node is rendered, all its child nodes are rendered in order. Any transformation, effect state applied on the group will be applied to all the child nodes.

  * Region − It is the base class of all the JavaFX Node based UI Controls, such as Chart, Pane and Control.

  * WebView − This node manages the web engine and displays its contents.

* Leaf Node − The node without child nodes is known as the leaf node. For example, Rectangle, Ellipse, Box, ImageView, MediaView, ...

## Hello World

It's time to begin our code journey with JavaFX. Let's try it out and create a simple "Hello World" application.

Create a new project in NetBeans and select "JavaFX => JavaFX Application" as project template.

![JavaFX and NetBeans](img/javafx_and_netbeans.png)

Give the application a decent name such as 'JavaFX_HelloWorld'.

You can run the application by pressing the Run button. You will get a window with a single button. If you press it, a "Hello World" message will be printed to the console.

![JavaFX and NetBeans](img/hello_world.png)

Congratulations, you just build your first JavaFX application.

### Code Analysis

```java
/*
 * To change this license header, choose License Headers in Project Properties.
 * To change this template file, choose Tools | Templates
 * and open the template in the editor.
 */
package javafx_helloworld;

import javafx.application.Application;
import javafx.event.ActionEvent;
import javafx.event.EventHandler;
import javafx.scene.Scene;
import javafx.scene.control.Button;
import javafx.scene.layout.StackPane;
import javafx.stage.Stage;

/**
 *
 * @author Nico De Witte
 */
public class JavaFX_HelloWorld extends Application {

    @Override
    public void start(Stage primaryStage) {
        Button btn = new Button();
        btn.setText("Say 'Hello World'");
        btn.setOnAction(new EventHandler<ActionEvent>() {

            @Override
            public void handle(ActionEvent event) {
                System.out.println("Hello World!");
            }
        });

        StackPane root = new StackPane();
        root.getChildren().add(btn);

        Scene scene = new Scene(root, 300, 250);

        primaryStage.setTitle("Hello World!");
        primaryStage.setScene(scene);
        primaryStage.show();
    }

    /**
     * @param args the command line arguments
     */
    public static void main(String[] args) {
        launch(args);
    }

}
```

Let's analyze the above code and try to understand how it works.

#### Extending the Application class

The first thing to note is that the `JavaFX_HelloWorld` class (or other program class name you chose) extends the class `Application`.

The entry point for JavaFX applications is the Application class. The JavaFX runtime does the following, in order, whenever an application is launched (this is called the lifecycle of a JavaFX program):

* Constructs an instance of the specified Application class
* Calls the init() method
* Calls the start(javafx.stage.Stage) method
* Waits for the application to finish, which happens when either of the following occur:
  * the application calls Platform.exit()
  * the last window has been closed and the implicitExit attribute on Platform is true
* Calls the stop() method

Note that the start method is abstract and must be overridden. The init and stop methods have concrete implementations that do nothing.

More information can be found @ https://docs.oracle.com/javase/8/javafx/api/javafx/application/Application.html

#### Launching the JavaFX application

As any Java program, the actual entry point is still the `static void main` method which is called first. To allow the actual JavaFX framework to start, a call is made to the launch() method of the Application class. This will launch a standalone application.

#### The start method

Most of the logic can be found in the start() method.

The first couple of lines are responsible for the instantiation of a Button object. This button first has its caption set and next an event handler is attached. More on event handlers later. For now all you need to know is that if the user presses the button the code of the handle() method is executed.

```java
Button btn = new Button();
btn.setText("Say 'Hello World'");
btn.setOnAction(new EventHandler<ActionEvent>() {

    @Override
    public void handle(ActionEvent event) {
        System.out.println("Hello World!");
    }
});
```

Next the root node of the Scene graph is created. This is standard an object of type `StackPane`. StackPane is a layout pane which lays out its children in a back-to-front stack. More on layout panes later.

After creating the StackPane, the button is added to the pane so it will shown when the application is run.

```java
StackPane root = new StackPane();
root.getChildren().add(btn);
```

Now that we have a root node with a leaf node, we still have to create the actual Scene. This is done using the code below. Note how the root node is passed to the constructor, together with the dimensions of the scene.

```java
Scene scene = new Scene(root, 300, 250);
```

Last but not least some properties of the primary stage are set such as its title (this will be displayed in the title bar). Next the current scene displayed in the stage is set to the scene we just created. And last but not least, the show method is called which makes the stage visible to the user.

```java
primaryStage.setTitle("Hello World!");
primaryStage.setScene(scene);
primaryStage.show();
```
