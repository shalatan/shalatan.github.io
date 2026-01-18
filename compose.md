
## <a name='Compose'></a>Compose

### <a name='table-of-contents'></a>Table of Contents
- [Compose](#compose)
  - [Table of Contents](#table-of-contents)
  - [Topics](#topics)
    - [Key Components](#key-components)
    - [Compose Phases](#compose-phases)
    - [Why Compose is declarative UI framework](#why-compose-is-declarative-ui-framework)
    - [Recomposition](#recomposition)
    - [State](#state)
    - [State Hoisting](#state-hoisting)

### <a name='topics'></a>Topics
*Jetpack compose is a modern toolkit for building native Android UI. Compose simplifies and accelerates UI development on Android with less code, powerful tools and inuitive Kotlin APIs*

#### <a name='key-components'></a>Key Components
- `Compose Compiler`: Responsible for converting declarative UI code written in Kotlin into optimized code that Jetpack compose can execute. Processes @Composable functions during compilation and generates necessary UI updates and recomposition logic. *Compose Compiler operates directly on FIR (Frontend Intermediate Representation) enabling compiler to access deeper static code insights during compilation, allowing it to tranform Kotlin source code dynamically and generate optimized Java byteocde.*
- `Compose Runtime`: Provides the core functionality required to support recomposition and state management, handles UI states, snapshhots and triggers UI updates whenever state changes. *Compose Runtime functions by memorizing the state of compositions using **slot-table** inspired by **gap-buffer** data-structure. Internally it performs several critical tasks essential for building resposive UIs like managing side-effects, preserving state with remember, triggering recompositions etc*
- `Compose UI`: Offers high-level compoenents and UI widgets for building applications and includes foundational elements like text, button, and layout containers.

#### <a name='compose-phases'></a>Compose Phases
- `1. Composition`: Compose builds the initial UI structure and records the relationship between composables in a data-structure called **Slot Table**. When state changes occur, the composition phase recalculates affected part of the UI and triggers the recomposition.
- `2. Layout`: Determins the size and position of each UI elements, each composable measures its children's dimensions and defines it's position relative to its parent.
- `3. Drawing`: Phase wheer composed and laid-out UI elements are rendered onto the screen. Compose uses **Skia Graphics engine** for this process, ensuring smooth and hardware-accelerated rendering.

#### <a name='why-declarative'></a>Why Compose is declarative UI framework
Because devs describe **what** the UI should look like at any given state rather than detailing **how** to update it when state changes. It handles **how** the UI updates automatically through recomposition.
- `State-driven UI`
- `Defining components as functions or classes`
- `Direct data binding`
- *XML itself is inherently declarative cause in it devs defines what the UI should look like by describing its structure and attributes, leaving the underlying rendering process to the framework. This aligns with core principle of declarative programming- specifying what UI should be, now how it should be rendered. But the key difference lies in state and logic handling. In XML, UI strcuture and attributes are defined in XML, while state management and UI updates are done in imperative code using Java or Kotlin*

#### <a name='recomposition'></a>Recomposition
Mechanism to redraw the UI when state changes occur is called recomposition. When recomposition happens, Compose starts from the Composition phase, notifies the framework about the UI changes.
- Mechanisms to trigger recompositions:
  - `Input changes`: When new input parameter is passed, compose runtime compares it with old arguments using equals() function.
  - `Observing State changes`: Observing a state, typically in combination with the remember functions.
- While recomposition is central to compose's reactive nature but excessive or unnecessary recomposition can degrade app performance. **Layout Inspector** can be used to optimize the number of recomposition counts, by helping us to monitor how often a composable is recomposed or skipped. **Composition tracing** is another tool that allows to try out the recomposition tracing in the project.

#### <a name='state'></a>State
State refers to any value that can change over time and trigger UI update when changed through recomposition. Ex: Snackbar messages, user inputs, animation triggered by interactions. The Compose Runtime automativally tracks state changes and updates the UI without required the manual calls like View.invalidate().
- Managing state in Compose:
  - `remember`: stores object in memory during initial composition and retrives them during recompositions.
  - `rememberSaveable`: same as *remember* but also stores them in *bundle* hence survives configuration changes. Store primitive types automatically like Int, String, boolean but custom objects/data classes needs to be parecelized.
  - `mutabletsateOf`: creates observables state objects that triggers recompositions when their calue changes.


#### <a name='state-hoisting'></a>State Hoisting
- `State hoisting`(lift/elevate) : State hoisting is a pattern where state is lifted to a higher level composable and passed down to child composables. This creates a clear, unidirectional data flow and makes components more reusable.
  - `Advantages of State Hoisiting`: 
    - `Improved Reusability`
    - `Simplified testing`
    - `Better seperation of concerns`
    - `Support for Unidirectional Flow`
    - `Enhanced state management`


- `rememberCoroutineScope`: Recommended approach to safely create and manage coroutine scope within comosable function, as it ensures that the coroutine scope is tied to the composition, preventing potential memory leaks, improper resource usage and manual lifecycle management.
  ```kotlin
  var coroutineScope = rememberCoroutineScope()
  ```
  - `How`:
    - `Composition Awarness`: Coroutine scope created is scoped to the composition and gets cancelled when the composable is removed from the composition.
    - `State Management`:  remember API is used to store and manage state values that need to survive recompoisition.
  - Use for UI-specific tasks tied to composition lifecycle, for longer-running or shared tasks that extends beyound composition's scope, use `viewModelScope` or `lifecycleScope`.
  - **It launches on Main thread by default, hence use it cautiously and avoid directly executing buisness logic, such a network or database calls.**
  - `Internal implementation`: it consists of two key parts:-
    - `createCompositionCoroutineScope`: a new coroutine is created and passed to next step
    - `CompositionScopedCoroutineScopeCanceller`: ensures coroutine scope is aware of the composition lifecycle. Implements `RememberObserver`, hence when composable is removed from the composition, the `onForgotten()` and `onAbandoned()` methods are triggered and coroutine scope is cancelled using coroutineScope.cancel(), preventing memory leaks
- `Side EfFect`: A side effect in Jetpack Compose is any operation that affects or interacts with the outside world and is not directly related to UI rendering, like network call, logging, database write. Three primary side effect handlers are:
  - `LaunchedEffect`: Used to launch coroutine that runs within the composition of the composable.
    - Executes once when the composable enter the composition
    - Automatically cancels and re-launches when the kay(s) chnages
    - Automatically cancels when composables leaves the composition
    - UseCase: *Fetching additional data from network when a user clicks on an item of the list by just updating the key provided to the launchedEffect*
    - UseCase: *To safely observe the flow, as the coroutine launched is automatically cancelled. Aditionally, the coroutine will not be re-launched during recompositions. To ensure the effect matches the lifecycle of the call site, we can pass a contant as key like `Unit` or `true`, this gurantees effect runs only once unless key changes*
    ```kotlin
    var selectedItem: Item by remember { mutableStateOf(null) }
    LaunchedEffect(key1 = selectedItem){
      //will be triggered everytime the key changes
    }
    LaunchedEffect(key1 = Unit){
      stateFlow.collect()
    }
    ```
  - `DisposableEffect`: Is used for managing resources or cleanup tasks that are bound to the composable;s composition. Unlike LaunchedEffect, it provides a `DisposbaleEffectScope` with an `onDispose` lambda to release resources when the composable leaves the composition
    - UseCase: *Ideal for managing resources like listeners, oberservers, or subscriptions. Use DisposableEffect to register the observer when composable enters the composition and automatically unregister when the composable leaves the composition. Ensures proper cleanup and prevents memory leaks.*
    ```kotlin
    DisposableEffect(lifecycleOwner){
      //create observer and attach
      lifecycleOwner.lifecycle.addObserver(observer)

      onDispose {
        lifecycleOwner.lifecycle.removeObserver(observer)
      }
    }
    ```
  - `SideEffect`: Used for running operations that need to apply immediately after every recomposition. **It gurantees execution after the composable has been recomposed,** making it suitable for synchronizing Compose state with external system, like updating UI state in ViewModel.
    - Runs after every recomposition
    - UseCase: *Useful for state synchronization with non-compose components*
    - UseCase *Start a lottie animation or trigger a non-composable action only when recomposition is completed*
    ```kotlin
    SideEffect {
      lottieAnimationView.playAnimation()
    }
    ```



- `Key Terms` :
  - `Composition` : Description of UI built by Compose when it executes composables.
  - `Initial Composition` : When composables gets drawn for the first time.
  - `Recomposition` : When composables (and their children) gets redrawn automatically when the value is updated. The only way to modify the Composition is through recomposition.
  - `State` : State or MutableState are interfaces that can hold some value and trigger UI updates whenever that value changes.
- `Annotations` : 
  - `@Composable`: These are the building blocks of Compose UIs, annotated with @Composable. They can emit UI elements and call other composable functions.
  - `@Preview`: Annotation to preview the composable functions within Android Studio. Not applicable for composable functions which does not take in parameters.
- `Modifiers` : Modifier tell a UI elemnet how to lay out, display, or behave within its parent layout, add high-level interactions, such as making element clickable. *As a best practice, your function should include a Modifier parameter that is assigned an empty Modifier by default.*
  - `ContentPadding` : To maintain the same padding, but still scroll your content within the bounds of your parent list without clipping it, all lists provide a parameter called contentPadding
- `Elements`
  - `Text` : 
  - `Surface` : Allows the customizing like shape and elevation of items.
  - `Layouts Elements` : 
    - `Column` : Arrange items vertically.
    - `Row` : Arrange items horizontally.
    - `Box` : Stack elements
  - `LazyColumn/LazyRow` : Composables that renders only the elements that are visible on screen, so they are designed to be very efficient for long lists. *Doesn't reyce its children like RecycleView, instead emits new composables as you scroll though it and is still performat, as emitting composables is relatively cheap compared to instantiating Views.
  - `Slots` : Slot-based layouts leave an empty space in the UI for the developer to fill as they wish. You can use them to create more flexible layouts.
- `APIs` : 
  - `rememberCoroutineScope`: Preserves a CoroutineScope across recompositions, useful for launching effects that need to survive recomposition:
  - `rememberUpdatedState`: Ensures a callback holds the latest state without restarting the effect.
  - `mutableStateOf` : creates an observable MutableState<T>
  - `collectAsState` : Collects value from StateFlow and represents its latest value via State. <br> *StateFlow.value* is used as an initial value, and everytime a new value is posted into the *StateFlow*, the returned *State* updates, causing recomposition of every *State.value* usage.
  ```kotlin
  var value by remember { mutableStateOf(default) }
  ```
  - `produceState`: For converting external data to state.
  - `LaunchedEffect`: Runs once when the Composable first enters Composition, or restarts when keys change.
  - `DisposableEffect`: Runs when the Composable enters Composition and cleans up when removed.
  ```kotlin    
    LaunchedEffect(userId) {
      fetchUserData(userId)  // Called when `userId` changes
    }
    DisposableEffect(Unit) {
        val sensor = startSensorListener()
        onDispose { stopSensorListener(sensor) }  // Cleanup when removed
    }
  ```
  - `derivedStateOf`: ensures that expensive calculations only run when dependent value change, instead of triggering recompositions unnecessarily.
  ```kotlin
    var text by remember { mutableStateOf("") }
    var isValid by remember { derivedStateOf {text.length > 5}}
    //without derivedStateOf, isValid would be recalculated on every recomposition.
  ```
- `Side EfFect`: A side effect in Jetpack Compose is any operation that affects or interacts with the outside world and is not directly related to UI rendering, like network call, logging, database write.
  - Types of Side Effects:
    - `One-time side effects`: These should only run once when a composable appears. `LaunchedEffect(Unit)` ensures logging runs only when the composables first enters composition.
    - `Continour Effect`: When side effect depend on a changing state, they should re-run when that state updates. `LaunchedEffect(userId)` will rexeucte whenever userId changes, ensuring fresh data.
    - `Continous Listening`: When continiously collecting from `StateFlow` or `SharedFlow`, use collectAsState or LaunchedEffect. CollectAsState() is for UI state, while LaunchedEffect is for one-time event handling.
- `Optimization Techniques for Recomposition`:
  - `Key-Based recomposition control`: Using keys to control which parts of the UI are preserved during recomposition.
  - `Stable Types and Immutability`: Using immutable data classes with stable equals() implementation reduces recompositions.
  ```kotlin
    @Immutable
    data class User(val name: String, val age: Int)

    @Composable
    fun UserProfile(user: User) { /* Won't recompose unnecessarily */ }
    //using immutable prevents unncessary recompsitions.
  ```
  - `derivedStateOf for computed properties`: When a state computation is expensive or shouldn't trigger recomposition on every intermediate value.
  - `SideEffect for Non-compose operations`: Use SideEffect for operations that should happen on every successful recomposition.
  - `LaunchedEffect for lifecycle-aware corotuines`: Run suspending operations safely with the composition lifecycle.
- `When is composable destroyed`:
  - When it is no longer needed in the UI like navigating to another screen.
  - It's parent composable is removed.
  - A condition inside `if` causes it to disappear.
- `Unidirectional Data Flow (UDF)` : Desing pattern in which state *flows down* and events *flow up*. By using UDF, we can decouple composables that **display state** in the UI from the parts of your app that **store and change state**.
- Jetpack Compose supports other observables types also. But before reading another observable type in Jetpack Compose, you must convert it to a `State<T>` so that Compose can automatically recompose when the state changes.
  - `Flow` : *collectAsStateWithLifecycle()* collects value from a flow in lifecycle-aware manner, allowing app to save unneeded app resources and tranforms it into Compose State. (*collectAsStateWithLifecycle() uses *repeatOnLifecycle* API under the hood, which is the recommended way to collect flows in Andorid using the View system.)
  - `Flow` : *collectAsState()* similar to *collectAsStateWithLifecycle()*. Use *collectAsState* for platform-agnostic code instead of *collectAsStateWithLifecycle()*, which is android-only.
  - `LiveData`: *observeAsState()* starts observing the LiveData and represents its values via State.
  - `RxJava2` : *subscribeAsState()* are extension functions that transform RxJava2's reactive streams into Compose State.
  - `RxJava3` : *subscribeAsState()* same as above.
