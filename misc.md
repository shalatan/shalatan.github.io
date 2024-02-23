# Misc

<!-- vscode-markdown-toc -->
* [Topics](#Topics)
	* [Time Complexity](#TimeComplexity)
	* [Bitwise Operators](#BitwiseOperators)
* [Misc](#Misc)
	* [Git](#Git)
	* [Heroku](#Heroku)

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