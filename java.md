# Java

<!-- vscode-markdown-toc -->
* [Introduction](#Introduction)
	* [Types of Programming Language](#TypesofProgrammingLanguage)
	* [Object and Reference Variables](#ObjectandReferenceVariables)
	* [Garbage Collection](#GarbageCollection)
	* [How Java code executes](#HowJavacodeexecutes)
	* [Architecture of Java](#ArchitectureofJava)
* [Topics](#Topics)
	* [Data types](#Datatypes)
	* [Access Modifiers](#AccessModifiers)
	* [Packages](#Packages)
	* [Object Cloning](#ObjectCloning)
* [Keywords](#Keywords)
* [Object Oriented Programming](#ObjectOrientedProgramming)
* [Interface](#Interface)

<!-- vscode-markdown-toc-config
	numbering=false
	autoSave=true
	/vscode-markdown-toc-config -->
<!-- /vscode-markdown-toc -->

## <a name='Introduction'></a>Introduction

### <a name='TypesofProgrammingLanguage'></a>Types of Programming Language

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

### <a name='ObjectandReferenceVariables'></a>Object and Reference Variables

![Untitled](res/obj_ref.png)

### <a name='GarbageCollection'></a>Garbage Collection

When system removes all the objects from memory which don’t have any reference-variable pointing to them.

### <a name='HowJavacodeexecutes'></a>How Java code executes

![Untitled](res/java_exec.png)

Platform independent: Java is an independent language, while C/C++ are not cause C/C++ compiler generates .exe file which is machine code whereas, Java compiler converts it into .class (byte code) which is later converted to machine code using JVM (which is platform dependent)

### <a name='ArchitectureofJava'></a>Architecture of Java

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

## <a name='Topics'></a>Topics

### <a name='Datatypes'></a>Data types

- `Primitive data type`: Data types that are predefined by the language and store simple values like number, char, boolean, and always have a value.
- `Non-Primitive data type`: Data types created by programmer or Java to store complex values like String, Integer, Array, Interfaces, and can be null

### <a name='AccessModifiers'></a>Access Modifiers
- `default`: accessible in same package, use for variables that you don't want to use outisde the package
- `public`: accessible everywhere
- `private`: accessible only in that class, for sensitive data, use public getter and setter methods to access and modify
- `protected`: accessible only in subclass

|type|class|package|sublass|global|
|-|-|-|-|-|
|public|+|+|+|+|+|||
|protected|+|+|+|||||
|default|+|+||||||
|private|+|||||||

### <a name='Packages'></a>Packages
Folders inside folders inside folders.
- User Defined:
- In-built:
    - java.lang: 
    - java.io: file reading/writing
    - java.util: data structures, collections framework
    - java.applet: 
    - java.awt: gui
    - java.net: networking

### <a name='ObjectCloning'></a>Object Cloning

- `Shallow copy`: Primitive Data types would be copied as it is, and non-primitive data types are not exactly copied but reference variables points to the same object.
- `Deep copy`: Both data types would be copied as it is.
    
## <a name='Keywords'></a>Keywords

- `new`: dynamically allocates memory and returns a reference to it
- `this`: ****
- `final`: non-access modifier used to make classes, methods, attributes non-changeable, impossible to inherit or override. Useful when you want a variable to always store the same value.
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
        

## <a name='ObjectOrientedProgramming'></a>Object Oriented Programming

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
            -   Classes whose objects can't be created, hence need to be inherited from other classes to be used.
            -   Can contain **Abstract methods**, methods which does not have a body, where body is provided by the subclass and also **regular methods** which have a body. 
            -   Can have constructor and static methods, and also final methods which will force the sublass not to change the body of the method.
        ```java
            public abstract class Car(){
                public abstract void company()
                public void price(){

                }
            }
        ```
- `Objects`: Instance of class
- `Inheritance`: When one object inherit aka acquire all the properties and behaviours of parent object.
   - Types of inheritance
        1. Single Level: One class extends another class. A-> B
        2. Multilevel: Multiple level of single inheritance. A-> B-> C
        3. Multiple (!java): One class extends more than one class. A-> C <-B (**Alternative: [Interfaces](#interface)**)
        4. Hierarchial: One class is inherited by many classes. A-> B, A-> C, A-> D
        5. Hybrid (!java): Combination of single and multiple inheritance.
            A-> B, B-> C <-D, D <-A
- `Polymorphism`: 
    - Types of polymorphism
        1. Compile Time/Static: Achieved by method overloading and operator loading (not provided in Java)
        2. Runtime/Dynamic: Achieved by method overriding.
    - Lamguages which don't support polymorphism are know as Object-based programming language instead of Object-oriented programming language.
- `Encapsulation`: Wrapping up the implementation of the data members and methods in class.
- `Abstraction`: Hiding implementation details and showing only functionality to the user.
    Ways to achieve abstraction:
    1. Abstract class (0 to 100%)
    2. Interface (100%)

## <a name='Interface'></a>Interface
Interface is a mechanism to achieve abstraction and multiple inheritance in Java.<br>
**An interface is a blueprint for a class that defines a set of abstract methods and properties that must be implemented by any class that implements the interface**
- Contains only abstract methods, variables are final and static, as we can't create object of Interface, hence can't intialize them using constructors.
- Class can implement multiple interfaces but can only extend one Abstract class.

```java
public interface Engine{
    abstract void start();
    //by default methods are abstract in interfaces
    void stop();
    //static methods should always have a body, as they can't be inherited or overridden
    static void name(){
        System.out.print("CarName");
    }
}

public class Car implements Engine{
    @Override
    public void stop(){}
    @Override
    public void start(){}
    public static void main(String[] args){
        Engine.name();
    }
    
}
```