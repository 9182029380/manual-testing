# Design Patterns in Java: Notes and Examples

## Creational Design Patterns

### 1. Singleton Pattern

**Purpose:** Ensures that a class has only one instance and provides a global point of access to it.

**Explanation:** 
- Useful when exactly one object is needed to coordinate actions across the system.
- Common uses: managing a connection to a database, file system, or hardware device.

**Java Implementation:**

```java
public class Singleton {
    private static Singleton instance;
    
    private Singleton() {}
    
    public static Singleton getInstance() {
        if (instance == null) {
            instance = new Singleton();
        }
        return instance;
    }
    
    public void showMessage() {
        System.out.println("Hello from Singleton!");
    }
}
```

**Usage:**
```java
Singleton object = Singleton.getInstance();
object.showMessage();
```

**Non-coder explanation:** Think of a Singleton like a one-of-a-kind item in a video game. No matter how many times you try to create it, you always get the same unique item.

### 2. Factory Pattern

**Purpose:** Creates objects without exposing the instantiation logic to the client.

**Explanation:**
- Useful when a class cannot anticipate the type of objects it needs to create.
- Provides a way to delegate the object creation to subclasses.

**Java Implementation (Factory Method):**

```java
interface Animal {
    void speak();
}

class Dog implements Animal {
    public void speak() {
        System.out.println("Woof!");
    }
}

class Cat implements Animal {
    public void speak() {
        System.out.println("Meow!");
    }
}

class AnimalFactory {
    public Animal createAnimal(String animalType) {
        if (animalType.equalsIgnoreCase("dog")) {
            return new Dog();
        } else if (animalType.equalsIgnoreCase("cat")) {
            return new Cat();
        }
        return null;
    }
}
```

**Usage:**
```java
AnimalFactory factory = new AnimalFactory();
Animal dog = factory.createAnimal("dog");
dog.speak(); // Output: Woof!
```

**Non-coder explanation:** Imagine a toy factory. You ask for a specific toy, and the factory creates it for you without you needing to know how it's made.

## Structural Design Patterns

### 1. Adapter Pattern

**Purpose:** Allows incompatible interfaces to work together.

**Explanation:**
- Useful when you want to use an existing class, but its interface doesn't match the one you need.
- Acts as a bridge between two incompatible interfaces.

**Java Implementation:**

```java
interface MediaPlayer {
    void play(String audioType, String fileName);
}

interface AdvancedMediaPlayer {
    void playVlc(String fileName);
    void playMp4(String fileName);
}

class VlcPlayer implements AdvancedMediaPlayer {
    public void playVlc(String fileName) {
        System.out.println("Playing vlc file: " + fileName);
    }
    public void playMp4(String fileName) {}
}

class MediaAdapter implements MediaPlayer {
    AdvancedMediaPlayer advancedMusicPlayer;

    public MediaAdapter(String audioType) {
        if (audioType.equalsIgnoreCase("vlc")) {
            advancedMusicPlayer = new VlcPlayer();
        }
    }

    public void play(String audioType, String fileName) {
        if (audioType.equalsIgnoreCase("vlc")) {
            advancedMusicPlayer.playVlc(fileName);
        }
    }
}
```

**Usage:**
```java
MediaPlayer player = new MediaAdapter("vlc");
player.play("vlc", "song.vlc");
```

**Non-coder explanation:** Think of an adapter like a travel power plug adapter. It allows you to use your device (with its specific plug) in a foreign country with a different socket type.

### 2. Decorator Pattern

**Purpose:** Adds new functionality to an object without altering its structure.

**Explanation:**
- Useful for extending the functionality of classes without modifying their code.
- Allows behavior to be added to individual objects, either statically or dynamically.

**Java Implementation:**

```java
interface Coffee {
    double getCost();
    String getDescription();
}

class SimpleCoffee implements Coffee {
    public double getCost() {
        return 1;
    }
    public String getDescription() {
        return "Simple coffee";
    }
}

abstract class CoffeeDecorator implements Coffee {
    protected Coffee decoratedCoffee;
    
    public CoffeeDecorator(Coffee c) {
        this.decoratedCoffee = c;
    }

    public double getCost() {
        return decoratedCoffee.getCost();
    }
    public String getDescription() {
        return decoratedCoffee.getDescription();
    }
}

class Milk extends CoffeeDecorator {
    public Milk(Coffee c) {
        super(c);
    }
    public double getCost() {
        return super.getCost() + 0.5;
    }
    public String getDescription() {
        return super.getDescription() + ", milk";
    }
}
```

**Usage:**
```java
Coffee c = new SimpleCoffee();
c = new Milk(c);
System.out.println(c.getCost()); // Output: 1.5
System.out.println(c.getDescription()); // Output: Simple coffee, milk
```

**Non-coder explanation:** Imagine customizing a car. You start with a basic model and add features (like leather seats or a better stereo) without changing the car's core structure.

## Behavioral Design Patterns

### 1. Observer Pattern

**Purpose:** Defines a one-to-many dependency between objects so that when one object changes state, all its dependents are notified and updated automatically.

**Explanation:**
- Useful when you need many other objects to receive an update when another object changes.
- Often used in event handling systems.

**Java Implementation:**

```java
import java.util.ArrayList;
import java.util.List;

interface Observer {
    void update(String message);
}

class NewsAgency {
    private List<Observer> observers = new ArrayList<>();
    private String news;

    public void addObserver(Observer observer) {
        observers.add(observer);
    }

    public void setNews(String news) {
        this.news = news;
        for (Observer observer : observers) {
            observer.update(news);
        }
    }
}

class NewsChannel implements Observer {
    private String news;

    @Override
    public void update(String news) {
        this.news = news;
        System.out.println("Channel received news: " + news);
    }
}
```

**Usage:**
```java
NewsAgency agency = new NewsAgency();
NewsChannel channel1 = new NewsChannel();
NewsChannel channel2 = new NewsChannel();

agency.addObserver(channel1);
agency.addObserver(channel2);

agency.setNews("Breaking News!");
```

**Non-coder explanation:** Think of it like a newspaper subscription. When the newspaper (subject) publishes a new edition, all subscribers (observers) automatically receive it.

### 2. Prototype Pattern

**Purpose:** Creates new objects by cloning existing objects, avoiding the need for creating subclasses.

**Explanation:**
- Useful when the cost of creating a new object is more expensive than copying an existing one.
- Allows you to copy existing objects without making your code dependent on their classes.

**Java Implementation:**

```java
interface Prototype {
    Prototype clone();
}

class ConcretePrototype implements Prototype {
    private String name;

    public ConcretePrototype(String name) {
        this.name = name;
    }

    @Override
    public Prototype clone() {
        return new ConcretePrototype(name);
    }

    public void setName(String name) {
        this.name = name;
    }

    public String getName() {
        return name;
    }
}
```

**Usage:**
```java
ConcretePrototype original = new ConcretePrototype("Original");
ConcretePrototype clone = (ConcretePrototype) original.clone();
System.out.println(clone.getName()); // Output: Original
```

**Non-coder explanation:** Imagine you have a document template. Instead of creating a new document from scratch each time, you make copies of the template and modify them as needed.

These design patterns are fundamental concepts in software engineering, each solving common problems in object-oriented design. Understanding them can greatly improve code organization, flexibility, and reusability.
