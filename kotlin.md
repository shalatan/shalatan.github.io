## <a name='Kotlin'></a>Kotlin

## <a name='Tableofcontents'></a>Table of contents
<!-- vscode-markdown-toc -->
* [Kotlin](#Kotlin)
* [Table of contents](#Tableofcontents)
* [Topics](#Topics)
	* [Advantages Over Java](#AdvantagesOverJava)
	* [Basics](#Basics)
	* [Keywords](#Keywords)
	* [Visiblity Modifiers](#VisiblityModifiers)
	* [Classes](#Classes)
	* [Constructors](#Constructors)
	* [Functions](#Functions)
	* [Scope Functions](#ScopeFunctions)
* [DSA](#DSA)
	* [Arrays](#Arrays)
	* [HashSet](#HashSet)
	* [HashMap](#HashMap)
	* [Loop](#Loop)

<!-- vscode-markdown-toc-config
	numbering=false
	autoSave=true
	/vscode-markdown-toc-config -->
<!-- /vscode-markdown-toc -->

## <a name='Topics'></a>Topics

### <a name='AdvantagesOverJava'></a>Advantages Over Java
[🔝](#table-of-contents)

  - `Data Class`
  - `Extension Functions`
  - `KMM`
  - `Concise Code`
  - `Support for Null Safety`: Kotlin provides Safe Call (?.), Elvis (?:) and Not Null Assertion (!!) operators which define what needs to be done in case of a null encounter.
    - Safe call (?.):  Operator that simplifies things by only doing an action when the specified reference holds non-null value.
        ```kotlin
        name?.toLowerCase()
        OR
        if(name!=null) name.toLowerCase()
        else null
        ```
    - Elvis Operator(?:): Operator used to return a non-null or default value. It returns the left value if it's not null, otherwise returns the right value.
        ```kotlin
        val a = b ?: "defaultValue"
        OR
        val a = if (b!=null) b
                else "defaultValue"
        ```
    - Not null assertion Operator(!!): 

### <a name='Basics'></a>Basics
[🔝](#table-of-contents)

  - `?:` : *Elvis Operator*, for safe call, unwraps the value from Nullable 
  - `!!` : value will not be null, if null will cause runtime crash
  - `==` : check if values are equal or not
  - `===` : check if reference is equal or not
  - `init` : it is the initialiser block in Kotlin, it's executed once the primary constructor is instantiated.

### <a name='Keywords'></a>Keywords
[🔝](#table-of-contents)

  - `var` : variable value can be changed
  - `val` : variable value cannot be changed, sets at runtime
  - `cont val` : makes val compile time constant
  - `open` : make the class open for inheritance by other classes as classes are final by default in kotlin.
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

### <a name='VisiblityModifiers'></a>Visiblity Modifiers
- `public`: default visibility modifier, are accessible everywhere, both, within and outside the module.
- `internal`: visibile only within the same module
- `protected`:  allows a declaration to be accessible within the same class and its subclasses.
- `private`: only visible within the scope where they are declared.

### <a name='Classes'></a>Classes
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

### <a name='Constructors'></a>Constructors
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
### <a name='Functions'></a>Functions
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

### <a name='ScopeFunctions'></a>Scope Functions
[🔝](#table-of-contents)[⭐](#interview-questions)

Functions whose sole purpose is to execute a block of code within the context of an object. When called with a lambda expression provided, a temporary scope is formed, inside which we can access the object without its name.
  |       |Context|Return |Use Case|
  |---    |---    |---    |---        |
  |`let`  |it     |lambda |Null Safety Calls|
  |`with` |this   |lambda |Grouping Function calls on an object|
  |`run`  |this   |lambda |Object Configuration and computing the result|
  |`apply`|this   |context|Object Configuration|
  |`also` |it     |context|Addtional Effects|

## Questions

- How to concatenate two strings in Kotlin? 
  - Using String Interpolation: 
  - Using + or plus() operator:
  - Using StringBuilder:
  ```kotlin
  val a = "dsa"
  val b = "algorithm"
  val si = "$a $b"
  val p1 = a+b
  val p2 = a.plus(b)
  val sb = StringBuilder().append(a).append(b).toString()
  ```

## <a name='DSA'></a>DSA

### Tips
- `Find number of digits in number`: (Math.log10(num))

### String
```kotlin
var str = "KOTLIN"

str.size    //5
```

### <a name='Arrays'></a>Arrays
- `Array<Int>` is an Integer[], means it will be boxed with Integer.parseInt()
- `IntArray` is an int[], in it no boxing will occur, becuase it translates to Java primitive array.
    - val arr = IntArray(10)
    - 
```kotlin
val arr = intArrayOf(1,2,3,4,5)

arr.length    //4
```

### <a name='HashSet'></a>HashSet
```kotlin
var hashSet = hashSetOf<Int>()
var hashSet = hashSetOf<Int>(1,2,3,4,5,6)
var hashSet: HashSet<String> = hashSetOf<String>()
val mySet = setOf(6,4,29)

// putting into hashSet
hashSet.add(item)
hashSet.addAll(mySet)

// checking
hashSet.contains(item)
hashSet.containsAll(mySet)

// removing
hashSet.remove(item)
hashSet.removeAll(mySet)

// traverssing hashSet
for(item in hashSet){

}

// misc
hashSet.isEmpty()
hashSet.isNotEmpty()
hashSet.clear()
hashSet.size
```

### <a name='HashMap'></a>HashMap
```kotlin
var hashMap: HashMap<String,Int>= HashMap<String,Int>()

// printing hashmap
print(hashMap)

// putting into hashmap
hashMap.put("IronMan", 3000)
hashmap["IronMan"] = 3000
hashMap.replace("IronMan",99) // for updating

// getting from hashmap
hashMap.get(key)

// traverssing hashmap keys
for(key in hashmap.keys){

// misc
hashMap.size
hashMap.isEmpty()
hashMap.clear()
hashMap.containsKey(key)
hashMap.containsValue(value)
hashMap.remove(key)
}
```
### <a name='Loop'></a>Loop
```kotlin
- val nums = {1,2,3,4,5}
- for(num in nums) l̥
    : 1,2,3,4,5
- for(i in nums.indices)
    : 0,1,2,3,4
- for(i in 1..5)
    : 1,2,3,4,5
- for(i in 5 downTo 1)
    : 5,4,3,2,1
- for(i in 1..5 step 2)
    : 1,3,5

- val text = "kotlin"
- for(letter in text)
    : k,o,t,l,i,n
- for(i in text.indices)
    : 0,1,2,3,4
```