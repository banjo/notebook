# Java

## MOOC

Notes from Helsinki MOOC.

- [Java](#java)
  - [MOOC](#mooc)
    - [Iterator](#iterator)
      - [Iterator to print](#iterator-to-print)
      - [Print with more than one "HasNext"](#print-with-more-than-one-hasnext)
      - [Remove with iterator](#remove-with-iterator)
    - [Comparator](#comparator)
      - [Sort](#sort)
    - [Enumerator](#enumerator)
      - [Enumerator basics](#enumerator-basics)
      - [Enumerator with names](#enumerator-with-names)
    - [Interface](#interface)
      - [Create readable](#create-readable)
      - [Ebook Example](#ebook-example)
      - [Interface example](#interface-example)
    - [Swing](#swing)
      - [Basic UserInterface](#basic-userinterface)
      - [Border Layout](#border-layout)
      - [Box Layout](#box-layout)
      - [Grid Layout](#grid-layout)
      - [Button Group](#button-group)
      - [Basic Action Listener](#basic-action-listener)
      - [Action Listener With Action](#action-listener-with-action)
      - [Action Listener with Multiple Buttons](#action-listener-with-multiple-buttons)
      - [Basic jPanel](#basic-jpanel)
      - [jPanel as Class](#jpanel-as-class)
      - [jPanel Best Practice](#jpanel-best-practice)
      - [jPanel with Graphics](#jpanel-with-graphics)
    - [Regular Expressions](#regular-expressions)

### Iterator

How to use an iterator. Below is an example that will use an iterator.

```java
public class Hand {
    private ArrayList<Card> cards;
    public Hand() {
        cards = new ArrayList<Hand>();
    }

    public void add(Card card){
        cards.add(card);
    }

  // this part is going to be used by the iterator
    public void print(){
        for (Card card : cards) {
            System.out.println( card );
        }
    }
}
```

#### Iterator to print

```java
public void print() {
    Iterator<Card> iterator = cards.iterator();

    while ( iterator.hasNext() ){
        System.out.println( iterator.next() );
    }
}
```

#### Print with more than one "HasNext"

```java
public void print(Education education) {
    Iterator<Person> iterator = employees.iterator();
    while (iterator.hasNext()) {

        // if you use "iterator.next" more than one time, make it to a variable.
        Person person = iterator.next();

        if (person.getEducation() == education) {
            System.out.println(person);
        }
    }
}
```

#### Remove with iterator

You can't remove objects while iterating through them, in that case you can use an iterator.

```java
public class Hand {
    // ...
    public void deleteWorst(int value) {
        Iterator<Card> iterator = cards.iterator();
        while (iterator.hasNext()) {
            if (iterator.next().getValue() < value) {
                // delete the object returned by the iterator with its previous method call
                iterator.remove();
            }
        }
    }
}
```

### Comparator

How to use a comparator to sort.

#### Sort

```java
	// sort movies based on their rating
public class FilmComparator implements Comparator<Film> {
    private Map<Film, List<Rating>> ratings;
    public FilmComparator(Map<Film, List<Rating>> ratings) {
        this.ratings = ratings;
    }
    //...
    @Override
    public int compare(Film o1, Film o2) {
        return (getAverageRating(o2) - getAverageRating(o1)); //this will return them in an decending order (biggest first)
    }
}
// the object needs to implement "Comparator", with the object you want to base your sorting on.
```

Main might look like this:

```java
List<Film> films = Arrays.asList(goneWithTheWind, theBridgesOfMadisonCounty, eraserhead);
System.out.println("The films before sorting: " + films);
Collections.sort(films, new FilmComparator(filmRatings));
System.out.println("The films after sorting: " + films);
```

### Enumerator

#### Enumerator basics

This is how an enumerator looks - with 4 suits in a card deck.

```java
public enum Suit {
  DIAMONDS, SPADES, CLUBS, HEARTS
}
```

A class called "Card" the implements the enumerator.

```java
public class Card {
    private int value;
    private Suit suit;
    public Card(int value, Suit suit) {
        this.value = value;
        this.suit = suit;
    }
    @Override
    public String toString() {
        return suit + " "+value;
    }
    public Suit getSuit() {
        return suit;
    }
    public int getValue() {
        return value;
    }
}
```

How the class and enumerator is used in Main.

```java
public class Main {
    public static void main(String[] args) {
        Card first = new Card(10, Suit.HEARTS);
        System.out.println(first);
        if (first.getSuit() == Suit.CLUBS) {
            System.out.println("It's clubs");
        } else {
            System.out.println("It's not clubs");
        }
    }
}

```

#### Enumerator with names

```java
public enum Colour {
    RED("red"), // the constructor parameters are defined as constant values when they are read
    GREEN("green"),
    BLUE("blue");

    private String name; // object variable

    private Colour(String name) { // constructor
        this.name = name;
    }

    public String getName() {
        return this.name;
    }
}
```

### Interface

Basics on how to use an interface.

#### Create readable

```java
// SMS is usually created was an SMS class, but it can be created as an Readable.
SMS message = new SMS("teacher", "Awesome stuff!");
Readable readable = new SMS("teacher", "The SMS is Readable!");

// same goes for arraylists.
ArrayList<Readable> numberList = new ArrayList<Readable>();
numberList.add(new SMS("teacher", "never been programming before..."));
numberList.add(new SMS("teacher", "gonna love it i think!"));
numberList.add(new SMS("teacher", "give me something more challenging! :)"));
numberList.add(new SMS("teacher", "you think i can do it?"));
numberList.add(new SMS("teacher", "up here we send several messages each day"));

for (Readable readable: numberList) {
    System.out.println(readable.read());
}
```

#### Ebook Example

```java
public class EBook implements Readable {
    private String name;
    private ArrayList<String> pages;
    private int pageNumber;
    public EBook(String name, ArrayList<String> pages) {
        this.name = name;
        this.pages = pages;
        this.pageNumber = 0;
    }
    public String getName() {
        return this.name;
    }
    public int howManyPages() {
        return this.pages.size();
    }

      // it contains the read function. If you call someting readable, this is the function you can access.
    public String read() {
        String page = this.pages.get(this.pageNumber);
        nextPage();
        return page;
    }
    private void nextPage() {
        this.pageNumber = this.pageNumber + 1;
        if(this.pageNumber % this.pages.size() == 0) {
            this.pageNumber = 0;
        }
    }
}
```

#### Interface example

Simple example how to implement an interface called Readable.

```java
public interface Readable {
  // everything the implements Readable must have a function called read which returns a string.
  String read();
}
```

How to use the Readable interface.

```java
 // uses the println to read the class the implemented readable
SMS message = new SMS("ope", "Awesome stuff!");
System.out.println(message.read());

ArrayList<SMS> messages = new ArrayList<SMS>();
messages.add(new SMS("unknown number", "I hid the body.");
```

### Swing

How to create a java application using Swing.

#### Basic UserInterface

This is a basic program with Swing.

```java
import java.awt.Container;
import java.awt.Dimension;
import javax.swing.JFrame;
import javax.swing.WindowConstants;

public class UserInterface implements Runnable {
    private JFrame frame;
    public UserInterface() {
    }

    @Override
    public void run() {
        frame = new JFrame("Title");
        frame.setPreferredSize(new Dimension(200, 100));
        frame.setDefaultCloseOperation(WindowConstants.EXIT_ON_CLOSE);
        createComponents(frame.getContentPane());
        frame.pack();
        frame.setVisible(true);
    }

    private void createComponents(Container container) {
      // create all components of the program here
       JLabel text = new JLabel("Text field!");
       container.add(text);
    }

    public JFrame getFrame() {
        return frame;
    }
}
```

To activate it in Main.

```java
import javax.swing.SwingUtilities;
public class Main {
    public static void main(String[] args) {
        UserInterface ui = new UserInterface();
        SwingUtilities.invokeLater(ui);
    }
}
```

#### Border Layout

How border layout works in Swing.

```java
private void createComponents(Container container) {
    // the following line is not essential in this case, because BorderLayout is default in JFrame
    container.setLayout(new BorderLayout());
    container.add(new JButton("North"), BorderLayout.NORTH);
    container.add(new JButton("East"), BorderLayout.EAST);
    container.add(new JButton("South"), BorderLayout.SOUTH);
    container.add(new JButton("West"), BorderLayout.WEST);
    container.add(new JButton("Center"), BorderLayout.CENTER);
    container.add(new JButton("Default (Center)"));
}
```

See how it looks [here](https://drive.google.com/open?id=1f13iNuCeeHmwLUL9qlpAN_P5ofbgwjNb).

#### Box Layout

How a box layout works.

```java
private void createComponents(Container container) {

    // X = horizontal, Y = verical.
BoxLayout layout = new BoxLayout(container, BoxLayout.X_AXIS);
container.setLayout(layout);
container.add(new JLabel("First!"));
container.add(new JLabel("Second!"));
container.add(new JLabel("Third!"));
}
```

#### Grid Layout

Vertical

```java
private void createComponents(Container container) {
    GridLayout layout = new GridLayout(3, 1);
    container.setLayout(layout);
    JTextArea textAreaLeft = new JTextArea("The Copier");
    JTextArea textAreaRight = new JTextArea();
    JButton copyButton = new JButton("Copy!");
    container.add(textAreaLeft);
    container.add(copyButton);
    container.add(textAreaRight);
}
```

Horizontal

```java
private void createComponents(Container container) {
    GridLayout layout = new GridLayout(1, 3);
    container.setLayout(layout);
    JTextArea textAreaLeft = new JTextArea("The Copier");
    JTextArea textAreaRight = new JTextArea();
    JButton copyButton = new JButton("Copy!");
    container.add(textAreaLeft);
    container.add(copyButton);
    container.add(textAreaRight);
}
```

Picture [here](https://drive.google.com/open?id=1aj7AZLfWDhFsrwLzptU2VjJUie__sHqm).

#### Button Group

How to create a button group in Swing.

```java
private void createComponents(Container container) {
    BoxLayout layout = new BoxLayout(container, BoxLayout.Y_AXIS);
    container.setLayout(layout);
    container.add(new JLabel("Choose meat or fish:"));
    JRadioButton meat = new JRadioButton("Meat");
    JRadioButton fish = new JRadioButton("Fish");
    ButtonGroup buttonGroup = new ButtonGroup();
    buttonGroup.add(meat);
    buttonGroup.add(fish);
    container.add(meat);
    container.add(fish);
}
```

#### Basic Action Listener

How to use an action listener.

```java
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
public class MessageListener implements ActionListener {
    @Override
    public void actionPerformed(ActionEvent ae) {
        System.out.println("Message received!");
    }
}
```

Activate it in "createComponents"

```java
private void createComponents(Container container) {
    JButton button = new JButton("Send!");
    button.addActionListener(new MessageListener());
    container.add(button);
}
```

#### Action Listener With Action

```java
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import javax.swing.JTextArea;
public class AreaCopier implements ActionListener {
    private JTextArea origin;
    private JTextArea destination;
    public AreaCopier(JTextArea origin, JTextArea destination) {
        this.origin = origin;
        this.destination = destination;
    }
    @Override
    public void actionPerformed(ActionEvent ae) {
        this.destination.setText(this.origin.getText());
    }
}
```

How it looks in "createComponents"

```java
private void createComponents(Container container) {
    GridLayout layout = new GridLayout(1, 3);
    container.setLayout(layout);
    JTextArea textAreaLeft = new JTextArea("The Copier");
    JTextArea textAreaRight = new JTextArea();
    JButton copyButton = new JButton("Copy!");
    AreaCopier copier = new AreaCopier(textAreaLeft, textAreaRight);
    copyButton.addActionListener(copier);
    container.add(textAreaLeft);
    container.add(copyButton);
    container.add(textAreaRight);
}
```

#### Action Listener with Multiple Buttons

Basic way to use action listener with multiple buttons.

```java
    public class ActionListenerExample implements ActionListener {

    @Override
      public void actionPerformed(ActionEvent e) {

        if (e.getSource() == button1){
              doSomething();
        } else if (e.getSoruce() == button2){
              doSomethingElse();
        }
    }
}


// buttons need to be added to action listener with the following command:
JButton button = new JButton("Button1");
button.addActionListener(ActionListenerExample);
```

#### Basic jPanel

Basic jPanel without inheritance.

```java
private void createComponents(Container container) {
    container.add(new JTextArea());
    container.add(createPanel(), BorderLayout.SOUTH);
}
private JPanel createPanel() {
    JPanel panel = new JPanel(new GridLayout(1, 3));
    panel.add(new JButton("Execute"));
    panel.add(new JButton("Test"));
    panel.add(new JButton("Send"));
    return panel;
}
```

Picture can be seen [here](https://drive.google.com/open?id=1yjA0ofoYlmvkGN2LvyKWrhvB9WTus5Yv).

#### jPanel as Class

The class looks like this.

```java
import java.awt.GridLayout;
import javax.swing.JButton;
import javax.swing.JPanel;
public class MenuPanel extends JPanel {
    public MenuPanel() {
        super(new GridLayout(1, 3));
        createComponents();
    }
    private void createComponents() {
        add(new JButton("Execute"));
        add(new JButton("Test"));
        add(new JButton("Send"));
    }
}
//Note that in case you need an action event listener, the class MenuPanel must be given all the objects its need as parameter.
```

Implemented like this:

```java
private void createComponents(Container container) {
    container.add(new JTextArea());
    container.add(new MenuPanel(), BorderLayout.SOUTH);
}
```

#### jPanel Best Practice

According to MOOC it should look like this:

```java
private void createComponents(Container container) {

    frame.setLayout(new GridLayout(3, 1));

    JTextField resultField = new JTextField("0");
    container.add(resultField);
    resultField.setEnabled(false);
    JTextField inputField = new JTextField("");
    container.add(inputField);

    JButton plus = new JButton("+");
    JButton minus = new JButton("-");
    JButton reset = new JButton("Z");

    EventListener handler = new EventListener(plus, minus, reset, resultField, inputField); //action listener

    plus.addActionListener(handler);
    minus.addActionListener(handler);
    reset.addActionListener(handler);

    reset.setEnabled(false);

        // create jpanel in the createComponentsFunction
    JPanel panel = new JPanel(new GridLayout(1, 3));
    panel.add(plus);
    panel.add(minus);
    panel.add(reset);
    container.add(panel);
}
```

#### jPanel with Graphics

Created with paintComponent.

Basic layout:

```java
public class DrawingBoard extends JPanel {
    public DrawingBoard() {
        super.setBackground(Color.WHITE);
    }
    @Override
    protected void paintComponent(Graphics graphics) {
        super.paintComponent(graphics);
    }
}
```

Example:

```java
@Override
protected void paintComponent(Graphics graphics) {
    super.paintComponent(graphics);
    graphics.setColor(Color.GREEN);
    graphics.fillRect(0, 0, 10, 200);
    graphics.setColor(Color.BLACK);
    graphics.fillRect(0, 0, 200, 10);
}
```

x, y, length, height (from top left on x and y)
Picture [here](https://drive.google.com/open?id=1n7qSP0YUSrI3TmWraaIS30XrA2RqayH6).

createComponents:

```java
private void createComponents(Container container) {
    container.add(new DrawingBoard());
}
```

### Regular Expressions

Regular expression summary:

```java
// use "matches" to use regex
if (num.matches("01[0-9]{7}") {
  return true;
}

// regex codes

// specific numbers, [] and {}.
String regex = "01[0-9]{7}"         // starts with "01", followed by 7 numbers between 0 and 9.
String example = "015748337"        // correct match
String wrongExample = "02443342"    // no match
// | - OR operator
String regex = "00|111"         // if the example is exactly 00 or 111, its a match (like equals, not contain)
String example = "00"           // correct example
String wrongExample = "11"      // incorrect

// () - round brackets
String regex = "0(0|1)"         // limit choice to only that part of the string. Starts with 0, and ends with 0 or 1.
String example = "01"           // correct
String example = "00"           // correct
String wrongExample = "11"      // incorrect

// * - repitition symbol from 0 to n
String regex = "trolo(lo)*"             // checks for repition from 0 to n times on the last part "lo".
String example = "trolololololo"        // correct
String wrongExample = "trololol"        // incorrect

// + - repitition symbol from 0 to 1
String regex = "trolo(lo)+"             // checks for repition 0 or 1 times".
String example = "trololo"              // correct
String wrongExample = "trolololo"       // incorrect

// ? - repitition symbol from 0 or 1
String regex = "You have accidentally (deleted)? the whole name"            // checks for repition from 0 or 1 times.
String example = "You have accidentally the whole name"                     // correct
String wrongExample = "trolololo"                                           // incorrect

// {a} - repitition of a times
String regex = "(10){2}"            // checks for repition of 10 two times.
String example = "1010"             // correct
String wrongExample = "101010"      // incorrect
// {a, b} - repitition of a to b times
String regex = "(1){2, 4}"      // checks for repition of 1 for 2, 3 or 4 times.
String example = "111"          // correct
String wrongExample = "1"       // incorrect

// {a,} - repitition of a to n times
String regex = "(1){2,}"        // checks for repition of 1 for 2 or more times.
String example = "1111"         // correct
String wrongExample = "1"       // incorrect

// [] - range of numbers
String regex = "[2-36-9]"       // same as (2|3|6|7|8|9).
String example = "7"            // correct
String wrongExample = "1"       // incorrect

```
