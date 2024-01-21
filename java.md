# Java

## Introduction

### Types of Programming Language:

- `Procedural`
- `Functional`
- `Object Oriented`

*or*

- `Static`
    - Perform type checking and shows error at compile time
    - Declare data type before using it
- `Dynamic`
    - Perform type checking at runtime and might not show error till runtime.
    - No need to declare datatype of variables

### Object and Reference Variables

![Untitled](res/obj_ref.png)

### Garbage Collection:

When system removes all the objects from memory which don’t have any reference-variable pointing to them.

### How Java code executes:

![Untitled](res/java_exec.png)

Platform independent: Java is an independent language, while C/C++ are not cause C/C++ compiler generates .exe file which is machine code whereas, Java compiler converts it into .class (byte code) which is later converted to machine code using JVM (which is platform dependent)

### Architecture of Java:

![Untitled](res/java_arc.png)

- JDK (Java Development Kit): Provides environment to develop and run Java program.
    
    Consists of:
    
    1. development Tools: to develop java program
    2. JRE: to execute java program
    3. compiler: javac: converts .java to .class
    4. archiver: jar
    5. docs generator: javadoc
    6. interpreter/loader
- JRE (Java Runtime Environment): Package that provides environment to only run the program.
    
    Consists of:
    
    1. deployment technologies
    2. ui toolkits
    3. integration libraries
    4. base libraries
    5. JVM: executes the code line by line
    
    Working:
    
    1. after we get the .class file, class loader loads all the classes that are needed
    2. JVM sends code to Byte code verifier to check the  format of the code

## Concepts:

1. `Data types`: 
    - Primitive data type: Data types that are predefined by the language and store simple values like number, char, boolean, and always have a value.
    - Non-Primitive data type: Data types created by programmer or Java to store complex values like String, Integer, Array, Interfaces, and can be null
2. `Access Modifiers`:
    - default: accessible in same package, use for variables that you don't want to use outisde the package
    - public: accessible everywhere
    - private: accessible only in that class, for sensitive data, use public getter and setter methods to access and modify
    - protected: accessible only in subclass

    |type|class|package|sublass|global|
    |-|-|-|-|-|
    |public|+|+|+|+|+|||
    |protected|+|+|+|||||
    |default|+|+||||||
    |private|+|||||||
3. `Packages`: Folders inside folders inside folders.
    - User Defined:
    - In-built:
        - java.lang: 
        - java.io: file reading/writing
        - java.util: data structures, collections framework
        - java.applet: 
        - java.awt: gui
        - java.net: networking
    
## Keywords:

- `new`: dynamically allocates memory and returns a reference to it
- `this`: ****
- `final`: 
- `static`: When a member is declared static, it can be accessed before any of the object of class is created, and without having reference of any its object.
    1. we can not call non-static functions from a static function, because it requires an instance.
    2. But we can call it referencing their instance in static context. 
    ```java
        class Main {
        	static void fun(){
        		// would show error (a)
        		greeting() 
        		// woulf work (b)
        		Main obj = new Main();
        		obj.greeting()
        	}
        
        	void greeting(){}
        }
    ```
- `super`: refers to super (parent) objects, it is used to call superclass methods and to access superclass constructor. By default it points to Object class.
        

## Object Oriented Programming:

- `Class`: User-defined template or prototype, which represents the set of properties and method functions.
    <br>
    - **Types of class**
        - `Singleton Class`: When only one instance of class can exist<br>
            ```java
            public class Singleton {
            private Singleton() {}
                
            public static Singleton instance;
            public static Singleton getInstance(){
                if(instance==null)
                    instance = new Singleton();
                return instance;
                }
            }
            ```
        - `Abstract Class`: 
            ```java
            public class java()
            ```
- `Objects`: Instance of class
- `Inheritance`: When one object inherit aka acquire all the properties and behaviours of parent object.
   - Types of inheritance
        1. Single Level: One class extends another class. A-> B
        2. Multilevel: Multiple level of single inheritance. A-> B-> C
        3. Multiple (!java): One class extends more than one class. A-> C <-B (`Alternative: Interfaces`)
        4. Hierarchial: One class is inherited by many classes. A-> B, A-> C, A-> D
        5. Hybrid (!java): Combination of single and multiple inheritance.
            A-> B, B-> C <-D, D <-A
- `Polymorphism`: 
    - Types of polymorphism
        1. Compile Time/Static: Achieved by method overloading and operator loading (not provided in Java)
        2. Runtime/Dynamic: Achieved by method overriding.
    - Lamguages which don't support polymorphism are know as Object-based programming language instead of Object-oriented programming language.
- `Encapsulation`: Wrapping up the implementation of the data members and methods in class.
- `Abstraction`: Hiding unnecessary details and showing only valuable information.