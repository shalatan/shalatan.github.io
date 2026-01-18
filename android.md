# <a name='Android'></a>Android

## <a name='guide'></a>Guide

- Click 🔝 Icons To Jump To Table of Contents
- Topic With ⭐ Icons are questions asked from me in Interviews, Click on it to jump to ***Interview Questions Section***
- Click 💉 before topics for detailed section of it.

## <a name='table-of-contents'></a>Table of Contents
- [Android](#android)
  - [Guide](#guide)
  - [Table of Contents](#table-of-contents)
  - [Topics](#topics)
    - [Android Platform Architecture](#android-platform-architecture)
    - [Definitons](#definitons)
    - [Anroid App Components](#anroid-app-components)
    - [Intents](#intents)
    - [Launch Modes](#launch-modes)
    - [Architecture Components](#architecture-components)
    - [Android Jetpack](#android-jetpack)
    - [Creational Design Patterns](#creational-design-patterns)
    - [Architectural Pattern](#architectural-pattern)
      - [Clean Architecture](#clean-architecture)
    - [Architectural Design Pattern](#architectural-design-pattern)
      - [MVC](#mvc)
      - [MVP](#mvp)
      - [MVVM](#mvvm)
      - [MVI](#mvi)
    - [Design Principles](#design-principles)
      - [SOLID](#solid)
      - [DRY](#dry)
      - [KISS](#kiss)
      - [DI](#di)
  - [Brief](#brief)
    - [Services](#services)
    - [Activities](#activities)
    - [Fragments](#fragments)
    - [ViewModel](#viewmodel)
    - [Coroutines](#coroutines)
    - [Flow](#flow)
    - [Dependency Injection](#dependency-injection)
      - [Hilt](#hilt)
    - [RecyclerView](#recyclerview)
    - [WorkManager](#workmanager)
    - [Thread](#thread)
    - [Compose](#compose)
  - [Optimization](#optimization)
    - [Build Speed](#build-speed)
    - [Performance](#performance)
  - [Tools and Libraries](#tools-and-libraries)
    - [Sentry](#sentry)
    - [Perfetto](#perfetto)
  - [Interview Questions](#interview-questions)
  - [References](#references)

## <a name='topics'></a>Topics

### <a name='android-platform-architecture'></a>Android Platform Architecture
[🔝](#table-of-contents)

- `Linux Kernel` : Core of android platform architecture. Manages all the hardware drivers, low-level memory.
- `Hardware Abstraction Layout (HAL)` : Bridges hardware capabilities to the higher-level Java API Framework by defining standard interfaces.
- `Android Runtime (ART)` : Converts Dalvik Executable Format (DEX) bytecode into machine code that system can understand. Replaced Dalvik Virtual Machine for devices running Android 5.0 (Lollipop).
- `Native C/C++ Libraries` : Native APIs let you manage native activities and access physical device components like camera, sensor, graphic .
- `Java API Framework (Application Framework)` : Collection of Android Libraries written in Java and Kotlin. Ex: Android Jetpack
- `System Apps` : Pre-installed apps such as email, SMS messaging, calendars, contacts

### <a name='definitons'></a>Definitons
[🔝](#table-of-contents)

- [⭐](#interview-questions)
  `Context` : It is the context of the current state of application/class. Used to get information regarding the activity and application. Used to access *Resources, Databases, SharedPreferences*
  - `Application Context` : Tied to lifecycle of an application, can be used to create singleton objects.
  - `Activity Context` : Tied to lifecycle of an activity, should be used when passing the context in activity.
- [⭐](#interview-questions)
  `Application Class` : Base class within an Android app that contains all other components such as activities and services. It is instantiated before any other class when the process for your application is created.
- `Android Manifest` : Describes essential information about the application such as package name, entry points, components, permissions, and metadata.
  - `Package Name` : Application's univerally unique application ID

### <a name='anroid-app-components'></a>Anroid App Components
[🔝](#table-of-contents)[⭐](#interview-questions)

App components are like entry points that allow systems and users to interact with your application. Each component have their own function and lifecycle.
- [💉](#activities)`Activities` : Entry point for interacting with users, represents single screen with UI
- [💉](#services)`Services` : Entry point for keeping app running in background for all kinds of reason, like music player, youtube video player.
  - `startService()` : Allows other components to run a service in background or stop it, using *startService()* & *stopService()* respectively.
  - `bindService()` : Same as startService but also provides IBInder interface, which allows the client to communicate with the service consistently. Use *unbindService* to cancel the connection
- `Broadcast Receivers` : Registerable listener that listens to broadcast messages from Android system or other applications. Where Broadcasts are used to send messages across apps, outside of the normal user flow, like device starts charging. No lifecycle like Services and Activities.
- `Content Providers` : Manages shared set of data. Through content providers, apps can query or modify other app's data ***if they have required permissions.***

### <a name='intents'></a>Intents
[🔝](#table-of-contents)
**Intent is a messaging object that is used to request an action from another app component.**
- `Explicit Intents` : Explicit Intents are used to start a specific component within the same application or another application by explicitly specifying the target component's class name.
- `Implicit Intents` : Implicit Intents declares a general action to perform like showing gallery image, opening URL on web browser, you can use implicit intent to request action to the android system. Then android system shows all the appropiate components for that request if found.

### <a name='launch-modes'></a>Launch Modes
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

### <a name='architecture-components'></a>Architecture Components
[🔝](#table-of-contents)


### <a name='android-jetpack'></a>Android Jetpack
[🔝](#table-of-contents)
> Suites of libraries to reduce boiler plate code, follow best practices.

- `App Architecture` : Google's recommneded app achitecture below allows apps to scale, improve quality, robustness and makes apps easier to test.

  `UI Layer` -> `Domain Layer` -> `Data Layer` 
  - `UI Layer` : Render the updated application data on screen. Also known as Presentation layer. Made of UI elements, and State holders, such as *ViewModel*
  - `Domain Layer` : Abstracting complex/simple business logic, converts complex data into suitable types for UI layers. **Optional**
  - `Data Layer` : Contains the *business logic*. Made of *repositories*, that can contain zero to many data sources.

- `UI Layer Libraries`
  - `ViewBinding` : Generates a binding class for each XML layout file.
  - `DataBinding` : Generates a binding class for XML layouts that includes a **layout** tag. Linkd View and ViewModel with observer pattern, properties and event callbacks.
  - [💉](#viewmodel)
    `ViewModel` : It's a state holder to store and manage UI related data surviving configuration changes.
  - [💉](#livedata)
    `LiveData` : It's a lifecycle-aware data holder, which can be observed by multiple Observers, used to implement Observer Pattern.
  - `Lifecycle` : Jetpack's Lifecycle allows you to build independent components, which observes the lifecycle changes of lifecycle owners like activities or fragments.
  - [💉](#fragments)
  `Fragment` : segment your app into multiple, independent screens that are hosted within an Activity.
  - [💉](#compose)
  `Compose`
- `Data Layer Libraries`
  - `DataStore` : Used to store lightweight key-value pairs in local storage, works with Coroutines and Flow to store data asynchonously. Can be used to replace SharedPreferences. 
  - `Room` : Abstraction layer over SQLite Databases simplyfying access of database.
  - [💉](#workmanager)`WorkManager` : Background Processing API, gurantees background work by scheduling works, runs deferrable.
  - `Paging` : 

### <a name='creational-design-patterns'></a>Creational Design Patterns
[🔝](#table-of-contents)

Reusable solutions to solve repeated and common software problems in software engineering.
**These are lower-level patterns used to address object creation and manage dependencies within your code. They focus on how objects are created, configured, and returned.**
- `Singleton Pattern`: Only one instance exists in the application
  ```kotlin
  object Singleton{ 
    fun doSomething(){

    }
  }
  ```
- `Factory Pattern`: Where factory takes care of all the object creational logic. In this pattern, factory class controls which object to instantiate. This pattern comes in handy when dealing with many common objects.
- `Builder Pattern`: Builder pattern in android is used to construct complex objects with optional parameters. It provides clean and fluent API for creating objects step by step. Ex: `AlertDialog.Builder()`, `Intent.Builder()`, Room, Retrofit
  ```java
  class Hamburger private constructor(
      val cheese: Boolean,
      val onions: Boolean
  ) {
      class Builder {
          private var cheese: Boolean = true
          private var onions: Boolean = true

          fun cheese(value: Boolean) = apply { cheese = value }
          fun onions(value: Boolean) = apply { onions = value }

          fun build() = Hamburger(cheese, onions)
      }
  }

  //use as 
  Hamburger ham = Hamburger.Builder().cheese(true).onions(false).build()
  ```
  Can be replaced with data classes in kotlin
  ```kotlin
  var ham = Hamburger(cheese = true, onions = false)
  ```
- `Facade Pattern`: Facade (surface) pattern is a structural design pattern that provides higher-level interface that make set of other interfaces easier to use. Example Retrofit's
  ```kotlin
  interface Movies {
    @GET("movies")
    fun getMovies(): List<Movies>
  }
  ```
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
  
### <a name='architectural-pattern'></a>Architectural Pattern
[🔝](#table-of-contents)

Architectural Patterns are system-wide and deal with the overall structure of the application, such as Clean Architecture. 

Architecture defines boundaries between each layer, defines the responsibilities clearly affecting project's complexity, scalability and robustness, and makes it easier to test.

#### <a name='clean-architecture'></a>Clean Architecture
- Clean architecture is about organizing code into layers to ensure that the core business logic is independent of frameworks, UI, and external data sources.
- In android it constitutes of three layers:
  - `Presentation Layer`: Architectural Design Patterns like MVVM and MVI focus on structuring the presentation layer, handling UI interactions, and managing state.
    - `View` : Its main responsibility is to display data to the user and respond to user interactions.
    - `ViewModel` : It holds and manages UI-related data. While it interacts with Use Cases to request or modify data, it does not perform business logic.
  - `Domain Layer`:
    - `Entities`: Core business objects that are independent of UI, databases, or any frameworks.
    - `UseCase`: This is where the business logic resides. A Use Case is responsible for performing specific operations, such as fetching a list of movies, processing data, or applying any necessary transformations.
  - `Data Layer`: These represent how the data is presented and consumed. Repositories and mappers live here, converting data from external sources (APIs, databases) into entities.
- `Flow`:
  1. The UI layer (View and ViewModel) interacts with the Domain layer (Use Cases) and asks for data.
  2. The Domain layer is independent of any Android-specific code, making it highly testable.
  3. The Data layer (Repositories) fetches data from external sources like databases or APIs and provides it to the Domain layer.
- `Dependency Rule:`: 
  1. Each layer should only depend on abstractions, not on concrete implementations.
  2. The outer layers (UI and Data) can depend on the inner layers (Domain), but the Domain layer should not depend on the UI or Data layers.

### <a name='architectural-design-pattern'></a>Architectural Design Pattern
[🔝](#table-of-contents)

Architectural Design Patterns like MVVM and MVI focus on structuring the presentation layer (of Clean Architecture), handling UI interactions, and managing state.

#### <a name='mvc'></a>MVC
Stands for Model, View, Controller.
- `Model` : It is the business logic and data state. Used to retieve and manipulate data, communicate with controllers, interact with database and update views.
- `View` : View determines what the user sees in an application, XML.
- `Controller` : It's Activity/Fragment i.e. communitcation betwween Model and View. Handls user interactions with our application.

***User interacts with the UI, which notifies the Controller. Based on the interaction the Controller modifies particular models, then Models perform some business logic and return the updated model state to Controller, which updates the UI according to the new data state.***

[figure](https://miro.medium.com/max/828/1*FZ0Lk8d8oUADJmG98S6nHw.png)

#### <a name='mvp'></a>MVP
Stands for Model, View, Presenter.
- `Model` : Layer for storing data, handles domain/business logic and is responsible for communicating with database and netwrok layers.
- `View` : UI layer i.e. Views/Layouts/Activities/Fragments. Will implement as interface for the Presenter's actions.
- `Presenter` : Presenter has no relation with Views (unlike MVC). Operations are invoked by our views, and View are updated via View's interface.
  
***In MVP, Views and Presenters interact each other via interface (unlike MVC). Presenters perform some action on the Interface, which is implemented in Views, which results in updation of View***

[figure](https://miro.medium.com/max/828/1*t5OmKxbq-jST_JtJhZCVJw.png)

#### <a name='mvvm'></a>MVVM 
[⭐](#interview-questions)

One of the most popular achitecture designs in modern Android Development since Google officially announced Architecture Components, such as ViewModel, LiveData and Data Binding.
Consists of View, ViewModel, Model
- `View` : Responsible for constructing the UI of what the user sees on the screen, includes UI elements such as TextView, Button, or Jetpack Compose UI. UI elements trigger user events to the **ViewModel** and configure UI screens by observing data or UI states from the **ViewModel.** Includes only UI logic and not business logic.
- [💉](#viewmodel)
  `ViewModel` : Independent component that does not have any dependencies on **View**, holds buisness logic or UI states from the **Model** to propogates them into UI elements. **ViewModel** notifies data changes to **View** as domain data or UI states.
- `Model` : Encapsulates the app's domain/data model, which typically includes buiness logic, complex computational works.

#### <a name='mvi'></a>MVI
MVI is another design pattern but focuses more on a **unidirectional data flow** and treating state as **immutable**. It's a bit more modern and reactive than MVVM and fits well with frameworks like Jetpack Compose
- `Model` : Represents the current state of the screen or UI. In MVI, this state is immutable and a single source of truth for the entire UI.
- `View` : This is similar to MVVM, where the View renders UI, but it reflects the current state provided by the Model.
- `Intent` : User actions or events from the View trigger Intents which are passed to the ViewModel. These Intents are then processed, resulting in a new state. 


### <a name='design-principles'></a>Design Principles
[🔝](#table-of-contents)

Design principles are a set of guidelines or best practices for writing clean, maintainable, and efficient code. These principles help in organizing and structuring code to make it easy to understand, flexible for future changes, and less prone to errors.

#### <a name='solid'></a>SOLID
SOLID is a set of five principles for designing maintainable, flexible, and scalable object-oriented software. These principles guide software development to ensure that systems are easy to understand, extend, and modify without causing major code breakage.
  - `Single Responsibility Principle` : Each class should focus on doing one thing well. If a class has more than one responsibility, changes to one part of the class can impact the other part, making the system harder to maintain.
  - `Open/Closed Principle` : Software entities (classes, modules, functions) should be open for extension but closed for modification. : *You should be able to add new functionality to a class or module without changing its existing code. This is typically done using abstraction and inheritance or interfaces.*
  - `Liskov Substitution Principle` :
  - `Interface Segregation Principle` : No client should be forced to depend on interfaces it does not use : *Instead of having one large interface that covers all use cases, it’s better to create smaller, more specific interfaces. This way, classes only need to implement methods they actually use.*
  - `Dependency Inversion Principle` : High-level modules should not depend on low-level modules. Both should depend on abstractions. This reduces coupling between components and makes the system more flexible and easier to modify.

#### <a name='dry'></a>DRY
#### <a name='kiss'></a>KISS
#### <a name='di'></a>DI

## <a name='brief'></a>Brief

### <a name='services'></a>Services
[🔝](#table-of-contents)

***A service is an application component that can perform long-running operations in the background. Moreover, main android components can bind to service to interact with it and also can perfrom InterProcess Communication (IPC)***
- For ex: Service to handle netwrok transactions, play music, perform I/O, or interact with content provider, all from backrgound.
- **Caution :** A service runs in the main thread, it neither creates its own thread nor run in a seperate process unless you specify otherwise. You should run any blocking operations on a seperate thread within the service to avoid Application Not Responding (ANR) erros.
- `Types of Services`
  - `Foreground` : Service which performs some operations that is noticeable to the user like playing audio track. **Must display a notification**, so that users are actively aware that service is running. This notification cannot be dismissed unless service is either stopped of removed from the foreground. It continues even when the user isn't interacting with the app. WorkManager API offers flexible and nearly same ways as foreground services too.
  - `Backgound` : Service which performs an operation that isn't directly notified by the user, e.g. background service to compact its storage. System imposes restrictions on API 26 or higher from running background services, when the app itself isn't in the foreground.
  - `Bound` : Type of service that offers a client-server interface that allows components(Activity, content provider and service can bind to the Bound service) to interact with the service, send requests, receive results, and even do so across processes with IPC. Bound service runs only as long as another application component is bound ot it. Multiple Components can bind to service at once, but when all of them unbind, the service is destroyed. Ex: Music Player service.
- `Services v/s Threads` : Service is simply a component that can run in the background, even when the user is not interacting with the application, whereas, if you must perform work outside of your main thread, but only while the user is interacting with your application, you should create a new thread. For example : Use service to play audio even if application is in background, and use Thread to play some video but only while the activity is running, you might create a thread in `onCreate()`, start running in `onStart()` and stop in `onStop()`

### <a name='activities'></a>Activities
[🔝](#table-of-contents)
***Activities is an independent and reusable component that interacts with the user by providing UI-relevant resources.***
- [Activity Lifecycle Figure](https://developer.android.com/guide/components/activities/activity-lifecycle)<br>
  `onCreate()` -> `onStart()` -> `onRestoreInstanceState` -> `onResume()` -> `onPause()` -> `onStop()` -> `onDestroy()`
  - `onCreate()` : This callback is called when the system creates your activity. **Includes initilization logic, which should occur only once like creating views or binding data**
  - `onStart()` : This callback is called when the activity becomes visible to the user.
  - `onRestoreInstanceState()` : Used to recover the saved state of an activity during recreation, through *Bundles*.
  - `onResume()` : Means activity is ready to come to foreground and interact with users. **Initialize components like camera, video player**
  - `onPause()` : Means activity is no longer in the foreground, and may still be partially visible. **Release components like camera, video player**
  - `onStop()` : This callback is called when the activity is no longer visible to the user. **Shutdown CPU intensive operations like maybe saving data in ROOM**
  - `onSaveInstanceState()` : Used to store data before pausing the activity.
  - `onDestory()` : This callback is called before and activity is destroyed. **Release all remaining resources here**
  
- LifeCycle Scenarios
  - `Navigate A to B` : <br>
    onPause(A) -> onCreate(B) -> onStart(B) -> onResume(B) -> onStop(A)
  - `Navigate back to A from B` : <br>
    onPause(B) -> onRestart(A) -> onStart(A) -> onResume(A) -> onStop(B) -> onDestory(B)
  - `Press HomeButton\ScreenLock From A` : <br>
    onPause() -> onStop() -> onSaveInstanceState()
  - `Opening From ScreenLock\HomeScreen` : <br>
    onRestart() -> onStart() -> onResume()
  - `Configuration Change` : <br>
    onPause() -> onStop() -> onSaveInstanceState() -> onDestroy() -> onCreate(bundle) -> onStart() -> onRestoreInstanceState() -> onResume()
  - `Destroying App` : <br>
    onPause(A) -> onStop(A) -> onDestroy(A)
  - `Calling *finish()*` : <br>
    onDestroy(A)

[ref: The Android Lifecycle cheat sheet](https://medium.com/@JoseAlcerreca/the-android-lifecycle-cheat-sheet-part-i-single-activities-e49fd3d202ab)

### <a name='fragments'></a>Fragments
[🔝](#table-of-contents)

***Reusable part of UI that interacts with users by providing UI elements on top of activities.*** Managed by Fragment Managers.
- [⭐](#interview-questions)[Fragment Lifecycle Figure](https://developer.android.com/static/images/guide/fragments/fragment-view-lifecycle.png)
  `onAttach()` - > `onCreate()` ->  `onCreateView()` -> `onActivityCreated()` -> `onStart()` -> `onResume()` -> `onPause()` -> `onStop()` -> `onDestroyView()` -> `onDestroy()` -> `onDetach()`
  - `onAttach()` : This method is called first to know that fragment has been attached to the Activity.
  - `onCreate()` : This method is called when the fragment instance initializes.
  - `onCreateView()` : This callback is called when frgament is ready to draw its UI for first time. To draw UI, return the fragment's root layout view component, return null if no UI.
  - `onActivityCreated()` : This callback is called when Activity completes its onCreate() method.
  - `onStart()` : Means fragment is visible.
  - `onResume()` : Means fragment is visible and ready to interact with users.
  - `onPause()` : This method is called when a fragment is not allowing the user to interact.
  - `onStop()` : This callback is called when the fragment is no longer visible to the user. 
  - `onDestroyView()` : This method is called when the view and realted resources created in onCreateView() are removed from activity's view hierarchy & destroyed.
  - `onDestory()` : This callback is called before and activity is destroyed.
  - `onDetach()` : When fragment is detached from its host activity.
- [⭐](#interview-questions)
  `add vs replace` : **replace** removes the existing fragment and adds a new fragment, means when you press back button the fragment that got replaced will be recreated with its *onCreateView()* being invoked, wheres **add** retains the existing fragments and adds a new fragments means existing fragment will be active, wont be in *paused* state.

### <a name='viewmodel'></a>ViewModel
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
- Q: How viewModel knows then to retain it when it's a screen rotation 

### <a name='coroutines'></a>Coroutines
[🔝](#table-of-contents)

***Coroutines are powerful feature introduced in Kotlin to handle asynchronous programming in a more concise and efficient manner. In context of Android development, coroutines provide a way to perform asynchronous operations, such as network requests, database queries, without blocking the main thread.***
- Advantages of coroutines:
  - **Main thread safety**: Coroutines allows developers to perform asynchronous tasks without blocking the main thread.
  - **Simplified asynchronous code**: Coroutines provide a more concise and readable way to write asynchronous code compared to traditional callback-based approaches. This leads to code that is easier to understand, maintain, and debug.
  - **Integration with Lifecycles**: Coroutines can be seamlessly integrated with the Android components lifecycle like Activity or fragment, helping to avoid memory leaks and waste of resources,
- `suspend` : Keyword to mark a function available to coroutines, *suspends* exceution until the result is ready then it resumes where it left off with the result. ***Using suspend doesn’t tell Kotlin to run a function on a background thread.***
- `Dispatchers` : Context
  - `Dispatchers.Main` : Lightweight tasks eg - updating UI, network calls, database queries, won't block the main thread while suspended. Common when you need to perform UI-related tasks or update the user interface from coroutines.
  - `Dispatchers.IO` : For heavy IO work such as reading from or writing to files, making network requests, or interacting with databases.
  - `Dispatchers.Default` : For CPU intensive tasks. It's suitable for computational work or network requests that don't require interaction with the UI.
  - `Dispatchers.Unconfined` : Runs coroutines unconfined on no specific thread, not recommended to use. 
- `CoroutineScopes` : Keeps track of coroutines, even suspended ones, can cancel all of the coroutines started in it.
  - `globalScope` : Top level Coroutine scope that will be associated with the application lifecycle. Since it's alive along the application lifetime, it's a *Singleton* object
  - `viewModelScope` : Coroutine scopre tied to *viewModel*. Extension function of the *viewModel* class, bound to *Dispatchers.Main* and will automatically be cancelled when viewModel is cleared.
  - `lifecycleScope` : Bound to lifecycle of the Activity/Fragment to avoid memory leak and resource waste.
  - `CoroutineScope`: Useful for creating a custom scope within a function, class or service. <br> ```CoroutineScope(Dispatchers.Main).launch { ... }```
  > **Q**: What if we want to cancel only some coroutines and retain some other coroutines inside the parent scope? <br>
  **Ans**: We can define Job using launch and cancel it whenever we want. Job is actually coroutine itself.<br>

  ```kotlin
  private lateinit var coroutineScope: CoroutineScope
  private lateinit var job1: Job
  private lateinit var job2: Job

  private fun startCoroutine(){
    coroutineScope = CoroutineScope(Dispatchers.Main)
    job1 = coroutineScope.launch {  println("job1") }
    job2 = coroutineScope.launch {  println("job2") }
  }

  private fun cancel() {
    if (::mJob1.isInitialized && mJob1.isActive) { 
      mJob1.cancel() 
      }
  }
  ```
- *Room* and *Retrofit* make suspending functions *main-safe*, it's safe to call these suspend functions from *Dispathers.Main*, even though they fetch from network and write to database. Do not use ***Dispatchers.IO***.
- `Builders` : 
  - `runBlocking{}` : Is used to create or launch a new coroutine that blocks the current thread until all its child coroutines complete *aka stop the excution of code written after it*
  - `launch{}` : Will start a new coroutine without blocking the current thread that is *fire and forget* - that means it won't return the result to the caller. Instead, it returns an object of type **Job**, which can be used to cancel the coroutine and also includes a function named **join()**. Like **await()**, the **join()** function suspends the coroutine until the code in the **launch()** block has completed.
  - `async{}` : This builder works a lot like launch(), but instead of returning a Job object, it returns an object that is a subtype of Job, named **Deferred**. This object gives us a function named **await()**, which allows us to get the result from order(). await() is a suspending function, and it will suspend the coroutine until its async() coroutine has completed.
  - `coroutineScope` : Is used to create a new coroutine scope and wait for all its child coroutines to complete. It's similar to runBlocking but doesn't block the thread it's called on
  - `withContext{}` : Is used to switch the coroutine's context temporarily. It's useful for changing the thread or coroutine dispatcher within a coroutine. This builder allows you to execute code in a different context without starting a new coroutine.
  ```kotlin
  withContext(Dispatcher.Main) { }
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
  - `CoroutineScope` : Coroutines launched within a CoroutineScope are automatically cancelled when the associated lifecycle component is destroyed, helping to manage the lifecycle of coroutines.
  - `coroutineScope` : coroutineScope builder will suspend itself until all coroutines started inside of it are complete, hence there's no way to return from `callTwoAPI` until all coroutines are completed.
  ***Cancels whenever any of the children coroutine fails*** meaning if one network request fails, all of the others request would be cancelled immediately.
  - `supervisorScope` : supervisorScope builder won't cancel children when one them fails.
- `Cancellation` : using function **cancel()** we can cancel any coroutine. 
  - Thanks to structured concurrency, when the root coroutine is canceled, we don’t need to manually cancel each of its children. Instead, each child coroutine is automatically sent a signal to cancel.
  - But if coroutine code doesn’t cooperate by choosing to check for cancellation, it won’t notice the signal itself. We can check the **isActive** property of the CoroutineScope, or by calling its **ensureActive()** function.
  - `Cancelling child coroutine` : We can cancel any child coroutine by calling **cancel()**, the cancellation does not affect parent or sibling coroutines.
  
> [⭐](#interview-questions)
  **Q**: What is a difference between Threads & Coroutines? <br>
  **Ans**: Threads are expensive, require context switches which are costly, and number of threads that can be launched is limited by the underlying operating system whereas, Coroutines can be thought of as light-weight threads, means the creating of coroutines doesn't allocate new thread, instead they use predefined thread pools and smart scheduling for the purpose of which task to execute next and which tasks later. <br>
  **Q**: What happens when launches coroutines finishes it's works<br>
  **Ans**: Once the coroutine finishes, its resources are released, and it will no longer consume memory or power. And coroutine along with any data associated with it, becomes eligible for garbage collection, as there would be no active references to it.
  <details>
  <summary>Sample Code for mostly asked in interviews</summary>
  <div markdown="1">

  ```kotlin
  import kotlinx.coroutines.*
  import kotlin.system.measureTimeMillis

  fun main() = runBlocking {
      val timeTaken = measureTimeMillis {	
          //sequential: will work in 7 seconds
  //      println(api1()) // Suspends for 2 sec
  //     	println(api2()) // Suspends for 5 sec

          //parallel: will work in 5 seconds
          coroutineScope {
              //can be done without coroutineScope, but to do in structured scope and better management
              val result1 = async { api1() }
              val result2 = async { api2() }
              try {
                  val pair = Pair(result1.await(), result2.await())
                  println(pair)
              }catch(e: Exception){
                  result1.cancel()
                  result2.cancel()
                  println("error: $e.message")
              }
          }     
      }
      println("timeTaken: $timeTaken")
  }

  suspend fun api1(): String {
      delay(2000)
  //     throw RuntimeException("API 1 failed")
      return "hello"
  }

  suspend fun api2(): String {
      delay(5000)
      return "world"
  }
  ```
</div></details>

### <a name='flow'></a>Flow
[🔝](#table-of-contents)

*Flow is an asynchronous data stream that emits values to the collector and gets completed with or without an exception.*
- Types of data streams:
  - `Hot Stream` : **Hot streams trasmit data even if there's no subscriber when the data arrives.** Ex: *Channels*, for fetching data from APIs, however since there will always be data flow in hot stream, it is necessary to keep the subscribers under control. Because it can cause data loses(if subscriber is forgotten) and memory leaks(open network cinnection)
  - `Cold Stream` : **Cold streams trasmit data only when you start collecting.** Ex: *Kotlin Flow*, powered by Kotlin Coroutines, and because of Kotlin Coroutines, when you cancel the scope, you also dispose of the flow. We don't have to free up memory manually.
- Major Components of Flow:
  - **`(a) Builders`**:
    - `flow{}` : create a flow from the suspendable lambda block.
      ```kotlin
      flow {
        (1..5).forEach{
          emit(it)
        }
      }.collect{
        print(it)
      }
      ```
    - `flowOf()` : to create a flow from fixed set of values
      ```kotlin
      flowOf(1,2,3,4,5)
        .collect {
          print(it)
        }
      ```
    - `asFlow()` : 
      ```kotlin
      (1,2,3,4,5).asFlow()
      .collect {
        print(it)
      }
      ```
    - `channelFlow()` : 
      ```kotlin
      channelFlow {
        (0..10).forEach{
          send(it)
        }
      }.collect{
        print(it)
      }
      ```
  - **`(b) Operators:`** The operator helps in transforming the data from one format to another.
    - `Intermediate Operator` : Used to modifying the data flows between the producer and consumer -OR- These operators are functions that, when applied to a stream of data, set up a chain of operations that aren't executed until the values are consumed in the future and **are executed lazily**
      ```kotlin
      fun main() = runBlocking { 
        requestNumbers()
            .filter { number -> number > 2 }
            .map { number -> toUiModel(number) }
            .catch { error -> println(error) }
            .collect { println(it) } 
      }
      ```
      `Upstream flow` : Flow produced by the operators that are called before the current operator whereas `Downstream flow` is Flow produced by operators that are called after the current operator.
      - `buffer()` : Normanlly, flows are sequential, that means the code of all the operators is executed in the same coroutine. Which means the total execution time is going to be the sum of execution times of all operators. Hence *buffer* creates a seperate coroutine during execution for the flow it applies to.
      - `zip()` : Zips the emissions of two flow emissions with a specified function and emits single item for each combination. Example: Merging two parallely running tasks and getting the results of both task in single callback when both are completed.
        ```kotlin
          fun runningTaskOne = Flow<String> { 
            return flow {
              delay(2000)
              emit(one) 
            }
          }
          fun runningTaskTwo = flow {
            return flow {
              delay(2000)
              emit(two)
            }
          }

          fun startTask() {
            viewModelScope.launch {
              longRunningTaskOne()
                .zip(longRunningTaskTwo()) { resultOne resultTwo ->
                  return@zip resultOne+resultTwo
                }
                .flowOn(Dispatchers.Default)
                .collect{

                }
            }
          }
        ```
    - `Terminal Operator` : Terminal operators are either suspending function such as *collect, single, reduce, toList etc* or *launchIn* operator that starts collection of the flow in the given scope. They are applied to the *upstream flow* and triggers execution of all operations. Execution of the flow is also called collecting the flow and is always performed in a suspending manner without actual blocking.
      - **`(c) Collector`** : Collect all the values in the stream as they're emitted. Is a suspend function and needs to be executed within a coroutine. It takes a lambda as a parameter that is called on every new value. Since it's a suspend function, the coroutine that calls collect may suspend until the flow is closed.
      - `count` : Count the values that matches specific conditions.
      - `reduce` : Apply a function to each item emitted and emit the final value
        ```kotlin
        val result = (1..5).asFlow()
                    .reduce {a,b -> a+b}
        print(result) 
        //15
      ```
      - `fold` : 
        ```kotlin
          val count = flow.count{

          }
          val reduce= flow.reduce{accumulator, value->

          }
        ```
- `flowOn()` : Used to controlling the thread on which the task will be done.
  ```kotlin
  val flow = flow {
    (1..5).forEach {
      emit(it)
    }
  }.flowOn(Dispatchers.Default)

  CoroutineScope(Dispatchers.Main).launch{
    flow.collect {
      print(it)
    }
  }
  ```
- `Cold Flow v/s Hot Flow` : `Cold Flow` only emits data when there's a collector, can't have multiple collectors and also can't store data whereas `Hot Flow` emits data even when there are no collectors attached to it, it can have multiple collectors and also can store data.
  ```kotlin
  fun getColdFlow(): ColdFlow<T> {}
  fun getHotFlow(): HotFlow<T> {}
  ```
- `State Flow v/s Shared Flow` : Both flow types are examples of *Hot Flow*.
  - `State Flow` : StateFlow needs an initial value and emits it as soon as collector starts collecting. It has the *value property* to check the current value, but also keeps the history of one value that we can fetch directly without collecting. StateFlow emits only distinctive values, and ignores repeated ones. It is similar to *LiveData* but without awareness of Android components lifecycle, ***repeatOnLifecycle*** scope can be used to add the lifecycle awareness to StateFlow. Ex: To store and show data from network calls so it retains value if orientation changes resulting in prohibiting the network call again.
  - `SharedFlow` : SharedFlow doesn't needs an initial value, so does not emit any value by default, neither it supports *value property*. It can emit previous values too using *replay* operator. SharedFlow also emits all the value including the repeated ones too.
  Ex: Show snackbars so it doesnt retains value if orientation changes and snackbar doesn't shows again.
  ```kotlin
  val stateFlow = MutableStateFlow(0)
  val sharedFlow = MutableSharedFlow<Int>()
  ```
- Generally flow refresents *cold streams* but there's a hot stream subtype i.e. `SharedFlow`, also any flow can be turned into *hot* one by `stateIn` or `shareIn` operators, or by converting the flow into a hot channel via `produceIn` operator.
- Difference between `launchIn` and `collect`: Use `collect` when you want to collect and process Flow emissions within a coroutine. Use `launchIn` when you want to launch a new coroutine to collect Flow emissions and manage its lifecycle separately.
  
[ref: Mastering Flow API](https://amitshekhar.me/blog/flow-api-in-kotlin)<br>[ref](https://medium.com/yemeksepeti-teknoloji/introduction-to-kotlin-flows-827f5a71ad7e)<br>[ref](https://kotlinlang.org/api/kotlinx.coroutines/kotlinx-coroutines-core/kotlinx.coroutines.flow/-flow/)

### <a name='dependency-injection'></a>Dependency Injection
[🔝](#table-of-contents)

- `Dependency` : Object which is to be used by a dependent i.e. class
- `Injection` : Technique which passes the dependency to dependent i.e. object to the class which wants to use it.
- `Dependency Injection` : Technique where dependencies are provided to a class instead of creating them itself.
- DI helps in laying the groundwork for good app architecture, greater code reuability, and ease of testing.
  
#### <a name='hilt'></a>Hilt

DI framework build on top of *Dagger*, brings benefits like **compile time correctness, runtime performance, scalability** that Dagger provides, but also Hilt is **integrated with Jetpack libraries and removes most of the boilerplate code** to let us focus on just the important parts.
- Hilt Automatically generates:
  - *Components for integrating Android framework classes*, in Dagger we have to do it manually.
  - *Scope Annotations* for the components.
  - *Predefined bindings and qualifiers*.
- Annotations
  - `@HiltAndroidApp` : Kicks off Hilt code generation. For Application class.
  - `@AndroidEntryPoint` : Add DI container to Android class. For Classes
  - `@Inject` :
    - Constructor Injection : Tells which constructor to use to provide instances and which dependencies it has
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

### <a name='recyclerview'></a>RecyclerView
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
> **Q**. How to optimize RecyclerView? <br>
**Ans:**

### <a name='workmanager'></a>WorkManager
[🔝](#table-of-contents)

*WorkManager aims to simplify the developer experience by providing a first-class API for system-driven background processing. It is intended for background jobs that should run even if the app is no longer in the foreground. Where possible, it uses JobScheduler or Firebase JobDispatcher to do the work; if your app is in the foreground, it will even try to do the work directly in your process.*
- `Components`

### <a name='thread'></a>Thread
[🔝](#table-of-contents)
**It is a lightweight process that an operating system can schedule and run concurrently**<br>
- `Types of thread`:
  - `OS Thread`: Based on OS concept, A thread is a basic unit of CPU utilization. It is comprises of Registers, Program Counter, ThreadID and a Stack. They are also known as Kernel Thread, as they are controlled by Kernel.
  - `User Thread`: Threads that are controlled by users, but in order for the kernel to process the operations in a user thread, each user thread should be passed into the kernel after they are created.
- User Thread in Java: In java, user thread is defined as ThreadClass, which is an implementation of Runnable.
- `Why do we need thread?`: Android application runs on a single thread by default, called the Main or UI thread, which is responsible for UI interactions and drawing on screen. However performing long, heavy tasks on this thread might lead to ANR, unresponsivenss, bad user interaction, hence we creatye background thread to offload heavy tasks.

- `Accessing UI from background/worker thread`: As Android UI toolkit is not thread-safe, we should manipulate UI always from UI/Main thread and not from any background thread. But in case we need to access the UI threads from other threads we can use
  - Activity.runOnUiThread(Runnable)
  - View.post(Runnable)
  - View.postDelayed(Runnable, long)

- `How to create a thread?`:
  - Extend ***Thread*** class
  - Implement a ***Runnable*** and pass it into a Thread object.
- `What are Thread and Runnable?`: Thread is a class that implements Runnable, which is a single method interface that has an abstract function called run()

- `Thread Lifecycle`:
  - **NEW**: state when thread is created
  - **RUNNABLE**: state when thread execute RUNNABLE, by calling THREAD#start()
  - **BLOCKED**
  - **WAITING**: state when current thread is waiting for result from anothe thread, can be achieved by calling *wait()*, *join()*, *park()*
  - **TIMED_WAITING**: similar to waiting, but will wait only for certain amount of time, can be achieved by *sleep(time)*, *wait(timeout)*, *join(timeout)*, *parnkNanos()*, *parkUntil()*
  - **TERMINATED**: state when thread is completed or interrupted


### <a name='compose'></a>Compose
[🔝](#table-of-contents)

## <a name='optimization'></a>Optimization

### <a name='build-speed'></a>Build Speed
- Optimize build configuration
  - `Using Gradle build cache`: Gradle build cache allows us to reuse build outputs to save time on subsequent builds. It can work across different machines or even remotely, allowing one dev to build and other devs (or CI machines) to leverage their cache.
    ```kotlin
    //it's not enabled by deafult, can be enbaled by using in gradle.properties
    org.gradle.caching = true
    //by defaults cache is stored in home directory, can be changed explicitly by
    //buildCache {
      local {
        isEnabled = true
        directory = File(rootDir, "build-cache)
        removeUnusedEntriesAfterDays = 30
      }
    }
    //don't forget to add the folder with cached builds in .gitignore
    ```
  - `Parallel project execution`: Even with decoupled modules, gradle will only run one task at a time by default, while most desktop and CI servers have extra CPU cores available, which can enable parallel execution improving build performance. When enabled, the compiling it done on-demand for multiple modules at the same time.
    ```kotlin
     org.gradle.parallel=true
    ``` 
  - `Keep tools up to date`: Android tools like Android Studio, SDK Tools, Gradle Plugin receive build optimizations and new featues with every update.
  - `Use KSP instead of KAPT`: Kotlin Annotation Processing Tool is significantly slower than the Kotlin Symbol Processor.
  - `Avoid compiling unncessary resources`: such as additional language localizations and screen-density resources.
  ```kotlin
  productFlavours {
    create("dev") {
      resourceConfigurations("en", "xxhdpi")
    }
  }
  ```
  - `Sequenceing repositories`: Gradle searches repositories in the order they're declared, so build performance is imporved if the repositories listed first contains most of the plugins.
  - `Use static dependency version`: Avoid using dynamic version numbers like (com.android.tools.build:gradle:2.+). Using dynamic version numbers can cause unexpected version updates, difficulty resolving version differences, and slower builds caused by Gradle checking for upated. Hence, use static version numbers instead.
  - `Create library modules`: [ref](https://developer.android.com/build/optimize-your-build#create_libraries)
  - `Convert images to WebP`: WebP is an image file format that provides lossy compression (like JPEG) as well as transparency (like PNG). Reducing images file sizes without having to perform build-time compression can speed up your builds. However, you may notice a small increase in device CPU usage while decompressing WebP images.
  - `Experiment with JVM parallel garbage collector`: Build performance can be improved by configuring the optimzal JVM garbage collector used by Gradle. While JDK 8 is configured to use the parallel GC by default, JDK 9 and higher are configured to use G1 GC. To potentially improve build performance, it's recommended to experiment building with parallel GC.
    ```kotlin
    org.gradle.jvmargs=-XX:+UseParallelGC
    org.gradle.jvmargs=-Xmx1536m -XX:+UseParallelGC //if there're other options already set
    ```
    - Parallel Garbage Collector: 
    - G1 Garbage Collector:
- Profile the build: 
- Build Analyzer Tool: Each time we build app, the build analyzer creates a report and displays data from the latest report in the Build window.
  - `Tasks`: Shows breakdown of plugins with tasks determining the build's duration. 
  - `Warnings`: If the Build Analyzer detects that some tasks could be configured to run more efficiently, it provides a warning. Some warnings have a Generate report link, which shows a dialog with additional information that might help the plugin developer resolve the issue in new version of the plugin.
    - `Always run tasks`:
    - `Task setup issues`: 
    - `Configuration cache`: Allows the build system to record information about the task graph once, and to reuse it in subsequent builds, thus avoiding the need to reconfigure the whole build again.
    - `Check Jetifier`: This warning is presented if the enableJetifier flag is present and enabled in your project (gradle.properties) file. The Build Analyzer can perform a check to see whether the flag can be safely removed to enable your project to have better build performance and migrate away from the unmaintained Android Support libraries.
  - `Downloads`: Provides a summary of time spent downloading dependencies and a detailed view of downloads per repository.
[ref](https://developer.android.com/build/optimize-your-build),[ref](https://www.runway.team/blog/advanced-tips-for-improving-android-build-times) [ref]()

### <a name='app-performance'></a>Performance
- `Inspecting Perfomance`:
  1. `Passive: using logcat`:
    - `tag:Choreographer`: info about slow rendering, >30sec is bad
    - `tag:OpenGLRenderer`: if app skips more frames lasting >700ms, its called frozen frame. If app freezes for 5 seconds, we get ANR.
    - `tag:ActivityTaskManager Displayed`: displays time-to-initial-display (TTID), means how long it took to draw the first frame every time open an activity.
  2. System Tracing:
  3. `Automated`:
     1. 

## <a name='tools-libraries'></a>Tools and Libraries

### <a name='sentry'></a>Sentry
To keep tracks of crashes

### <a name='perfetto'></a>Perfetto
Perfetto is a system profiling and app tracing tool by Google. It helps analyse the app by collecting system and app-level performance traces.


## <a name='interview-questions'></a>Interview Questions
- `ListView vs RecyclerView`
- `LiveData vs Flow`
- `lazy vs lateinit`
- `add() vs replace()`
- `Are object variables thread safe`
- `Inner working of ViewModel`
- `Inner working of Extension Functions`
- `Serializable vs Parcelable`: Both are mechanism to pass data between different components but they function differently in terms of performance and implementation.
    - `Serializable`: Serializable is standard Java interface used to convert an object into a byte stream, which can be passed between activities. It works through Java reflection, meaning the system dynamically inspects the class and its fields at runtime to serialize the object. Hence, it is slower process than Parcelable as refection is a slow process. It also generates alot of temporary objects during serialization, increasing the memory overload.
    - `Parcelable`: It is a Android-specific  interface designed specially for high-performance inter-process communication within Android Components. It's faster because it's optimized for Android and doesn't rely on reflection and also minimizes gc by avoiding creating many temporary objects. Preferred when peformance is important.

## <a name='references'></a>References
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
- [The Android Lifecycle cheat sheet — part I: Single Activities](https://medium.com/androiddevelopers/the-android-lifecycle-cheat-sheet-part-i-single-activities-e49fd3d202ab)
- [The Android Lifecycle cheat sheet — part II: Multiple activities](https://medium.com/androiddevelopers/the-android-lifecycle-cheat-sheet-part-ii-multiple-activities-a411fd139f24)
- [The Android Lifecycle cheat sheet — part III : Fragments](https://medium.com/androiddevelopers/the-android-lifecycle-cheat-sheet-part-iii-fragments-afc87d4f37fd)
- [The Android Lifecycle cheat sheet — part IV : ViewModels, Translucent Activities and Launch Modes](https://medium.com/androiddevelopers/the-android-lifecycle-cheat-sheet-part-iv-49946659b094)
- [Android  Fragments and its Lifecycle](https://blog.mindorks.com/android-fragments-and-its-lifecycle)
