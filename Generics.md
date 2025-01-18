# GENERICS

-> Generics in Java is a feature that allows us to create reusable classes and methods that can work with different data types.
-> Generics let us write true polymorphic code that works with any data type.

-> public interface Map<K,V>{

  }
  <K> - the type of keys maintained by this Map
  <V> - the type of mapped values

## Why we need Generics

```java
// Non-generic implementation of Pair class
public class Pair {
    private Object first; // Can store any type of object
    private Object second; // Can store any type of object

    // Constructor to initialize the Pair with any objects
    public Pair(Object first, Object second) {
        this.first = first;
        this.second = second;
    }

    // Get the first object; requires casting to the original type
    public Object getFirst() {
        return first;
    }

    // Get the second object; requires casting to the original type
    public Object getSecond() {
        return second;
    }

    // Set the first object; no compile-time type checking
    public void setFirst(Object first) {
        this.first = first;
    }

    // Set the second object; no compile-time type checking
    public void setSecond(Object second) {
        this.second = second;
    }
}

// Example usage
Pair stringIntPair = new Pair("Hello", 42);                       // Pair can hold different types of values
String myString = (String) stringIntPair.getFirst();              // Casting required, can lead to runtime errors
int myInt = (Integer) stringIntPair.getSecond();                  // Casting required, can lead to runtime errors

// Why Generics Are Needed:
// - The current implementation lacks compile-time type safety. This means incorrect assignments or casts 
//   will only be detected at runtime, potentially leading to ClassCastException.
// - Generics allow us to define the types of 'first' and 'second' when creating a Pair object, 
//   providing compile-time type checking and eliminating the need for explicit casting.


```

## Generic class

```java
class GenericDemo<T,U>{
  private T first;
  private U second;

  //Getter and Setter
}

GenericDemo<String,Integer> gd=new GenericDemo<>("Hii",5);

String str=gd.getFirstO();   // No casting needed

// Using Generics in this way provides compile-time checking and avoids need for explicit casting.

```
