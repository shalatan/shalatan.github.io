## Table of Content
- [Language](#language)
  * [Java](#java)
    + [Constructors](#constructors)
  * [Kotlin](#kotlin)
    + [Advantages Over Java](#advantages-over-java)
    + [Basics](#basics)
    + [Keywords](#keywords)
    + [Defaults](#defaults)
    + [Classes](#classes)
    + [Constructors](#constructors-1)
    + [Functions](#functions)
    + [Scope Functions](#scope-functions)
- [Android](#android)
  * [Architectures](#architectures)
    + [MVVM](#mvvm)
  * [Compose](#compose)
    + [Compose Navigation](#compose-navigation)
- [Misc](#misc)
  * [Git](#git)
  * [Heroku](#heroku)

# Language

## Java
- JDK : Java Development Toolkit
  - Compiler
  - Tools
  - JRE : Java Runtime Environment
    - JVM : Java Virtual Machine, Java, Kotlin, Scala are compiled to JVM Bytecode.
    - Libraries
### Constructors
  - 

---
## Kotlin
### Advantages Over Java
  - `Data Class`
  - `Extension Functions`
  - `KMM`
  - `Concise Code`
  - `Support for Null Safety`

### Basics
  - `var` : variable value can be changed
  - `val` : variable value cannot be changed, sets at runtime
  - `cont val` : makes val compile time constant
  - `?:` : *Elvis Operator*, for safe call, unwraps the value from Nullable 
  - `!!` : value will not be null, if null will cause runtime crash
  - `==` : check if values are equal or not
  - `===` : check if reference is equal or not
  - `init` : it is the initialiser block in Kotlin, it's executed once the primary constructor is instantiated.

### Keywords
  - `open` : make the class open for inheritance by other classes
  - `when` : substitute for the *switch case* of java
    ```
    when(a){
      1..10 -> println("Value Less Than 10")
      11..100 -> println("Value More Than 10")
    }
    ```
  - `lazy` : is as method or rather say lamba exppression, it's set on *val* only, the val *would be created at runtime only when it's required*, should be used for time-consuming intializations, so that code can be faster and efficient.
  - `lateinit` : used to declare the variable with a gurantee to initialize it before using, otherwise would throw exception, used with *var*. Use `isInitialized` to check if variable has been initialized.
  - `object` : used to create *Singleton*, ensure that only one instance of that class is created even if 2 threads try to create it, it's a *lazy* instance, hence will be created once the object is accessed, otherwise it won't even be created.
  - `companion object` : similar to *static* method in java, to access something by their class name without having the instance of class.

### Defaults

  - Constructor arguments are `val` unless explicitly set to `var`
  - Visibilty modifier of a variable is `public`, other visibility modifiers are - `public internal protected private`
  - Classes are `final`, making them non-inheritable, hence use `open` to make class's inheritance possible.

### Classes

  - `data classes` : used to store values, data. Generates equals(), hashCode(), copy(), toString() automatically, which can be overriden.
    ```
    data class User(val name, val string)
    ```
  - `enum classes` : used to model types that represent a finite set of distinct values
    ```
    enum class State {
      IDLE, RUNNING, FINISHED
      }
    val state = State.RUNNING
    ```
  - `sealed classes` : restricts the use of inheritance, a sealed class can only be subclassed from inside the same package where the sealed class is declared.

### Constructors

  - `Primary Constructor` : Type of constructor that is initialized in the class header, after the class name with *constructor* keyword. Parameters are optional. If no annotations are provided, it can be skipped and if required initialization code can be placed in seperate initializer block i.e. `init`, because primary constuctor cannot contain any code.
  ```
  class Sample constructor(val a: Int){

    init {

    }
  }
  ```
  - `Secondary Constructor` : It allows for the initialization of variables as well as addition of logic to the class.
  ```
  class Sample{
    constructor(a: Int){
      println(a)
    }
  }
  ```
### Functions
What is `Lambda Expression` (LE) ? : Lambda expression is nothing but simplified representation of function, which can be passed as parameter, stored in a variable, even returned as a value.
```
val lambda: (Int, Int) -> Unit = { param1: Int, param2: Int -> param1+param2 }
val sum: (Int, Int) -> Int = {a: Int, b: Int -> a+b}
```
- `Higher Order Functions` : Functions the either takes function/LE as parameter, or returns a function/LE
```
// takes a function as parameter
fun passItFunction(paramFunction: () -> Unit){
  paramFunction()
}
// returns a function
fun addBothValue(a: Int,b: Int){
  return a+b
}
```
- `Extension Functions` : When you want to add some method or functionalities to an existing class without inheriting it.
```
fun View.hide() {
  this.visibility = View.INVISIBLE
}
//to call it
appbar.hide()
```
- `Infix Function` :
- `Inline Function` : When a function is made *inline* function, compiler will treat the function code as direct code in the calling function instead of seperate function.
```
fun main(){
  printMessage()
}

inline fun printMessage(){
  println("Hehe")
}

// will become
fun main(){
  println("Hehe")
}
```

### Scope Functions

Functions whose sole purpose is to execute a block of code within the context of an object. When called with a lambda expression provided, a temporary scope is formed, inside which we can access the object without its name.
  |       |Context|Return |Use Case|
  |---    |---    |---    |---        |
  |`let`  |it     |lambda |Null Safety Calls|
  |`with` |this   |lambda |Grouping Function calls on an object|
  |`run`  |this   |lambda |Object Configuration and computing the result|
  |`apply`|this   |context|Object Configuration|
  |`also` |it     |context|Addtional Effects|

# Android

## Architectures
---
### MVVM
- Model-View-ViewModel
- ViewModel
  - Object that provides data for UI Components and survive configuration changes.
  - Is Lifecycle Aware, knows the current callback state of attached view
  - *ViewModel Provider* provides the new instance of ViewModel if old instance doesn't exists, otherwise returns the previous instance.
  - Outlives the lifecycle of associated view.
- Advantages
  - Introduced to handle memory leaks, and lifecycle changes.
  - Surives the orientation changes
  - Adding savedStateHandled can add support when the View is killed by OS.

  ||ViewModel|onSaveInstanceState|
  |---|---|---|
  |Config Changes|Survices|Survives + Process Death
  |Data Capacity|Lots of data|Small
  |What to Store?|All data for view|Data to reload view in emergency

## Compose
---
- StateFlow.collectAsState() - Shows the latest value of the StateFlow, updates the composable when a item is updated

  ```viewmodel.destinations.collectAsState()```
- Side-Effect - Side-Effect in compose is a change to the state of the app that happens outside the scope of composable function.
- LaunchedEffect - To call suspend function safely from inside a composable, triggers a coroutine-scoped side-effect in Compose.
- rememberCoroutineScope() - To call suspend function from composables, automatically gets cancelled once it leaves the composition.

### Compose Navigation
- Steps
  - Declare NavController at the top level of composable hierarchy
  
    ```val navController = rememberNavController()```

# Misc

## Git
---
- Git Commands
  - `git init` : initialize a empty git
  - `git status` : shows all the changed files
  - `git add .` : add all the files/changed files
  - `git commit -m "message"` : commit the changes with message

## Heroku
---
- Heroku CLI Commands
  - `heroku login`
  - `heroku create` : create a new app
  - `git add .` -> `git commit -m "message"` -> `git push heroku master` : deploy the latest code
  - `heroku open` : open the app
  - `heroku logs` --tail : get logs