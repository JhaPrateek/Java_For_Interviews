# JVM, JRE, and JDK

Java is a platform-independent and object-oriented language. Its main advantage is portability (WORA - Write Once, Run Anywhere). Java achieves portability through the Java Virtual Machine (JVM).

## Structure

- Inside JDK, we have JRE, and inside JRE, we have JVM.

## Program Flow

JAVA PROGRAM --> compiler --> BYTE CODE --> JVM --> MACHINE CODE --> CPU --> OUTPUT


1. **Java Program**: We write the source code in a `.java` file using the Java programming language.
2. **Compiler**: The `javac` compiler translates the source code into an intermediate language called Bytecode, which is stored in a `.class` file.
3. **Bytecode**: A platform-independent representation of your program, optimized for execution by the JVM.
4. **JVM (Java Virtual Machine)**: The JVM reads the bytecode and translates it into machine code specific to the operating system and hardware.
5. **Machine Code**: This is the low-level binary code that the CPU can directly execute.
6. **CPU**: Executes the machine code instructions to perform the program's tasks.
7. **Output**: The final result or effect of the program, such as printing to the console, calculations, or other operations.

### Note
- The Java Compiler ensures portability by converting source code into bytecode, which can run on any JVM regardless of platform.
- The JVM acts as an interpreter or JIT (Just-In-Time) compiler, translating bytecode into platform-specific machine code.
- Java is compiled into bytecode and then interpreted or JIT-compiled into machine code at runtime, making it a hybrid language.

## JVM

- The JVM is an abstract machine, meaning it doesn't exist physically.
- JVM is platform-dependent.
- JVM has a JIT (Just-In-Time) compiler that converts bytecode into machine code.

## JRE

- JRE is JVM + class libraries.
- JRE contains JVM and class libraries (The class library refers to a collection of pre-written classes, methods, and packages that provide essential functionality to Java programs. Examples: `java.lang.Object`, `java.lang.String`, `java.util.ArrayList`, `java.util.HashMap`).
- With JRE, we can run any Java program, but we cannot code the program because the coding part comes under the JDK (Java Development Kit). The JDK provides all the tools needed to write, compile, and debug Java programs.

## JDK

- JDK is JRE + programming language information + compiler + debugger, etc.
- The Java Development Kit (JDK) is a software development environment used for creating Java applications and applets. It provides all the tools and resources required to write, compile, debug, and execute Java programs.

### Note
- JVM, JRE, and JDK are all platform-dependent.
- Bytecode is platform-independent.

### Why 1 public class in Java
- The one public class per file rule in Java exists to maintain a clear 1:1 mapping between file names and public classes, making code organization predictable and class loading efficient. The file name must match its public class name, so Java knows exactly where to find each class. 

## Class loaders

- A class loader in Java is a part of the Java Virtual Machine (JVM) responsible for loading Java classes into the memory at runtime. The purpose of the class loader is to dynamically find and load .class files into memory, allowing Java programs to execute.
- Types : 1) Bootstrap class loader
          2) Extension class loader
          3) Application class loader
## Java Editions

- **JSE**: Java Standard Edition
- **JEE**: Java/Jakarta Enterprise Edition (Used to build large applications)
- **JME**: Java Micro/Mobile Edition

### Additional Information
- JSE is the core Java.
- JEE is JSE + JSP + Transaction API + Persistence API.
- JME is the API for mobile application development.
