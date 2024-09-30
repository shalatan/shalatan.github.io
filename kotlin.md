# Kotlin

## <a name='Tableofcontents'></a>Table of contents
<!-- vscode-markdown-toc -->
* [Table of contents](#Tableofcontents)
* [Topics](#Topics)
	* [Advantages Over Java](#AdvantagesOverJava)
	* [Basics](#Basics)
	* [Keywords](#Keywords)
	* [Visiblity Modifiers](#VisiblityModifiers)
	* [Classes](#Classes)
	* [Constructors](#Constructors)
	* [Functions](#Functions)
	* [Scopes Functions](#ScopeFunctions)
* [Questions](#Questions)
* [DSA](#DSA)
	* [Tips](#Tips)
	* [String](#String)
	* [Arrays](#Arrays)
	* [Matrix](#Matrix)
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
    - Safe call (?.):  Safe calls allow you to safely access properties and methods on nullable objects without risking an NPE. If the object is null, the call returns null instead of throwing an exception.
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
      val a = if (b!=null) b else "defaultValue"
      ```
    - Not null assertion Operator(!!): promising that the value will not be null, but if found null, will cause null pointer exception

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
  - `cont val` : makes val compile time constant, hence must be known at compile time
  - `open` : make the class open for inheritance by other classes as classes are final by default in kotlin.
  - `when` : substitute for the *switch case* of java
    ```kotlin
    when(a){
      in 1..10 -> println("Value Less Than 10")
      in  11..100 -> println("Value More Than 10")
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
  - `nested class`: Class inside another class, but by default nested class don't have access to members of the outer class.
  - `inner class`: makes the members of outer class accessible by the nested class by adding the inner keyword to nested class.
  - [⭐](#interview-questions)
    `data classes` : used to store values, data. Generates equals(), hashCode(), copy(), toString() automatically, which can be overriden.
    ```kotlin
    data class User(val name, val string)
    ```
    cons: 
    - Can't be inherited, but can inherit.
    - a data class may have properties that are not part of its constructor, they will not be regarded in any of the functions that are generated.
    ```kotlin
    data class DollarBill(val amount: Int) {
        var serialNumber: String? = null
    }
    ```
  - `enum classes` : used to model types that represent a finite set of distinct values
    ```kotlin
    enum class SchnauzerBreed(val height: Int) {
        MINIATURE(33),
        STANDARD(47),
        GIANT(65);

        val family: String = "Schnauzer"
        fun isShorterThan(centimeters: Int) = height < centimeters
    }
    
    println(SchnauzerBreed.STANDARD.family)             // Prints "Schnauzer"
    println(SchnauzerBreed.STANDARD.isShorterThan(40))  // Prints "false"
    ```
    - Built-in properties offered by enum:
      - ordinal: position of item in list
      - name: 
  - `abstract classes` : Abstract classes can be extended by other classes. Their functions and properties can be:
    - `abstract`, in which case they have no body in the abstract class, but subclasses must implement them.
    - `open`, in which case they have a body in the abstract class, but subclasses may override them.
    - `Final` (i.e., neither abstract nor open), in which case subclasses cannot override them.
  - `open classes` : An open class is a class that can be both extended and instantiated directly. Open classes cannot contain abstract members.
  - `sealed classes` : A sealed class is, by definition, also an abstract class. This means that you can’t directly instantiate it - you can only instantiate one of its subclasses.
  Hence, if you want exhaustive subtype matching, you’ll need to include the sealed modifier. ***If you need to limit values, then use an enum class. If you need to limit types, then use a sealed type.***
  <br>OR<br>
  A sealed class is a class that restricts which other classes can inherit from it. All subclasses must be declared within the same file as the sealed class itself.
  ```kotlin
  sealed class Shape {
    class Circle(val radius: Double) : Shape()
    class Rectangle(val width: Double, val height: Double) : Shape()
    object NotAShape : Shape()
  } 
  ```
  - Benefits of sealed class:
    - `Restrictive Inheritance`: All subclasses of a sealed class are known at compile-time.
    - `Exhaustive when Expressions`: When using `when` expressions with sealed classes, Kotlin ensures that all possible subclasses are handled, leading to safer and more maintainable code.
[ref](https://www.youtube.com/watch?v=KvehHqnEXuc&ab_channel=DaveLeeds)

### <a name='Reference Equality'></a>Reference Equality
[🔝](#table-of-contents)
- `reference equality`: when two variables refer to same object instance, then they will be considered equal.
- `value equality`: when objects are considered equal based on their property values rather than their identity
- `referential equality operator` : Even when you override the equals() function to give a class value equality, you can still check to see whether two variables refer to the same instance.
```kotlin
//reference equality
class DollarBill(val amount: Int)
val bill1 = DollarBill(5)
val bill2 = DollarBill(5)
println(bill1 == bill2) // false

//value equality
class DollarBill(val amount: Int) {
    override fun equals(other: Any?) =
        if (other is DollarBill) amount.equals(other.amount) else false
}
println(bill1 == bill2) // true

//referential equality operator
println(bill1 == bill2) // false
```

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

- `Higher Order Functions` : Functions the either takes function/LE as parameter, or returns a function/LE

```kotlin
//this is hof because it takes function as parameter
fun calculateTotal(initialPrice: Double, applyDiscount: (Double) -> Double): Double {
  val priceAfterDiscount = applyDiscount(initialPrice)
  val total = priceAfterDiscount * taxMultiplier
  return total
}

//this is hof because it returns a function
fun discountForCouponCode(couponCode: String): (Double) -> Double =
  when(couponCode) {
  "FIVE_BUCKS" -> ::discountFiveDollars
  "TAKE_TEN" -> ::discountTenPercent
  else -> ::noDiscount
}
```

- `Lambda` : Lambda expression is nothing but simplified representation of function aka function literals, which can be passed as parameter, stored in a variable, even returned as a value.

```kotlin
val applyDiscount: (Double, Double) -> Double = { price: Double, discount: Double -> price - discount }
// opening braces - paramters - arrow - function body - closing braces

//Lambdas with multiple statements 
//In Kotlin, writing the lambda outside of the parentheses like this is called trailing lambda syntax.
val withFiveDollarsOff = calculateTotal(20.0) { price ->
    val result = price - 5.0
    println("Discounted price: $result")
    result          //result of function, without return keyword
}
```

- `Anonymous Function` : Because lambdas have no name, many languages regard lambdas as Anonymous Function but in Kotlin the term anonymous function refers to another way of writing the function literal.
```kotlin
val applyDiscount: (Double) -> Double = 
  fun(price: Double): Double { return price - 5.0 }
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
- `Scope` : Section of code where you can declare or use any particular varibale or function.
  - `Statement Scope` : You can only use something that was declared in a statement scope after the point where it was declared.
  ```kotlin
  fun circumference(): Double {
        fun diameter() = radius * 2     //right
        val result = pi * diameter()
        fun diameter() = radius * 2     //wrong
        return result
    }
  ```
  - `Declaration Scope` : Unlike statement scopes, things declared within a declaration scope can be used from a point in the code either before or after that declaration.
  ```kotlin
  class Circle(val radius: Double) {
    val circumference = pi * diameter()
    fun diameter() = radius * 2
  }
  ```
- `Scope Functions` : Functions whose sole purpose is to execute a block of code within the context of an object. When called with a lambda expression provided, a temporary scope is formed, inside which we can access the object without its name.
The point of a scope function is to take an existing object - called a *context object* - and represent it in a particular way inside that new scope.
  - `with` : introduces a new scope (the lambda) in which the context object is represented as an **implicit receiver** (an implicit receiver can be used with no variable name at all)
  ```kotlin
  //before
  address.street1 = "9801 Maple Ave"
  address.street2 = "Apartment 255"
  //after
  with(address){
    street1 = "9801 Maple Ave"
    street2 = "Apartment 255"
  }
  ```
  - `run` : works same a `with` but it's an extension function instead of a normal, top-level function. As it's a extension function, it can be inserted into a call chain. The run() function returns the result of the lambda.
  ```kotlin
  address.run {
    street1 = "9801 Maple Ave"
    street2 = "Apartment 255"
  }
  val title = "The Robots from Planet X3"
  val newTitle = title
    .removePrefix("The ")
    .run { "'$this'" }
    .uppercase()
  ```
  - `let` : very similar to `run()`, but instead of representing the context object as an implicit receiver, it’s represented as the parameter of its lambda.
  ```kotin
  val newTitle = title
    .removePrefix("The ")
    .let { it -> "'$it'" }
    .uppercase()
  ```
  - `also` : As with let(), the also() function represents the context object as the lambda parameter, too. However, unlike let(), which returns the result of the lambda, the also() function returns the context object. This makes it a great choice for inserting into a call chain when you want to do something “on the side” - that is, without changing the value at that point in the chain.
  ```kotin
    val newTitle = title
      .removePrefix("The ")
      .also { println(it) }
      .uppercase()
  ```
  - `apply` : Like *also()*, the apply() function returns the context object rather than the result of the lambda. However, like run(), the apply() function represents the context object as the implicit receiver.
    ```kotin
    val newTitle = title
      .removePrefix("The ")
      .apply { println(this) }
      .uppercase()
  ```
  |       |Context|Return |Use Case|
  |---    |---    |---    |---        |
  |`with` |this   |lambda |Grouping Function calls on an object|
  |`run`  |this   |lambda |Object Configuration and computing the result|
  |`let`  |it     |lambda |Null Safety Calls|
  |`also` |it     |context|Addtional Effects|
  |`apply`|this   |context|Object Configuration|
<br>

  [which one to use and when](https://typealias.com/img/start/scopes-and-scope-functions/scope-function-flow-chart.png)

  - Scope functions and Null Check: Other than *with()*, all other scope functions are extension functions, hence we use safe-call operator when calling them, so that they are not called when the receiver is not null.
  ```kotin
  if (payment != null) {
    orderCoffee(payment)
  }
  payment?.let { orderCoffee(it) }
  payment?.let { orderCoffee(it) } ?: println("value null")
  ```

## <a name='Questions'></a>Questions

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

### <a name='Tips'></a>Tips
- `Find number of digits in number`: (Math.log10(num))

### <a name='String'></a>String
```kotlin
var str = "KOTLIN"

str.size    //5

//iterate string
for(char in str)
```

### <a name='Arrays'></a>Arrays
- `Array<Int>` is an Integer[], means it will be boxed with Integer.parseInt()
- `IntArray` is an int[], in it no boxing will occur, becuase it translates to Java primitive array.
    - val arr = IntArray(10)
    - 
```kotlin
val arr = intArrayOf(1,2,3,4,5)
var arr = IntArrya(10)
var arr = IntArray(5) {0}   // {0,0,0,0,0}

arr.size    //4
```

### <a name='Matrix'></a>Matrix
```kotlin
//declare two dimensional array
var matrix = Array(2) { Array<Int>(2) {0} }
println(matrix.contentDeepToString())
: [[0,0],[0,0]]

//declare three dimensional array
var matrix = Array(3) { Array(3) { Array<Int>(3) {0} }}
println(matrix.contentDeepToString())
: [[[0, 0, 0], [0, 0, 0], [0, 0, 0]], [[0, 0, 0], [0, 0, 0], [0, 0, 0]], [[0, 0, 0], [0, 0, 0], [0, 0, 0]]]
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
//increase the count by 1 if present, else insert
map.put(num,(map.get(num)?:0)+1)
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