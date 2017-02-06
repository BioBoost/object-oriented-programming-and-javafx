# Solutions

## Application Structure

### Second Button

The main clue lies in the fact that the StackPane needed to be replaced with a FlowPane layout. This will place controls after each other (left to right) in a flow-like-manner.

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
import javafx.scene.layout.FlowPane;
import javafx.stage.Stage;

/**
 *
 * @author Nico De Witte
 */
public class JavaFX_HelloWorld extends Application {

    @Override
    public void start(Stage primaryStage) {
        Button sayHello = new Button();
        sayHello.setText("Say 'Hello World'");
        sayHello.setOnAction(new EventHandler<ActionEvent>() {

            @Override
            public void handle(ActionEvent event) {
                System.out.println("Hello World!");
            }
        });

        Button sayHal = new Button();
        sayHal.setText("Say 'I am HAL'");
        sayHal.setOnAction(new EventHandler<ActionEvent>() {

            @Override
            public void handle(ActionEvent event) {
                System.out.println("I am HAL");
            }
        });

        FlowPane root = new FlowPane();
        root.getChildren().add(sayHello);
        root.getChildren().add(sayHal);

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

### Nine buttons keypad

```java
/*
 * To change this license header, choose License Headers in Project Properties.
 * To change this template file, choose Tools | Templates
 * and open the template in the editor.
 */
package javafx_keypad;

import javafx.application.Application;
import javafx.event.Event;
import javafx.event.EventHandler;
import javafx.scene.Scene;
import javafx.scene.control.Button;
import javafx.scene.layout.FlowPane;
import javafx.stage.Stage;

/**
 *
 * @author Nico De Witte
 */
public class JavaFX_Keypad extends Application {

    @Override
    public void start(Stage primaryStage) {
        FlowPane flow = new FlowPane();
        flow.setVgap(5);
        flow.setHgap(5);

        for (int i = 0; i < 9; i++) {
            Button button = new Button();
            button.setText("" + i);
            button.setMinSize(80, 80);

            button.setOnAction(new EventHandler() {
                @Override
                public void handle(Event event) {
                    System.out.println("You pressed a button");
                }
            });

            flow.getChildren().add(button);
        }

        Scene scene = new Scene(flow, 255, 255);

        primaryStage.setTitle("Make some noise");
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
