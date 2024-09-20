# Java 8 to 17 Features Overview

This document provides an overview of key features introduced in Java versions 8 through 17, with simple code examples and explanations for non-coders.

## Java 8 (2014)

### 1. Lambda Expressions
**What it is:** A short way to write small functions.
**Example:**
```java
// Before Java 8
Runnable runnable = new Runnable() {
    @Override
    public void run() {
        System.out.println("Hello, Java 8!");
    }
};

// With Java 8 Lambda
Runnable runnableLambda = () -> System.out.println("Hello, Java 8!");
```
**Non-coder explanation:** Think of it as a quick way to tell the computer "do this simple task" without a lot of extra words.

### 2. Stream API
**What it is:** A way to process collections of data more easily.
**Example:**
```java
List<String> names = Arrays.asList("Alice", "Bob", "Charlie");
names.stream()
     .filter(name -> name.startsWith("A"))
     .forEach(System.out::println);
```
**Non-coder explanation:** Imagine you have a list of items and want to quickly find and do something with specific ones. Streams make this easier.

## Java 9 (2017)

### 3. Module System
**What it is:** A way to organize large applications into smaller, more manageable parts.
**Example:**
```java
module com.example.myapp {
    requires java.logging;
    exports com.example.myapp.api;
}
```
**Non-coder explanation:** Think of it as organizing a big project into smaller, more focused folders that can work together.

## Java 10 (2018)

### 4. Local Variable Type Inference
**What it is:** Lets Java guess the type of a variable so you don't have to specify it.
**Example:**
```java
// Before Java 10
String message = "Hello, Java 10!";

// With Java 10
var message = "Hello, Java 10!";
```
**Non-coder explanation:** It's like telling Java "Figure out what type of thing this is" instead of always having to spell it out.

## Java 11 (2018)

### 5. HTTP Client
**What it is:** A built-in way to send HTTP requests (like accessing websites) from Java.
**Example:**
```java
var client = HttpClient.newHttpClient();
var request = HttpRequest.newBuilder()
      .uri(URI.create("https://example.com"))
      .build();
var response = client.send(request, HttpResponse.BodyHandlers.ofString());
System.out.println(response.body());
```
**Non-coder explanation:** This makes it easier for Java programs to communicate with websites and online services.

## Java 14 (2020)

### 6. Switch Expressions
**What it is:** An improved way to make decisions in code.
**Example:**
```java
String day = "MONDAY";
String typeOfDay = switch (day) {
    case "MONDAY", "TUESDAY", "WEDNESDAY", "THURSDAY", "FRIDAY" -> "Weekday";
    case "SATURDAY", "SUNDAY" -> "Weekend";
    default -> "Unknown";
};
```
**Non-coder explanation:** It's like a more powerful version of a light switch, where you can easily handle multiple options and do different things based on each choice.

## Java 15 (2020)

### 7. Text Blocks
**What it is:** An easier way to write multi-line text in code.
**Example:**
```java
String html = """
              <html>
                  <body>
                      <h1>Hello, Java 15!</h1>
                  </body>
              </html>
              """;
```
**Non-coder explanation:** It's like writing a paragraph in your code without having to use special symbols for each new line.

## Java 16 (2021)

### 8. Records
**What it is:** A quick way to create simple data-holding classes.
**Example:**
```java
record Person(String name, int age) {}

// Usage
Person alice = new Person("Alice", 30);
System.out.println(alice.name()); // Prints: Alice
```
**Non-coder explanation:** It's like creating a template for storing related pieces of information together, without having to write a lot of extra code.

## Java 17 (2021) - Long-Term Support (LTS) Version

### 9. Sealed Classes
**What it is:** A way to control which classes can inherit from or implement another class or interface.
**Example:**
```java
sealed class Shape permits Circle, Rectangle, Triangle {}

final class Circle extends Shape {}
final class Rectangle extends Shape {}
final class Triangle extends Shape {}
```
**Non-coder explanation:** It's like creating a "club" of related classes and specifying exactly which classes can be part of that club.

This overview covers some of the most significant features introduced from Java 8 to Java 17. Each version brought more improvements and features, making Java more powerful and easier to use for developers.
