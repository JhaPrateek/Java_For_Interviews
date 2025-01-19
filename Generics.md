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

-> Character standard
    T for Type
    E for Element
    L for Key
    N for Number
    V for Value

Note -These are not mandatory to use. We can use any character


## Generic method

-> Generic methods are methods that introduce their own type parameters, independent of any generic type parameters declared in their enclosing class. These parameters are specified within angle brackets <T> before the return type of the method.

```java

public class GenericMethodExample {
    public static <T> void swap(T[] array, int i, int j) {
        T temp = array[i];
        array[i] = array[j];
        array[j] = temp;
    }

    public static void main(String[] args) {
        Integer[] numbers = {1, 2, 3, 4};
        swap(numbers, 1, 3);
        System.out.println(Arrays.toString(numbers)); // Output: [1, 4, 3, 2]
    }
}

```

-> Key Features
    Type Safety: The compiler ensures type safety, reducing runtime errors.
    Flexibility: Operates on various types without rewriting the method.
    Independent of Class: Generic methods can exist in both generic and non-generic classes.

## Collections Without Generics

-> Collections can be created without using generics.
-> This allows adding elements of any type but requires explicit casting during retrieval, which is error-prone and may cause runtime exceptions.

```java
ArrayList list = new ArrayList(); // No generics used
list.add("Hello"); // Adding a String
list.add(123);     // Adding an Integer
list.add(true);    // Adding a Boolean

// Retrieval requires explicit casting
String greeting = (String) list.get(0); // Valid cast
int number = (int) list.get(1);         // Valid cast
boolean flag = (boolean) list.get(2);   // Valid cast

```
-> Using raw collections (without generics) increases the risk of runtime errors due to incorrect type casting.

## Collections With Generics

-> By specifying a type parameter (e.g., <String>), we enforce type safety.
-> Only elements of the specified type can be added, avoiding runtime errors and removing the need for explicit casting during retrieval.

```java
ArrayList<String> list = new ArrayList<>(); // Generics used with type String
list.add("Hello"); // Adding a String
// list.add(123);     // Compilation error: Only Strings are allowed
// list.add(true);    // Compilation error: Only Strings are allowed

// Retrieval without casting
String greeting = list.get(0); // Type-safe retrieval

```
-> Using generics ensures compile-time type safety, reducing errors and improving code readability.

## Covariance

-> Covariance allows assigning a child type reference to a parent type reference.
-> For arrays, this rule is supported because Developer[] or Manager[] (subtypes) can be assigned to Employee[] (supertype).
-> Covariance works with arrays because the compiler recognizes Developer[] as a subtype of Employee[].

```java
public static void process(Employee[] employees) {
    // Some logic
}

// Example
Developer[] devs = new Developer[10];
process(devs); // Covariance allows this
```

```java
String[] strArray = {"Generics", "Collections"};
Object[] objArray = strArray; // Valid due to covariance
```

-> Covariance with collection
```java
List<String> listStr = new ArrayList<>();
List<Object> listObj = listStr; // Compilation error: Collections do not support covariance
```

->Generic collections like List<Employee> cannot accept List<Developer> as they are considered different types.
```java
public static void process(List<Employee> employees) {
    // Some logic
}

// Example
List<Developer> devs = new ArrayList<>();
process(devs); // Compilation error: Invariant generic type

```

### Note -> Why covariance not supported by collections

    The decision to make arrays covariant in Java was a deliberate design choice, providing a significant degree of polymorphic behavior. This design allowed the storage of various business objects inside an "Object[]" array, enabling the creation of generic code. However, this choice introduced the potential for bugs that could only be identified at runtime. 

```java
    Number[] numArray={1,2,3};
    Object[] objArray=numArray;
    objArray[0]="Hello";    // Compilation will be fine but at runtime ArrayStoreException will be throwed
```

## Subtype or Upper Bound Wildcards

-> < ? extends T > means a type that is either T or a child of T, where T is the type used as the generics of a collection.
-> The wildcard ? extends T represents an unknown type that is either T or a subtype of T. This is often referred to as an upper-bounded wildcard.
-> We can call this method with an ArrayList<Employee> or an array list of a subtype, such as ArrayList<Developer>.

```java
public class Main {
    public static void printEmployeeNames(ArrayList<? extends Employee> employees) {
        for (Employee e : employees) {
            System.out.println(e.getName());
        }
    }

    public static void main(String[] args) {
        ArrayList<Developer> developers = new ArrayList<>();
        developers.add(new Developer("Alice"));
        developers.add(new Developer("Bob"));

        printEmployeeNames(developers); // Prints names of developers
    }
}
```

-> We cannot add a new element/object inside the collection when using Subtype or Upper Bound Wildcards. For example, in the above method, you cannot add an object of Employee or its subtypes. This is because the wildcard ? extends Employee could refer to any subclass, making it impossible to determine the specific type and potentially leading to a compilation error.

## Supertype or Lower Bound Wildcards

-> The lower-bounded wildcard (? super T) is used in Java generics to restrict a type parameter to a specific type (T) or any of its supertypes. This is useful when you need to add elements of type T or its subtypes to a collection but don't need to read specific types from the collection.

```java
public class Main {
    public static void addNumbers(List<? super Integer> list) {
        for (int i = 1; i <= 10; i++) {
            list.add(i); // Adding Integers is safe
        }
    }

    public static void main(String[] args) {
        List<Number> numbers = new ArrayList<>();
        addNumbers(numbers); // Works because Number is a supertype of Integer

        List<Object> objects = new ArrayList<>();
        addNumbers(objects); // Works because Object is a supertype of Integer

        // List<Double> doubles = new ArrayList<>();
        // addNumbers(doubles); // Compilation error: Double is not a supertype of Integer
    }
}
```
-> Contravariance:
    Contravariance is the opposite of covariance:
    Covariance (? extends T) allows reading elements but restricts writing to ensure type safety.
    Contravariance (? super T) allows writing elements but restricts reading to maintain type safety.
    It enables a method or collection to work with more generic types (i.e., supertypes of a given type).

-> Restriction: You can either specify an upper bound (? extends T) or a lower bound (? super T), but not both simultaneously.

## Unbounded Wildcards

