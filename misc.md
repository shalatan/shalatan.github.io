# Misc

<!-- vscode-markdown-toc -->
- [Misc](#misc)
  - [Topics](#topics)
    - [Time Complexity](#time-complexity)
    - [Bitwise Operators](#bitwise-operators)
  - [Misc](#misc-1)
    - [Gradle](#gradle)
    - [Git](#git)
    - [Heroku](#heroku)

<!-- vscode-markdown-toc-config
	numbering=false
	autoSave=true
	/vscode-markdown-toc-config -->
<!-- /vscode-markdown-toc -->
  
## <a name='Topics'></a>Topics

### <a name='TimeComplexity'></a>Time Complexity
> *Time Complexity != Time taken* <br> Time complexity is a function that gives us the relationship about how the processing time will grow as the input grows
- Procedure for analysing complexity
  1. Look for **worst case** complexity
  1. Look at complexity for large/infinte data
  1. Ignore the constants
  1. Ignore less dominating terms
- Notations
  1. Big Oh: Upper bound
  1. Big Omega: Lower bound
  1. Theta: When both upper and lower bounds are same


### <a name='BitwiseOperators'></a>Bitwise Operators

- Operators
  - AND
    |a|b|a&b|
    |-|-|--|
    |0|0|0|
    |0|1|0|
    |1|0|0|
    |1|1|1|
    > When you &1 with any number, digits remain same
  - OR
    |a|b|ab|
    |-|-|--|
    |0|0|0|
    |0|1|1|
    |1|0|1|
    |1|1|1|
  - XOR (^)
    |a|b|a^b|
    |-|-|--|
    |0|0|0|
    |0|1|1|
    |1|0|1|
    |1|1|0|
    > When you ^1 any number, it's reverse: 1^1 = 0 <br>
    > When you ^0 any number, it's same: a^0 = a<br>
    > When you ^a any number, it's 0: a^a = 0
  - Complement (~)
  - Left Shift (<<): Shifts the bits one left
    10 = (1010) becomes (10100) = 20
    > Doubles the number, a << 1 = 2a<br>
    > Generalized as, a << b= a*2^b
  - Right Shift (>>): Shift the bits one right
    001101 becomes 001100
    > Halves the number, a >> b = a/(2^b)
- Questions
  1. Check if number is prime?
    If last bit is 0 -> even, 1 -> odd
    As, 1&1=1, hence n&1 == 1 -> odd else even
  

## <a name='Misc'></a>Misc

### <a name='Gradle'></a>Gradle
**Gradle is a build tool that we use for Android development to automate the process of building and publishing apps.**
<br>
- When we click on *Run* button, it exceutes multiple built-in tasks like:
  1. reads app's build configuration file (build.gradle)
  2. downloads and resolves the app's dependencies
  3. compiles the apps code, including converting java and kotlin files into bytecode
  4. packs the compiled code and resources into an APK
  5. installs the APK file on the device and runs the app
- `DSL`: Gradle comes with lot of built-in functionalities, but we can write our own logic too using DSL (domain specific language), which is tailored to build automation domain based on Groovy or Kotlin.

### <a name='Git'></a>Git

- Git Commands
  - `git init` : initialize a empty git
  - `git status` : shows all the changed files
  - `git add .` : add all the files/changed files
  - `git commit -m "message"` : commit the changes with message

### <a name='Heroku'></a>Heroku

- Heroku CLI Commands
  - `heroku login`
  - `heroku create` : create a new app
  - `git add .` -> `git commit -m "message"` -> `git push heroku master` : deploy the latest code
  - `heroku open` : open the app
  - `heroku logs` --tail : get logs