### Guide
- Click 🔝 Icons To Jump To Table of Contents
- Topic With ⭐ Icons are questions asked from me in Interviews, Click on it to jump to ***Interview Questions Section***
- Click 💉 before topics for detailed section of it.
  
## Table of Contents
- [Language](#language)
  - [Java](#java)
  - [Kotlin](#kotlin)
    - [Advantages Over Java](#advantages-over-java)
    - [Basics](#basics)
    - [Keywords](#keywords)
    - [Defaults](#defaults)
    - [Classes](#classes)
    - [Constructors](#constructors)
    - [Functions](#functions)
    - [Scope Functions](#scope-functions)
- [Android](#android)
  - [Android Platform Architecture](#android-platform-architecture)
  - [Definitons](#definitons)
  - [Android Manifest](#android-manifest)
  - [Anroid App Components](#anroid-app-components)
  - [Intents](#intents)
  - [Activities](#activities)
  - [Fragments](#fragments)
  - [Launch Modes](#launch-modes)
  - [Architecture Components](#architecture-components)
  - [Android Jetpack](#android-jetpack)
  - [Design Patterns](#design-patterns)
  - [Architectures](#architectures)
  - [MVVM](#mvvm)
  - [Brief](#brief)
    - [ViewModel](#viewmodel)
    - [LiveData](#livedata)
    - [Flow](#flow)
    - [Coroutines](#coroutines)
    - [Dependency Injection](#dependency-injection)
  - [Differences](#differences)
  - [Interview Questions](#interview-questions)
  - [Compose](#compose)
    - [Compose Navigation](#compose-navigation)
  - [References](#references)

# Language

## Java
- JDK : Java Development Toolkit
  - Compiler
  - Tools
  - JRE : Java Runtime Environment
    - JVM : Java Virtual Machine, Java, Kotlin, Scala are compiled to JVM Bytecode.
    - Libraries

---
---

## Kotlin

---
### Advantages Over Java
[🔝](#table-of-contents)
  - `Data Class`
  - `Extension Functions`
  - `KMM`
  - `Concise Code`
  - `Support for Null Safety`

### Basics
[🔝](#table-of-contents)
  - `?:` : *Elvis Operator*, for safe call, unwraps the value from Nullable 
  - `!!` : value will not be null, if null will cause runtime crash
  - `==` : check if values are equal or not
  - `===` : check if reference is equal or not
  - `init` : it is the initialiser block in Kotlin, it's executed once the primary constructor is instantiated.

### Keywords
[🔝](#table-of-contents)
  - `var` : variable value can be changed
  - `val` : variable value cannot be changed, sets at runtime
  - `cont val` : makes val compile time constant
  - `open` : make the class open for inheritance by other classes
  - `when` : substitute for the *switch case* of java
    ```kotlin
    when(a){
      1..10 -> println("Value Less Than 10")
      11..100 -> println("Value More Than 10")
    }
    ```
  - [⭐](#interview-questions)
    `lazy` : is as method or rather say lamba exppression, it's set on *val* only, the val *would be created at runtime only when it's required*, should be used for time-consuming intializations, so that code can be faster and efficient.
  - [⭐](#interview-questions)
    `lateinit` : used to declare the variable with a gurantee to initialize it before using, otherwise would throw exception, used with *var*. Use `isInitialized` to check if variable has been initialized.
  - [⭐](#interview-questions)
    `object` : used to create *Singleton*, ensure that only one instance of that class is created even if 2 threads try to create it, it's a *lazy* instance, hence will be created once the object is accessed, otherwise it won't even be created.
  - `companion object` : similar to *static* method in java, to access something by their class name without having the instance of class.

### Defaults
[🔝](#table-of-contents)
  - Constructor arguments are `val` unless explicitly set to `var`
  - Visibilty modifier of a variable is `public`, other visibility modifiers are - `public internal protected private`
  - Classes are `final`, making them non-inheritable, hence use `open` to make class's inheritance possible.

### Classes
[🔝](#table-of-contents)
  - [⭐](#interview-questions)
    `data classes` : used to store values, data. Generates equals(), hashCode(), copy(), toString() automatically, which can be overriden.
    ```kotlin
    data class User(val name, val string)
    ```
  - `enum classes` : used to model types that represent a finite set of distinct values
    ```kotlin
    enum class State {
      IDLE, RUNNING, FINISHED
      }
    val state = State.RUNNING
    ```
  - `sealed classes` : restricts the use of inheritance, a sealed class can only be subclassed from inside the same package where the sealed class is declared.

### Constructors
[🔝](#table-of-contents)
  - `Primary Constructor` : Type of constructor that is initialized in the class header, after the class name with *constructor* keyword. Parameters are optional. If no annotations are provided, it can be skipped and if required initialization code can be placed in seperate initializer block i.e. `init`, because primary constuctor cannot contain any code.
  ```kotlin
  class Sample constructor(val a: Int){

    init {

    }
  }
  ```
  - `Secondary Constructor` : It allows for the initialization of variables as well as addition of logic to the class.
  ```kotlin
  class Sample{
    constructor(a: Int){
      println(a)
    }
  }
  ```
### Functions
[🔝](#table-of-contents)

What is `Lambda Expression` (LE) ? : Lambda expression is nothing but simplified representation of function, which can be passed as parameter, stored in a variable, even returned as a value.

```kotlin
val lambda: (Int, Int) -> Unit = { param1: Int, param2: Int -> param1+param2 }
val sum: (Int, Int) -> Int = {a: Int, b: Int -> a+b}
```

- `Higher Order Functions` : Functions the either takes function/LE as parameter, or returns a function/LE

```kotlin
fun passItFunction(paramFunction: () -> Unit){
  paramFunction()
}

fun addBothValue(a: Int,b: Int){
  return a+b  
}
```

- [⭐](#interview-questions)
  `Extension Functions` : When you want to add some method or functionalities to an existing class without inheriting it.

```kotlin
fun View.hide() {
  this.visibility = View.INVISIBLE
}
appbar.hide()
```

- `Infix Function` :
- `Inline Function` : When a function is made *inline* function, compiler will treat the function code as direct code in the calling function instead of seperate function.
  
```kotlin
fun main(){
  printMessage()
}

inline fun printMessage(){
  println("Hehe")
}

Becomes ->
fun main(){
  println("Hehe")
}
```

### Scope Functions
[🔝](#table-of-contents)[⭐](#interview-questions)

Functions whose sole purpose is to execute a block of code within the context of an object. When called with a lambda expression provided, a temporary scope is formed, inside which we can access the object without its name.
  |       |Context|Return |Use Case|
  |---    |---    |---    |---        |
  |`let`  |it     |lambda |Null Safety Calls|
  |`with` |this   |lambda |Grouping Function calls on an object|
  |`run`  |this   |lambda |Object Configuration and computing the result|
  |`apply`|this   |context|Object Configuration|
  |`also` |it     |context|Addtional Effects|

---
---

# Android

## Android Platform Architecture
[🔝](#table-of-contents)
- `Linux Kernel` : Core of android platform architecture. Manages all the hardware drivers, low-level memory.
- `Hardware Abstraction Layout (HAL)` : Bridges hardware capabilities to the higher-level Java API Framework by defining standard interfaces.
- `Android Runtime (ART)` : Converts Dalvik Executable Format (DEX) bytecode into machine code that system can understand. Replaced Dalvik Virtual Machine for devices running Android 5.0 (Lollipop).
- `Native C/C++ Libraries` : Native APIs let you manage native activities and access physical device components like camera, sensor, graphic .
- `Java API Framework (Application Framework)` : Collection of Android Libraries written in Java and Kotlin. Ex: Android Jetpack
- `System Apps` : Pre-installed apps such as email, SMS messaging, calendars, contacts

## Definitons
[🔝](#table-of-contents)
- [⭐](#interview-questions)
  `Context` : It is the context of the current state of application/class. Used to get information regarding the activity and application. USed to access *Resources, Databases, SharedPreferences*
  - `Application Context` : Tied to lifecycle of an application, can be used to create singleton objects.
  - `Application Context` : Tied to lifecycle of an activity, should be used when passing the context in activity.
- [⭐](#interview-questions)
  `Application Class` : Base class within an Android app that contains all other components such as activities and services. It is instantiated before any other class when the process for your application is created.

## Android Manifest
[🔝](#table-of-contents)

Describes essential information about the application such as package name, entry points, components, permissions, and metadata.
- `Package Name` : Application's univerally unique application ID

## Anroid App Components
[🔝](#table-of-contents)[⭐](#interview-questions)

App components are like entry points that allow systems and users to interact with your application. Each component have their own function and lifecycle.
- `Activities` : Entry point for interacting with users, represents single single with UI
- `Services` : Entry point for keeping app running in background for all kinds of reason, like music player, youtube video player.
  - `startService()` : Allows other components to run a service in background or stop it, using *startService()* & *stopService()* respectively.
  - `bindService()` : Same as startService but also provides IBInder interface, which allows the client to communicate with the service consistently. Use *unbindService* to cancel the connection
- `Broadcast Receivers` : Registerable listener that listens to broadcast messages from Android system or other applications. Where Broadcasts are used to send messages across apps, outside of the normal user flow, like device starts charging. No lifecycle like Services and Activities.
- `Content Providers` : Manages shared set of data. Through content providers, apps can query or modify other app's data ***if they have required permissions.***

## Intents
[🔝](#table-of-contents)

An asynchronous message that activates 3 of the 4 android app components i.e. Activities, Services, Broadcast Receivers.
- `Explicit Intents` : Requires specified information, which targets an application's package name.
- `Implicit Intents` : Implicit Intents declares a general action to perform like showing gallery image, opening URL on web browser, you can use implicit intent to request action to the android system. Then android system shows all the appropiate components for that request if found.

## Activities
[🔝](#table-of-contents)
  - [Activity Lifecycle](https://developer.android.com/guide/components/activities/activity-lifecycle)
  - Q : When *onDestroy()* gets called directly without *onPause()* and *onStop()* ? 
    And : When we call ***finish()*** in *onCreate()*
  - `onSavedInstanceState()` : Used to store data before pausing the activity.
  - `onRestoreInstanceState()` : Used to recover the saved state of an activity during recreation, through *Bundles*.j

## Fragments
[🔝](#table-of-contents)

Reusable part of UI that interacts with users by providing UI elements on top of activities. Managed by Fragment Managers.
- [⭐](#interview-questions)[Fragment Lifecycle]()
- [⭐](#interview-questions)
  `add vs replace` : **replace** removes the existing fragment and adds a new fragment, means when you press back button the fragment that got replaced will be recreated with its *onCreateView()* being invoked, wheres **add** retains the existing fragments and adds a new fragments means existing fragment will be active, wont be in *paused* state.

## Launch Modes
[🔝](#table-of-contents)
- `Standard` : Default launch mode, creates new instance every time even if activity instance is already present
  ```
  A->B->C->D
  launch B1
  A->B->C->D->B(new instance)
  ```
- `Single Top` : If instance of same activity exists on top pass the extras data though *onNewIntent(Intent intent), otherwise creates a new instance.
  ```
  A->B->C->D
  launch D
  A->B->C->D(old instance gets extra data)
  launch C
  A->B->C->D->C(new instance of C)
  ```
- `Single Task` : Can only have one instance in the system (Singleton)
  ```
  A->B->C->D
  launch C
  A->B->C(old instance gets extra data) destroyed D
  ```
- `Single Instance` :
  ```
  A->B->C->D
  launch E
  A->B->C->D | E
  launch F from E
  E | A->B->C->D->F
  ```

## Architecture Components
[🔝](#table-of-contents)

Suite of libraries to solve fundamental Android problems and guide app architecture. It comes under Android Jetpack.
- `App Architecture` : Google's recommneded app achitecture below allows apps to scale, improve quality, robustness and makes apps easier to test.
  ```UI Layer``` -> ```Domain Layer``` -> ```Data Layer```    
  - `UI Layer` : Render the updated application data on screen. Also known as Presentation layer. Made of UI elements, and State holders, such as *ViewModel*
  - `Domain Layer` : Abstracting complex/simple business logic, converts complex data into suitable types for UI layers. **Optional**
  - `Data Layer` : Contains the *business logic*. Made of *repositories*, that can contain zero to many data sources.

## Android Jetpack
[🔝](#table-of-contents)
- `UI Layer Libraries`
  - `ViewBinding` : Generates a binding class for each XML layout file.
  - `DataBinding` : Generates a binding class for XML layouts that includes a **layout** tag. Linkd View and ViewModel with observer pattern, properties and event callbacks.
  - [💉](#viewmodel)
    `ViewModel` : It's a state holder to store and manage UI related data surviving configuration changes.
  - [💉](#livedata)
    `LiveData` : It's a lifecycle-aware data holder, which can be observed by multiple Observers, used to implement Observer Pattern.
  - `Lifecycle` : Jetpack's Lifecycle allows you to build independent components, which observes the lifecycle changes of lifecycle owners like activities or fragments.
- `Data Layer Libraries`
  - `DataStore` : Used to store lightweight key-value pairs in local storage, works with Coroutines and Flow to store data asynchonously. Can be used to replace SharedPreferences. 
  - `Room` : Abstraction layer over SQLite Databases simplyfying access of database.
  - `WorkManager` : Background Processing API, gurantees background work by scheduling works, runs deferrable.

## Design Patterns
[🔝](#table-of-contents)

Reusable solutions to solve repeated and common software problems in software engineering.

- `Dependency Injection` : When dependencies are provided to a class instead of creating them itself. Advantages of DI are **reduces boilerplate code, loose coupling between classes, hence easy testing, code reuability, code maintainability.**
  - `Hilt` : Compile time dependency injection tool which works on top of Dagger, reduces the boilerplate code compared to Dagger.
  - `Dagger` : Also compile time dependency injection tool based on *javax.inject* annotation.
  - `Koin` : Popular dependency injection tool for Kotlin projects.
<br><br>
- `Observer Pattern` : It is a behavioral design pattern that allows you to build a subscription mechanism to notify observers automatically of any state changes.
  - [💉](#livedata)
    `LiveData` : ***Lifecycle-aware, thread-safe and data-holder observer pattern.*** Bounds to lifecycle, so we don't need to unsubscribe observers manually, ***prevents memory leaks***, but with adoption of coroutines broadly, Kotlin Flows are more preferred now.
  - [💉](#flow)
    `Kotlin Flows` : Asynchronous solution that is cold streams similar to sequences working with Coroutines. They are asynchronous and non-blocking solutions.
  - `RxKotlin` : Originated from ReactiveX, which is combination of observer pattern, iterator pattern, functional programming.
  
- `Repository Pattern` :
  
## Architectures
[🔝](#table-of-contents)

Architecture defines boundaries between each layer, defines the responsibilities clearly affecting project's complexity, scalability and robustness, and makes it easier to test.
- [⭐](#interview-questions)
  `MVVM` : 
- `MVI` :
- `MVP` :
- `MVC` :
- `Clean Architecture` :

## MVVM
[🔝](#table-of-contents)
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

## Brief

### ViewModel
[🔝](#table-of-contents)

***ViewModel is class designed to hold and manage  UI-related data in a life-cycle consious way. This allows data to survive configuration changes such a screen rotations.***
- ViewModel exists from when you first request a ViewModel (usually `onCreate`) untill the activity is finished and destroyed.
- Extend `AndroidViewModel` if you need context inside viewModel, which will provide Application Context.
- `ViewModelProviders.of` method creates a new ViewModel instance when it's called first time, when it's called again, which happens whenever `onCreate` is called, it will return the pre-existing ViewModel associated with the specific Activity/Fragment. This preserves the data.
- Advantages :
  - Handle Configuration changes
  - Lifecycle Awareness
  - Data Sharing
  - Kotlin Coroutines Support
- [⭐](#interview-questions) `How ViewModels Work Internally` :
  
  Code to get the instance of `viewModel`
  ```kotlin
  viewModel = ViewModelProvider(this, ViewModelFactory()).get(SampleViewModel::class.java)
  ```
  We get the instance of `ViewModelProvider` by passing instance of the `Activity` and `ViewModelFactory`, then we are using that `ViewModelProvider` instance to get the `SampleViewModel` object.
  ```kotlin
  public open classViewModelProvider constructor(
    private val store: ViewModelStore,
    private val factory: Factory,
    private val defaultCreationExtras: CreationExtras = CreationExtras.Empty
    ) {
      ..
  }
  ```
  Where `ViewModelStore` looks like
  ```kotlin
  public class ViewModelStore {
    private final HashMap<String, ViewModel> mMap = new HashMap<>();
    final void put(String key, ViewModel vm) {..}
    final ViewModel get(String key) {..}
    ..
  }
  ```
  At the lowest, the object creation of `ViewModel` is handled by `ViewModelStore`, which contains `HashMap<String, ViewModel>` 
  
  where, Key Format : `val canonicalName = modelClass.canonocalName`.
  
  Hence `ViewModelStore` checks if key for `ViewModel` exists in the HashMap.
  - If yes, return the already existing object.
  - If no, create a new `ViewModel`, and store the object in HashMap for future usage.
  
### LiveData
[🔝](#table-of-contents)

### Flow
[🔝](#table-of-contents)

### Coroutines
[🔝](#table-of-contents)

***Coroutines are Kotlin feature that converts async background processes to the sequential code***
- `suspend` : Keyword to mark a function available to coroutines, *suspends* exceution until the result is ready then it resumes where it left off with the result. ***Using suspend doesn’t tell Kotlin to run a function on a background thread.***
- `Dispatchers` : Context
  - `Dispathcers.Main` : Lightweight tasks eg - network calls, database queries, won't block the main thread while suspended.
  - `Dispathcers.IO` : For heavy IO work, eg - long running database queries.
  - `Dispathcers.Default` : For CPU intensive tasks.
  - `Dispathcers.Unconfined` : Runs coroutines unconfined on no specific thread, not recommended to use. 
- `CoroutineScopes` : Keeps track of coroutines, even suspended ones, can cancel all of the coroutines started in it.
  - `globalScope` : Coroutine lifecycle will be associated with the application lifecycle.
  - `viewModelScope` : Coroutine scopre tied to *viewModel*. Extension function of the *viewModel* class, bound to *Dispatchers.Main* and will automatically be cancelled when viewModel is cleared.
  - `lifecycleScope` : 
- *Room* and *Retrofit* make suspending functions *main-safe*, it's safe to call these suspend functions from *Dispathers.Main*, even thought they fetch from network and write to database. Do not use ***Dispatchers.IO***.
- `Builders` : 
  - `runBlocking{}` : Runs a new coroutine and *blocks* the current thread until its completion.
  - `runCatching{}` :
  - `launch{}` : ***Launch is a bridge from regular functions into coroutines.*** Will start a new coroutine that is *fire and forget* - that means it won't return the result to the caller.
  Launches a new coroutine without blocking the current thread and returns a reference to the coroutine as a *Job*, which can be used to cancel the corutine.
  - `async{}` : Will start a new coroutine and it allows us to return a result with a suspended function called `await`. Hence, expects that we will eventually call `await` to get a result(or excecption) so it won't throw exceptions by default.
- `withContext{}` : Calls the specified suspending block with a given coroutine context, suspends until it completes, and returns the result. ***Can be used to switch between dispatchers/contexts of coroutine***
  ```kotlin
  withContext(Dispatcher.Main) {

  }
  ```
- `Structured Concurrency` : *A parent coroutine scope having children coroutine scopes*. It gurantees that when a suspend function returns, all of its work is done and also when a coroutine errors, its caller or scope is notified.
  ```kotlin
  suspend fun callTwoAPI(){
    coroutineScope{
      async { callAPI(1) }
      async { callAPI(2) }
    }
  }
  ```
  - `coroutineScope` : coroutineScope builder will suspend itself until all coroutines started inside of it are complete, hence there's no way to return from `callTwoAPI` until all coroutines are completed.
  ***Cancels whenever any of the children coroutine fails*** meaning if one network request fails, all of the others request would be cancelled immediately.
  - `supervisorScope` : supervisorScope builder won't cancel children when one them fails.
  
- [⭐](#interview-questions)
  `Difference between Threads & Coroutines` : Threads are expensive, require context switches which are costly, and number of threads that can be launched is limited by the underlying operating system whereas, Coroutines can be thought of as light-weight threads, means the creating of coroutines doesn't allocate new thread, instead they use predefined thread pools and smart scheduling for the purpose of which task to execute next and which tasks later.

### Dependency Injection

## Differences
- `ListView vs RecyclerView`

## Interview Questions
- `ListView vs RecyclerView`
- `LiveData vs Flow`
- `lazy vs lateinit`
- `add() vs replace()`
- `Are object variables thread safe`
- `Inner working of ViewModel`
- `Inner working of Extension Functions`
- `Context and Types of context`

## Compose

- StateFlow.collectAsState() - Shows the latest value of the StateFlow, updates the composable when a item is updated
  ```kotlin
  viewmodel.destinations.collectAsState()
  ```
- Side-Effect - Side-Effect in compose is a change to the state of the app that happens outside the scope of composable function.
- LaunchedEffect - To call suspend function safely from inside a composable, triggers a coroutine-scoped side-effect in Compose.
- rememberCoroutineScope() - To call suspend function from composables, automatically gets cancelled once it leaves the composition.

### Compose Navigation
- Steps
  - Declare NavController at the top level of composable hierarchy
  
    ```kotlin
    val navController = rememberNavController()
    ```

## References
- https://medium.com/androiddevelopers/viewmodels-a-simple-example-ed5ac416317e
- https://blog.mindorks.com/android-viewmodels-under-the-hood
- https://medium.com/androiddevelopers/coroutines-on-android-part-i-getting-the-background-3e0e54d20bb
- https://medium.com/androiddevelopers/coroutines-on-android-part-ii-getting-started-3bff117176dd
- https://medium.com/androiddevelopers/coroutines-on-android-part-iii-real-work-2ba8a2ec2f45