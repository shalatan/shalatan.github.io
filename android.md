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
  - [Anroid App Components](#anroid-app-components)
  - [Intents](#intents)
  - [Launch Modes](#launch-modes)
  - [Architecture Components](#architecture-components)
  - [Android Jetpack](#android-jetpack)
  - [Design Patterns](#design-patterns)
  - [Architectures](#architectures)
    - [MVC](#mvc)
    - [MVP](#mvp)
    - [MVVM](#mvvm)
    - [MVI](#mvi)
    - [Clean Architecture](#clean-architecture)
  - [Brief](#brief)
    - [Services](#services)
    - [Activities](#activities)
    - [Fragments](#fragments)
    - [ViewModel](#viewmodel)
    - [LiveData](#livedata)
    - [Flow](#flow)
    - [Coroutines](#coroutines)
    - [Dependency Injection](#dependency-injection)
      - [Hilt](#hilt)
    - [RecyclerView](#recyclerview)
    - [WorkManager](#workmanager)
    - [Notification](#notification)
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
<br><br>

## Kotlin

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
  - [⭐](#interview-questions)
    Q: Are `Object` declarations thread safe, even if two threads tries to create it at same time?
    A: Yes, **object** is thread safe by construction. As it's just final class with static instance initializations, when decompiled. [ref](https://stackoverflow.com/a/30190567)
  - `companion object` : similar to *static* method in java, to access  something by their class name without having the instance of class.

### Defaults
[🔝](#table-of-contents)

  - Constructor arguments are `val` unless explicitly set to `var`
  - Visibilty modifier of a variable is `public`, other visibility    modifiers are - `public internal protected private`
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
  `Extension Functions` : When you pick up a receiver class, and dynamically inject a member function into the class which acts pretty much same as regulary defined member functions of that class.

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
<br><br>

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
  `Context` : It is the context of the current state of application/class. Used to get information regarding the activity and application. Used to access *Resources, Databases, SharedPreferences*
  - `Application Context` : Tied to lifecycle of an application, can be used to create singleton objects.
  - `Application Context` : Tied to lifecycle of an activity, should be used when passing the context in activity.
- [⭐](#interview-questions)
  `Application Class` : Base class within an Android app that contains all other components such as activities and services. It is instantiated before any other class when the process for your application is created.
- `Android Manifest` : Describes essential information about the application such as package name, entry points, components, permissions, and metadata.
  - `Package Name` : Application's univerally unique application ID

## Anroid App Components
[🔝](#table-of-contents)[⭐](#interview-questions)

App components are like entry points that allow systems and users to interact with your application. Each component have their own function and lifecycle.
- [💉](#activities)`Activities` : Entry point for interacting with users, represents single screen with UI
- [💉](#services)`Services` : Entry point for keeping app running in background for all kinds of reason, like music player, youtube video player.
  - `startService()` : Allows other components to run a service in background or stop it, using *startService()* & *stopService()* respectively.
  - `bindService()` : Same as startService but also provides IBInder interface, which allows the client to communicate with the service consistently. Use *unbindService* to cancel the connection
- `Broadcast Receivers` : Registerable listener that listens to broadcast messages from Android system or other applications. Where Broadcasts are used to send messages across apps, outside of the normal user flow, like device starts charging. No lifecycle like Services and Activities.
- `Content Providers` : Manages shared set of data. Through content providers, apps can query or modify other app's data ***if they have required permissions.***

## Intents
[🔝](#table-of-contents)

An asynchronous message that activates 3 of the 4 android app components i.e. Activities, Services, Broadcast Receivers.
- `Explicit Intents` : Requires specified information, which targets an application's package name.
- `Implicit Intents` : Implicit Intents declares a general action to perform like showing gallery image, opening URL on web browser, you can use implicit intent to request action to the android system. Then android system shows all the appropiate components for that request if found.

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
  - [💉](#workmanager)`WorkManager` : Background Processing API, gurantees background work by scheduling works, runs deferrable.

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

### MVC
Stands for Model, View, Controller.
- `Model` : It is the business logic and data state. Used to retieve and manipulate data, communicate with controllers, interact with database and update views.
- `View` : View determines what the user sees in an application, XML.
- `Controller` : It's Activity/Fragment i.e. communitcation betwween Model and View. Handls user interactions with our application.

***User interacts with the UI, which notifies the Controller. Based on the interaction the Controller modifies particular models, then Models perform some business logic and return the updated model state to Controller, which updates the UI according to the new data state.***

[figure](https://miro.medium.com/max/828/1*FZ0Lk8d8oUADJmG98S6nHw.png)

### MVP
Stands for Model, View, Presenter.
- `Model` : Layer for storing data, handles domain/business logic and is responsible for communicating with database and netwrok layers.
- `View` : UI layer i.e. Views/Layouts/Activities/Fragments. Will implement as interface for the Presenter's actions.
- `Presenter` : Presenter has no relation with Views (unlike MVC). Operations are invoked by our views, and View are updated via View's interface.
  
***In MVP, Views and Presenters interact each other via interface (unlike MVC). Presenters perform some action on the Interface, which is implemented in Views, which results in updation of View***

[figure](https://miro.medium.com/max/828/1*t5OmKxbq-jST_JtJhZCVJw.png)

### MVVM 
[⭐](#interview-questions)

One of the most popular achitecture designs in modern Android Development since Google officially announced Architecture Components, such as ViewModel, LiveData and Data Binding.
Consists of View, ViewModel, Model
- `View` : Responsible for constructing the UI of what the user sees on the screen, includes UI elements such as TextView, Button, or Jetpack Compose UI. UI elements trigger user events to the **ViewModel** and configure UI screens by observing data or UI states from the **ViewModel.** Includes only UI logic and not business logic.
- [💉](#viewmodel)
  `ViewModel` : Independent component that does not have any dependencies on **View**, holds buisness logic or UI states from the **Model** to propogates them into UI elements. **ViewModel** notifies data changes to **View** as domain data or UI states.
- `Model` : Encapsulates the app's domain/data model, which typically includes buiness logic, complex computational works.

### MVI

MVI (Model-View-Intent) is also a popular architecture in modern Android Development since Jetpack Compose has brought declarative programming to android.

### Clean Architecture

## Brief

### Services
[🔝](#table-of-contents)
***A service is an application component that can perform long-running operations in the background. Moreover, main android components can bind to service to interact with it and also can perfrom InterProcess Communication (IPC)***
- For ex: Service to handle netwrok transactions, play music, perform I/O, or interact with content provider, all from backrgound.
- **Caution :** A service runs in the main thread, it neither creates its own thread nor run in a seperate process unless you specify otherwise. You should run any blocking operations on a seperate thread within the service to avoid Application Not Responding (ANR) erros.
- `Types of Services`
  - `Foreground` : Service which performs some operations that is noticeable to the user like playing audio track. **Must display a notification**, so that users are actively aware that service is running. This notification cannot be dismissed unless service is either stopped of removed from the foreground. It continues even when the user isn't interacting with the app. WorkManager API offers flexible and nearly same ways as foreground services too.
  - `Backgound` : Service which performs an operation that isn't directly notified by the user, e.g. background service to compact its storage. System imposes restrictions on API 26 or higher from running background services, when the app itself isn't in the foreground.
  - `Bound` : Type of service that offers a client-server interface that allows components(Activity, content provider and service can bind to the Bound service) to interact with the service, send requests, receive results, and even do so across processes with IPC. Bound service runs only as long as another application component is bound ot it. Multiple Components can bind to service at once, but when all of them unbind, the service is destroyed.
- `Services v/s Threads` : Service is simply a component that can run in the background, even when the user is not interacting with the application, whereas, if you must perform work outside of your main thread, but only while the user is interacting with your application, you should create a new thread. For example : Use service to play audio even if application is in background, and use Thread to play some video but only while the activity is running, you might create a thread in `onCreate()`, start running in `onStart()` and stop in `onStop()`

### Activities
[🔝](#table-of-contents)
***Activities is an independent and reusable component that interacts with the user by providing UI-relevant resources.***
- [Activity Lifecycle Figure](https://developer.android.com/guide/components/activities/activity-lifecycle)<br>
  `onCreate()` -> `onStart()` -> `onResume()` -> `onPause()` -> `onStop()` -> `onDestroy()`
  - `onCreate()` : This callback is called when the system creates your activity, includes initilization logic, which should occur only once like creating views or binding data.
  - `onStart()` : This callback is called when the activity becomes visible to the user.
  - `onResume()` : Means activity is ready to come to foreground and interact with users.
  - `onPause()` : Means activity is no longer in the foreground, and may still be partially visible.
  - `onStop()` : This callback is called when the activity is no longer visible to the user.
  - `onDestory()` : This callback is called before and activity is destroyed. **Release all remaining resources here.**
  
- LifeCycle Scenarios
  - `Navigate A to B` : <br>
    onPause(A) -> onCreate(B) -> onStart(B) -> onResume(B) -> onStop(A)
  - `Navigate back to A from B` : <br>
    onPause(B) -> onRestart(A) -> onStart(B) -> onResume(B) -> onStop(B) -> onDestory(B)
  - `Press HomeButton\ScreenLock From A` : <br>
    onPause(A) -> onStop(A)
  - `Opening From ScreenLock\HomeScreen` : <br>
    onRestart(A) -> onStart(A) -> onResume(A)
  - `Destroying App` : <br>
    onPause(A) -> onStop(A) -> onDestroy(A)
  - `Calling *finish()*` : <br>
    onDestroy(A)
- `onSavedInstanceState()` : Used to store data before pausing the activity.
- `onRestoreInstanceState()` : Used to recover the saved state of an activity during recreation, through *Bundles*.

### Fragments
[🔝](#table-of-contents)

***Reusable part of UI that interacts with users by providing UI elements on top of activities.*** Managed by Fragment Managers.
- [⭐](#interview-questions)[Fragment Lifecycle]()
- [⭐](#interview-questions)
  `add vs replace` : **replace** removes the existing fragment and adds a new fragment, means when you press back button the fragment that got replaced will be recreated with its *onCreateView()* being invoked, wheres **add** retains the existing fragments and adds a new fragments means existing fragment will be active, wont be in *paused* state.

### ViewModel
[🔝](#table-of-contents)

***ViewModel is class designed to hold and manage UI-related data in a life-cycle consious way. This allows data to survive configuration changes such a screen rotations.***
- ViewModel exists from when you first request a ViewModel (usually `onCreate`) untill the activity is finished and destroyed.
- Extend `AndroidViewModel` if you need context inside viewModel, which will provide Application Context.
- `ViewModelProviders.of` method creates a new ViewModel instance when it's called first time. When it's called again, which happens whenever `onCreate` is called, it will return the pre-existing ViewModel associated with the specific Activity/Fragment. This preserves the data.
- Advantages :
  - Handle Configuration changes
  - Lifecycle Awareness
  - Data Sharing
  - Kotlin Coroutines Support
- [⭐](#interview-questions) `How ViewModels Work Internally` :
  
  Here's code to get the instance of `viewModel` :-
  ```kotlin
  viewModel = ViewModelProvider(this, ViewModelFactory()).get(SampleViewModel::class.java)
  ```
  We get the instance of `ViewModelProvider` by passing instance of the `Activity` and `ViewModelFactory`, then we are using that `ViewModelProvider` instance to get the `SampleViewModel` object.
  Now, `ViewModelProvider` internal codes looks like:-
  ```kotlin
  public open classViewModelProvider constructor(
    private val store: ViewModelStore,
    private val factory: Factory,
    private val defaultCreationExtras: CreationExtras = CreationExtras.Empty
    ) {
      ..
  }
  ```
  Where `ViewModelStore` internal code looks like:-
  ```kotlin
  public class ViewModelStore {
    private final HashMap<String, ViewModel> mMap = new HashMap<>();
    final void put(String key, ViewModel vm) {..}
    final ViewModel get(String key) {..}
    ..
  }
  ```
  At the lowest, the object creation of `ViewModel` is handled by `ViewModelStore`, which contains `HashMap<String, ViewModel>` 
  
  where, Key Format : `val canonicalName = modelClass.canonicalName`.
  
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
[🔝](#table-of-contents)

- `Dependency` : Object which is to be used by a dependent i.e. class
- `Injection` : Technique which passes the dependency to dependent i.e. object to the class which wants to use it.
- `Dependency Injection` : Technique where dependencies are provided to a class instead of creating them itself.
- DI helps in laying the groundwork for good app architecture, greater code reuability, and ease of testing.
  
#### Hilt

DI framework build on top of *Dagger*, brings benefits like **compile time correctness, runtime performance, scalability** that Dagger provides, but also Hilt is **integrated with Jetpack libraries and removes most of the boilerplate code** to let us focus on just the important parts.
- Hilt Automatically generates:
  - *Components for integrating Android framework classes*, in Dagger we have to do it manually.
  - *Scope Annotations* for the components.
  - *Predefined bindings and qualifiers*.
- Annotations
  - `@HiltAndroidApp` : Kicks off Hilt code generation. For Application class.
  - `@AndroidEntryPoint` : Add DI container to Android class. For Classes
  - `@Inject` :
    - Construtor Injection : Tells which constructor to use to provide instances and which dependencies it has
      ```kotlin
      @AndroidEntryPoint
      class SomeAdapter @Inject constructor(private val service: SomeService)
      {..}
      ```
    - Field Injection : Populates fields in @AndroidEntryPoint classes.
      ```kotlin
      @AndroidEntryPoint
      class MainActivity: AppCompatActivity(){
        @Inject lateint var adapter: SomeAdapter
        ...
      }
      ```
  - `@HiltViewModel` : Tell hilt how to provide instances of ViewModel.
  - `@Module` : Class in which you can add bindings for types that cannot be constructor injected.
  - `@InstallIn` : Indicates in which Hilt generated DI container module bindings must be available
  - `@Provides` : Adds binding for a type that cannot be constructor injected. Like ROOM instance, Retrofit Instance.
      ```kotlin
      @InstallIn(SingletonComponent::class)
      @Module
      class SomeModule {
        @Provides
        fun providesRetrofitInstance(..): RetrofitInstance {..}
      }
      ```
  - `@Binds` : Shorthand for binding an interface type
  - `@Singleton/@ActivityScoped` : Scoping object to container. The same instance of a type will be provided by container when using that type as a dependency.

### RecyclerView
[🔝](#table-of-contents)

- A `ViewGroup` to efficiently display large sets of data. You supply data, and define how each item looks, and RecyclerView library dynamically creates the elements when they're needed.
- `Components of RecyclerView`
  - `Adapter` : Takes data and sets the data for views
    - `onCreateViewHolder()` : To create a new ViewHolder, not filled with data.
    - `onBindViewHolder()` : To associate a ViewHolder with data.
    - `getItemCount()` : To get the size of the data set.
  - `ViewHolder` : Wrapper around a `View` that contains layout of and individual item.
  - `LayoutManager` : Manages how we need to display the items on screen.
- [⭐](#interview-questions)
  `Difference between ListView & RecyclerView?`
  - `ViewHolderPattern` : In ListView it was a recommended pattern but not compulsion like in RecylerView.
  - `LayoutManager` : ListView only supported vertical ListView, not even horizontal ListViews. While recyclerView has
    - LinearLayoutManager : Both Vertical and Horizontal lists.
    - GridLayoutManager : Displaying items in grid like gallery.
    - StaggeredLayoutManager : Like Pinterest.
  - `Performance` : As name implies RecyclerView ***recycles*** the individual elements. When an item scrolls off the screen, it doesn't destroy its view. Instead, it reuses the view for new items that have scrolled onscreen. ***This resue vastly improves performance, app's responsiveness and reduces power consumption.***
  - `Animations & Decorations` : ListView lacks in support of good animations and decorations, but `ItemAnimator` and `ItemDecorator` classes of RecyclerView provides developers huge control over these things.
- `Internal Working Of RecyclerView`
  - RecyclerView loads view just ahead and behind the visible entries. So, the **Scrapped View** (View which was once visible and now not visible) gets stored in a collection of scrapped views. Now as we keep scrolling, the view from that collection is used. The view which we loaded from the scrapped view is called **Dirty view**. Now. the dirty view gets *recycled* and is relocated as the new item in queue which has to be displayed on the screen.

### WorkManager
[🔝](#table-of-contents)

*WorkManager aims to simplify the developer experience by providing a first-class API for system-driven background processing. It is intended for background jobs that should run even if the app is no longer in the foreground. Where possible, it uses JobScheduler or Firebase JobDispatcher to do the work; if your app is in the foreground, it will even try to do the work directly in your process.*
- `Components`

### Notification

- `NotificationManager` : A system service which helps in displaying the content as notification. It is responsible for sending a notification, updating its content, and cancelling the notification.
- `NotificationChannel` : Way to group notifications, making it easy for developers and users to control all of the notifications in the channel.

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
- [ViewModel](https://medium.com/androiddevelopers/viewmodels-a-simple-example-ed5ac416317e)
- [ViewModel](https://blog.mindorks.com/android-viewmodels-under-the-hood)
- [ViewModel](https://www.youtube.com/watch?v=LNWpj2k9RUk&t=2988s&ab_channel=RajeshHadiya)
- [Coroutine 1](https://medium.com/androiddevelopers/coroutines-on-android-part-i-getting-the-background-3e0e54d20bb)
- [Coroutine 2](https://medium.com/androiddevelopers/coroutines-on-android-part-ii-getting-started-3bff117176dd)
- [Coroutine 3](https://medium.com/androiddevelopers/coroutines-on-android-part-iii-real-work-2ba8a2ec2f45)
- [Architecture 1](https://www.codingninjas.com/codestudio/library/difference-between-mvc-mvp-and-mvvm-architecture-in-android)
- [Architecture 2](https://anmolsehgal.medium.com/common-android-architectures-mvc-vs-mvp-vs-mvvm-afd8461e1fee)
- [The Ugly Truth about Extension Functions in Kotlin](https://medium.com/android-news/the-ugly-truth-about-extension-functions-in-kotlin-486ec49824f4)
- [Services](https://developer.android.com/guide/components/services)
- [Android Services](https://medium.com/@huseyinozkoc/android-services-tutorial-with-example-fa329e6a5b4b)
- [Services. The life with/without. And WorkManager](https://medium.com/google-developer-experts/services-the-life-with-without-and-worker-6933111d62a6)
