# JavaScript

## Execution Context
  - Everything in the javascript happens inside an Execution Context.
  - It can be considered as a container in which whole javascript code is executed.
  - It has 2 components in it.
      1. Memory Component
        - It is the place where the variables and functions are stored in the form of key-value pairs.
        - It can be also known as **Variable environment**.
      2. Code Component
        - It is the place where our code is executed line by line as it is single-threaded.
        - It can be also known as **Thread of Execution**.
### JavaScript is a Synchronous Single-Threaded Language.
  - As it is a single-threaded language, js can execute only one command at a time.
  - Synchronous single-threaded means that js can execute one command at a time and in a specific order which means it will only go to the next line if it executed the current line.


## What happens when we run js code?
  - When we run a javascript code, a **global execution context** is created with memory and code component and it will be deleted after complete execution of the js program.
  - And this execution context is created in two phases.
    1. **Memory Allocation Phase (Creation phase)**
      - In this phase, js will goes through the program line by line and allocates memory to all the variables and functions in the code.
      - When a variable is created or allocated with memory, the value of the key(variable name) will be undefined.
      - When a function is allocated with memory, the value of that function name(key) will be the entire code in that function.
    2. **Code Execution Phase**
      - Now, js once again runs through the entire program again and executes line by line.
      - This is the phase where calculations and operations are done in the program.
      - In this phase, the variables which are assigned with undefined in the 1st phase are assigned with their value specified in the program.
      
      
      - The functions will not be executed directly until they have been called or invoked.
      - When the *function is called*, a *new execution context is created* which again consists of memory and code components. And it also contains the memory creation phase and the code execution phase.
      - When the return statement is encountered in the function, it takes the value of the variable in the return statement from the local memory of the function execution context and it returns the control back to the place in the main execution context(parent) where the function the is called.
      - And the **whole execution context of the function is deleted after the control coming to the main execution context**. It means when we call the same function another time again the new execution context is created and the same process is repeated.
     

### Call stack
  - It is a stack that is populated when a program is executed.
  - By using this, javascript is working and managing with all the execution contexts it created.
  - Every time in the bottom of the stack, the global execution context is populated.
  - When a function is invoked a new execution context is put into the stack and control is now to the top of the stack i.e., the function's execution context.
  - After the function returns the value to the global execution context, that function is popped from the call stack and the control goes back to the global execution context (as it is the top element in the stack now).
  - After the complete execution of the js program the global execution context is also popped out from the call stack.

  - Therefore, we can see that the **Call Stack** is the one that **Maintains the order of execution of the Execution Contexts**.
  - _Call Stack_ is also known as 
    - _Execution Context Stack_
    - _Program Stack_
    - _Control Stack_
    - _Runtime Stack_
    - _Machine Stack_
    
## Hoisting
- Hoisting is the mechanism in js through which we can access the variables and functions in the program even before initialising them or even before the lines of declaring those variables and functions without any error.
- In js even before the js code starts executing, the memory is allocated to variables and functions.
(As seen above in the memory allocation phase of the js)

### Not-Defined vs Undefined
- **Not defined** means the variable is not in the memory which means not declared anywhere.
- **Undefined** means the variable is in the memory which means declared somewhere in the program but till now or till this point it is not initialised as while keeping in the memory in the **Memory allocation phase** js will keep the variable in the memory by specifying a special value called undefined.

### Functions types and their behaviour
- In the case of the **Normal Functions or Proper Functions**, they are defined somewhere in the program code with the _keyword function_, so the js will load the entire function code into the memory in the **Memory Execution Phase** itself. So even before the line, it declared we can access or call the function directly.
- In the case of the **Arrow Functions or Anonymous Functions assigned to Variable**, they are defined somewhere in the program code like _variable which is assigned with function_. So js will load the _variable_ into the memory with specifying as undefined instead of the entire function code because here the arrow function is assigned to some variable.


## Shortest JS Code is an Empty JS File
- Even we don't write a single line of code in the js file, it will run.
- When we execute that empty js file, the global execution context will be created along with the memory space by the js engine even there is nothing to do externally in the file.

### JS engine
- Different browsers or environments use different engines to run the js.
- Chrome uses the v8 js engine to run the javascript.
- Firefox uses Spider Monkey js engine
- Chakra Jscript engine is used in edge
- These engines have a responsibility to create this global object, incase of browsers it is known as _window_, in case of node some other object(called global), and wherever you run the code the js program it is different but there will be a global object created.
- And also creates some objects and keywords. Like
### window object
- Which contains a huge collection of methods and variables related to the window.
- window objects can be used from anywhere globally.
- Its a global object which will be created along with global execution context when we run any program.

#### this variable
- Along with the window object while creation of global execution context, the js engine creates a _this_ variable.
- It will points to the window object while the global execution context creation time itself.
- At global level, this===window is true.

#### Whenever you create any variables in the global space (not in any functions) they are attached to that global object (_window_ in the browser). 
#### Whenever we try to access any variables or function without any objects (which are declared globally) then the js engine assumes implicitly that it is in the global space.
```
var a=10;
console.log(a);
console.log(window.a);
console.log(this.a);
```
- All the above 3 console statements result in the same.

## Scope Chain, Scope & Lexical Environment
- As we discussed above, all the variables declared in global space will have the scope and can be accessed within the inner functions also.
```
  function a(){
    console.log(b) // prints 10
    function c(){
      console.log(b) // prints 10
    }
    c()
  }
  var b = 10
  a()
  
```
- Here we have declared the b in a() as c() is within the a() it can access the variable b. But we cannot access the variable b outside the function a which pulls the scope into action.
```
  function a(){
    var b = 10
    console.log(b) // prints 10
    function c(){
      console.log(b) // prints 10
    }
    c()
  }
  a()
  console.log(b);
```
### Scope 
  - It means where can we access the specific variable or specific function in our code.

- So, let's look at the code.
- When we run our code, Initially a global execution context is created and pushed into the call stack and all the variables and functions in the global scope are allocated with the memory.
- Later while the function a is called, it will create another execution context, then memory is created for variable b and function c.
- After that the execution of code in the function begins, b is assigned with the value 10 and call function c.
- As function invoked, execution context for C is created and again the memory is allocated along with the code component.
### Lexical Environment
- Lexical (in a hierarchy or order) means where the specific code is physically present.
   Eg: From the above example, we can say that c is lexically inside function a & function a is lexically inside the global space.
- Wherever an execution context is created, a lexical environment is also created.
- Lexical Environment is the local memory along with the lexical environment of its lexical parent(where the current lexical env sits).
   Eg: From the above example, the lexical environment of the function c includes the local execution context memory and the parent lexical environment means the function a's execution context memory
   - In the same way, a lexical environment of function a  =  local execution context memory space + lexical environment of global execution context
   - In the case of the global lexical environment, the parent lexical environment points to null.
 Eg:
 - When we try to print the variable b, first js engine searches within the local lexical environment and as it is not found it will searches in the parent lexical environment through some reference to that and so on until it is found or the parent lexical environment is null.
 ```
  function a(){
    console.log(b) // prints 10
    function c(){
      console.log(b) // prints 10
    }
    c()
  }
  var b = 10
  a()
  
```
- In this below example, when we print the variable b in the global space outside the function a, then first it searches in the current global execution context lexical environment.
```
  function a(){
    var b = 10
    console.log(b) // prints 10
    function c(){
      console.log(b) // prints 10
    }
    c()
  }
  a()
  console.log(b);
```
- As it is not found, then it tries to search for the reference of the parent lexical environment of the global lexical environment but it is null. Therefore no more lexical environments.
- So as the js engine did not found b in the global and its parent, it declares and raises that the variable b is _not defined_ (not in the scope).

## Scope Chain
- The way/mechanism of the finding variable or functions through this chain of lexical environments and their parent references is known as Scope Chain.
- It is nothing but the chain of all these lexical environments and their parent references.
- Finally, the js engine first try to find the variable in the local lexical environment and if it is not found it moves up to the parent level of the scope chain.
- **Chain of the lexical environments is known as Scope Chain.**
- In browser *Scope* is the lexical environment.

## let & const vs var
- Generally, all the variables are hoisted despite whether they are declared with let/const/var.
- But in the memory allocation phase, memory will be allocated for let & const variables and also for var variables but the variables declared using var are attached to the Global object but the let/const is attached to some other memory space other than global.
- As the let and const variables are put in some other location than global, they cannot be accessed without assigning some value.
- These let/const variables will not be accessed with the window object.
### Duplicate Declaration
- Re-declaration of let/const variables is not allowed and raises syntax error (specifying identifier has already been declared) even before the start of program execution.
- But Re-declaration of var variables is permitted.

### let vs const
- Re-initialization/initialization after the declaration is possible in to incase of the let but incase of the const, re-initialization is not possible and also the value for the const variable should be given at the time of declaration itself.
- If we did not give value to const variable at the time of declaration, it will throw a syntax error saying that the initializer for the const variable is missing because the const syntax expects initialization & declaration at the same time.
- If we do not try to re-initialize or change the value of the const variable after declaration time, it throws Type Error: Assignment to a constant variable because const type variable can be reassigned.

### Reference error
- When the js engine tries to access the specific variable inside the memory space but it cannot access it then it raises a reference error.

**Whenever possible we need to use const then let or if needed we need to use var**


## Temporal Dead Zone
- The time between when the let/const variables are hoisted & till they are initialized with some value is called the Temporal dead zone.
- If we are trying to access those variables which are in the temporal dead zone we get a reference error specifying that **we cannot access variable before initialization**.
- This is a different error from the error which is caused if we try to access the variable which is not even declared anywhere in the program. (If it is not declared anywhere it will raise the reference error specifying **variable is not defined**).
- Moving all the declarations to the top of the code is the best way to avoid the temporal dead zone/shrink the temporal dead zone.

## Block Scope & Shadowing

### Block
- Block is also known as a compound statement.
```
{

}
```
- Block is used to group the multiple statements.
- This grouping of multiple statements is needed and can be used in a place where javascript expects a single statement.
Eg: Suppose if we take an if condition, it expects only a single statement.
i.e., we cannot write multiple statements directly under if condition. there comes the block to group the multiple statements as a single statement.
```
<!-- With Single statement -->
if() ....;
<!-- With Multiple Statements  -->
if(){
.........;
.........;
}
```

### Block Scope
- It means what all variables and functions that can be accessed inside a block are called Block Scope.
Eg:
```
{
  var a = 10;
  let b = 20;
  const c = 30;
}
```
- When we take the above example code and run it, we can observe that the b & c variables are hoisted at separate space called block scope.
- But a will be a global scope as we discussed variables declared with var always tied to the scope where they are declared.
- As here, it is not declared in any function and declared in the global execution context so it is hoisted to global space.
- And we can also check that even let and const are declared in the global execution context, but they are hoisted in a special space called block scope. So let and const variables are called block-scoped variables.
- Block scope also follows the lexical order, which means if we have nested blocks with same variable declared in each block and when we print the variable in some block, it will access the value of the variable from the nearest block. (i.e., checks in the current lexical environment and if it is not there then it will search in the parent lexical environment.)
```
const a = 20;
{
  const a = 100;
  {
    const a = 200;
    console.log(a); //200
  }
}
```
- Scopes for the normal functions and arrow functions is same.

### Shadowing in js
- Suppose if we have the same-named variable outside the block and also inside the block then the variable inside the block will shadow the variable which is outside the block.
- In the case of let and const, when the same variable with the same type of global scope is declared in the block, the value in the block will shadow the global variable until the end of the block scope. That means after the end of the block scope if try to print the value, it prints the value before shadowing i.e., the value in the global scope.
- Program
    ```
      let b = 200
      {
        var a = 10;
        let b = 20;
        const c = 30;
        console.log(a);//10
        console.log(b);//20
        console.log(c);//30
      }
      
      console.log(b);//200
    ```
    
- But in the case of var, along with shadowing the value, it will also modify the variable which is outside the block. 
- Let's see an example for a clear understanding
- Program
    ```
      var a = 200
      {
        var a = 10;
        let b = 20;
        const c = 30;
        console.log(a);
        console.log(b);
        console.log(c);
      }
      console.log(a);
    ```
 - Output
    ```
      10
      20
      30
      10
    ```
   - Here the variable a is declared inside the block and also outside the block. When we assign the variable a with value 10, it shadows its value to the var which is outside the block or in the global scope and also changes the value of var a. So that even we print the variable after the block ends we get the value as 10 due to shadowing.
   - This is happening because both are of type **" var"**, also with the same name and also as we discussed above the **var** type variables are attached to the global scope even though they are in the block. 
   - So, when the value of a is initially declared and assigned with 100, it will be allocated some memory space and attached to the global scope. And after when we are trying to create the same variable again in the block, it will also be attached to the global scope and due to the same name, the value will be shadowed and also replaced with the value 10.
 
- It is not only a concept of the block but also for the function and behaves in the similar way.

#### Illegal Shadowing
- If we are trying to redeclare a variable _in a block as let/const type variable_, which is already declared as _let/const type variable in the global scope_ then it accepts and works fine.
- But what if we are trying to redeclare a variable in a _block as var type variable_, which is already declared as _let/const type variable in the global scope_, then it raises an error that the particular variable is already been declared. 
- Because the boundary of the var is either function scope if it is declared in a function or global scope if it is anywhere other than the functions(may be in blocks). So, as the var type variables scope is entire the program, when we try to redeclare the let type variable as var type variable in a block scope, var type variable is trying to redeclare at the global scope which raising conflict with the existing let variable as let variables cant be redeclared.
- So, redeclaring of the let type variables as var type variables in the block (but not in the functions) cause the Illegal shadowing which cant be done.
- But reverse is possible. i.e., redeclaring the var type variable as let type variable in a block is possible as the let type variable is specific to that particular block, it will not cause any issue.

## Closures
- Closure is a function together bundled with its lexical environment.
- In simple terms,the function along with its lexical scope bundles together forms a closure.
- Lets get some clear understanding from the example.
```
function x(){
  var a = 7;
  function y(){
    console.log(a);
  }
  y()
}
x()
```
- When you executed this code, according to our previous knowledge of the lexical environments, we can predict that value 7 will be printed for the console log in function y. Here we understood that as the function is in y, while printing the variable a, it will search in the current function lexical environment and if it is not found then it will check at the parent lexical environment(in its global execution context) and prints the variable.
- And if you seriously observe in the browser, you can see that a new scope is present other than that of the global and local scope, which is a closure and in that we can see the variable a. This is created when the function y execution context is pushed into the call stack.
- This closure is nothing but the function and its corresponding lexical scope bundle (which means all the variables/functions used in that corresponding function).
- It means the value that is printed in the console is from closure as it is from the parent function lexical environment.
- This is so useful and lovely feature in javascript functions especially when returning the functions. i.e., when you return a function, the closure will be returned to the caller instead of the single function. 
- This makes us to access all the variables in the lexical scope of the function defination even they are not declared/initialized in the function.
- Lets see an example.
```
function x(){
  var a = 7;
  function y(){
    console.log(a);
  }
  return y
}
var z = x()
z()
```
- Here we are returning y then its assigned to z. Then how the value of a will be accessed according to our lexical environment concept? Its not accessible right? But its accessible when we call z because the z is a closure now, which contains the function bundled with its lexical scope(event its further parents variables also). That the beauty of js.
- This closures are more and more powerful concept of the js because these functions remembers things even when they are not in that lexical scope.
### Uses of closures
  -  Module Design pattern
  -  Currying
  -  Functions like "once"
  -  memoize
  -  maintaining state in async world
  -  setTimeouts
  -  Iterators
  -  and many more
- Closures are almost everywhere in the js.

## setTimeOut & Closures Interview Questions
->
  ```
  function x(){
    var i = 1;
    setTimeout(function(){
      console.log(i);
    },3000)
    console.log("Namaste JS");
  }
  x()
  ```
Output:
```
Namaste JS
1 (After waiting for 3 seconds)
```
- What happened is that, JS forms a closure of the function in the setTimeout and the setTimeout function will takes this callback function, attaches a timer to it and stores it somewhere.
- And continues to execute the remaining lines of the code without awaiting for the setTimeout.
- And later when that timer expires, js takes that function and again put it to the call stack & then runs it.

->
```
function x(){
  for(var i=1; i<=5;i++){
    setTimeout(function(){
      console.log(i);
    },i*1000);
  }
  console.log("Namaste JS");
}
x();
```
- Output
```
Namaste JS
6
6
6
6
6
```
- Its printing like this because, it is due to the closures.
- As the closure is a function along with its lexical environments, So even when the function is taken from its original scope, still it remembers its lexical environment.
- What happened here is that, when the js takes and stores this function somewhere by attaching a timer, it remembers the **reference** to the variable i not its value.
- So when the loop runs for the each time, it store/makes a new copy of the function (closure) which is in the setTimeout & attaches a timer along with remembering the reference that points to the i.
- Here, in this case all the functions that are created and stored are pointing to the **same reference of i because the var scope is global**.
- After storing, the js will completes the execution of loop quickly and doesnot wait for anything. So when the timer finishes, it will print/use the values of the remembered references at that particular point of time.
- Here its too late to print the value on the each iteration as their timer is too long, the js continues with remaining program. So, in this case after the completion of the timer all the functions prints the same.


- Here to fix it we can simply replace the variable i of type var with the variable i of type let.
```
function x(){
  for(let i=1; i<=5;i++){
    setTimeout(function(){
      console.log(i);
    },i*1000);
  }
  console.log("Namaste JS");
}
x();
```
Output:
```
Namaste JS
1
2
3
4
5
```
- This is because all the background process is done as same as above, which stores the functions in the each loop and that function remembers its reference to that variable in the loop but as here we used the variable type as let which is a block scoped variable, js will create a new copy of i each and every time in the loop, so while storing the function in each iteration, the callback function will point out to a new reference of i(different memory location), which means different reference of i with every function.

- So as we got some understanding, it all due to the maintance of single copy in each and every function right? so we seperated the copies with the let variables in a way that each function will point to a new copy of i as let is a block scoped.
- So, we can also do with var by maintaining a new of copy of the i in each iteration which will be pointed by the function in setTimeouts.
- So for that, what we can do is by using the concept of closures.
```
function x(){
  for(let i=1; i<=5;i++){
    function close(j){
        setTimeout(function(){
          console.log(j);
        },j*1000);
     }
     close(i);
  }
  console.log("Namaste JS");
}
x();
```
- Here, we wrapped the setTimeout function inside a new function and calling that function close by passing the value of i.
- Above approach will works because, every time when we called that close function with the i, it creates a new copy of i for itself.
- So, by using this close function, we kind of created a new copy of x with the current value of the i in that iteration.

- Or the below code also works fine.
```
function x(){
  for(let i=1; i<=5;i++){
    let j = i
    setTimeout(function(){
      console.log(j);
    },j*1000);
  }
  console.log("Namaste JS");
}
x();
```
Output:
```
Namaste JS
1
2
3
4
5
```
- ```
  function outest(){
    var c=20;
    function outer(b){
      function inner(){
        console.log(a,b,c);
      }
      let a = 10
      return inner
    }
    return outer
  }
  let a = 100
  var close = (outest())("helloworld")
  close(); // 10 "helloword" 20
```
- *Closure in the sense the function binded with its lexical environment which includes all the below lexical environments in the callstack.*
- Closures can be used to have dataprivacy or data hiding which means hiding or making the data invisible to other functions which are accessing it by encapsulating the data along with the functions.
- Eg: When we wanted to implement the counter and make no one accessible to the counter variable directly without that function. Then by using closures, we can acheive it.
```
function counter(){
  var count = 0;
  function incrementCounter(){
    count++;
    console.log(count);
  }
  return incrementCounter;
}

// If we want to access the count outside, without using that function then it raises as count not defined
console.log(count); //error as not defined

// Instead we need to call the counter
var counter1 = counter();
counter1(); // 1
counter1(); // 2

// We can create as many ass instances as we want. i.e., a new closure is called and starts from the initial state.
var counter2 = counter();
counter2();
counter2();
counter2();
```

## Function Constructor in js
- Its a normal function but by using the *this* object to initialize or declare the functions and variables makes it as scalable and use like a class.
```
function Counter(){
  var count = 0;
  this.incrementCounter = function(){
    count++;
    console.log(count);
  }
  this.decrementCounter = function(){
    count--;
    console.log(count);
  }
  
}
<!-- Initializing the constructor -->
<!-- As it is a constructor function we need to initialize object using a new keyword -->
var counter1 = new Counter();
counter1.incrementCounter(); // 1
counter1.incrementCounter(); // 2
counter1.decrementCounter(); // 3
```
- This constructor function also follows the concept of closures.

## Disadvantages of Closures
- There is a chance of Overconsumption of the memory due to closures. Because, when everytime a closure is formed, it consumes a lot of memory and those closed over variables (which are used by closures) are not garbage collected.
- It means if we use a lot of closures it may leads to accumalate of the memory which leads to memory leaks and slows down the browser.

## Garbage Collector in Javascript
-  Its like a program in the js engines of the browser, which frees up the unwanted or unused memory when the js engine finds that they are not used anymore/ no longer needed.
Eg:
- ```
function a(){
  var x = 0;
  return function b(){
    console.log(a);
  }
}
a();
```
  - Here when we called a, the variables and functions in that a are created and after the execution of the function a, they are garbage collected in this case.
- But if we use some closures in this function a,
- 
```
function a(){
  var x = 0;
  return function b(){
    console.log(x);
  }
}
var y = a();
```
- Here x is refered in the inner function which closed over x and forms a closure and it is returned outside the function, then in this case the js engine cant directly clean/freeup the space of variable x because it is referenced in the other function until unless it confirms that all the usages of it are completed.
- But in some modern browsers like chrome v8 engines, they finds out the unreacheable variables and smartly collects the garbage variables.
- Smartly collects in the sense, when there is some code like this
```
function a(){
  var x = 0, z=10;
  return function b(){
    console.log(x);
  }
}
var y = a();
```
```
y();
```
- When we called the function y() (the closure b which contains the referenc to both x and z but only x is used in the function b), and its execution is completed x will be still accessible because y is still present in the scope. But when comes to z which is not used the function y it will be smartly garbage collected by modern browser js engines.

## Function Statement aka Function Declaration
- The below way of creating a function is called Function Statement.
```
function a(){
 console.log(1);
}
a();
```
## Function Expression 
- The below way of creating a function is called Function Expression.
```
var b = function(){
console.log(2);
}
b();
```
## Difference b/w Function Statement and Function Expression
- The difference is hoisting.
- During the memory creation phase, the function created in the way of *function statement* is treated as an *function* but the function created in the way of *function expression* is treated as an *variable*.
- After in the code execution phase, the function is assigned to the variable, till then its a variable assigned with some undefined, in case of function expression.
- That means by considering above examples of function statement and expression, a can be called before the lines of function code but b cannot be called before its initialization and will cause error mentioning that *b is not a function* if we call 'b' before the initialization.

## Anonymous function
- Functions without name is an Anonymous function.
- These functions does not have their identity means that they cant be called directly unless it is assigned to some variables as function expression
```
// Below is a anonymous function but using directly as below causes an error saying that function statements require a function name.
function(){
}

// Below is valid
var b = function(){
}
```
- Anonymous functions are used when they are used as values.

## Named Function Expression
- The below way of function is a named function expression.
```
var b = function xyz(){
console.log(2);
}
b();
- We can call the function using variable name b but we cant use the function with the name xyz from outside the function.(Means, xyz can be used inside of that function itself like below)
var b = function xyz(){
console.log(2);
xyz();
}
```

## Difference b/w parameters and arguments
- Parameters are the names used in the function defination.
- Arguments are the values(may be functions,numbers,other variables etc..) that we pass to the function in the time of calling it. 
```
function c(param1, param2){
<!-- Params are local scoped in this particular function -->
 console.log(param1+param2);
}
c(3,4)
```
## First Class Functions / First class citizens
- It is a programming pattern.
- The ability of the functions to use them as values is called first class functions
- Functions can be used as a value for assigning a variable, can be passed into another functions, returned out of another functions.
- Above all are the examples.

## Callback Function
- It is a function passed as an argument in another function.
- Due to this callback functions, javascript which is a synchronous and single-threaded language is able perform async operations efficiently.
```
function x(y){

}
x(function y(){
  
})
<!-- y is the callback function here -->
```
- The function y in the above example can be called back at some time in the function x, so it is called as callback function.

```
setTimeout(function(){
  console.log("Timer")
},5000)

function x(y){
console.log(x);
y();
}
x(function y(){
  console.log(y);
})

```
- When executed the above code, 
- As javascript is a single threaded language, that means the code will be executed one line at a time and in a order.
1. setTimeout will be registered and that setTimeout will take that callback function and store it in a seperate space and will attach a timer to it. And the js will not wait for 5s for the completion of the timer instead it move on to next lines. Whatever need to be run after 5s is passed to the setTimeout as a callback function.
 "Time tide and Javascript waits for none 😜"
2. It will see the function defination of x.
3. Next, will call the function x by passing the callback function y and executes the console.log("x") and later calls the callback and then prints the logs in the function y. After that call stack will get empty.
4. After then, the timer will expires after few milli seconds and then suddenly the setTimeout anonymous function will appear in the callstack and execute timer log in that callback function.

## Blocking main thread
- Javascript has only one callstack which is also called as main thread.
- Everything whatever executed in the page is executed through the callstack only.
- If any operation blocks this callstack, then it is called **Blocking the main thread**
- Suppose a function x has very heavy operation that may take 20-30 seconds to complete. By that time as js has only one call stack(one main thread), it wont be able to execute any other function in the code that means everything is blocked until the completion of function x.
- We should never block our callstack.
- We should always try to use async operations for the things which takes time.
- If js doesnt have the first class functions we cannot execute the asynchronous operations.

## Event listners
```
<!-- HTML -->
<button id="clickMe">Click Me</button>

<!--script Js  -->
document.getElementById("clickMe")
  .addEventListener("click",function xyz(){
    console.log("button clicked");
  })
```
- Here in the above example, event listener takes the eventtype, a function which is a callback function.
- So whenever an click event happens on that function, it will call that callback function which will be stored somewhere and automatically pushed into our callstack.

### Get the count of how many times the button clicked
1. First way is by using the global variable which is not a good solution as the variable can be modified and accessible outside the program.
```
let count = 0;
document.getElementById("clickMe")
  .addEventListener("click",function xyz(){
    console.log("button clicked ",++count);
  })
```
2. Another way is by using closures, through which we can make the count variable secure and make count cannot be modified through any other program.
```
function attachEventListeners(){
  let count = 0;
  document.getElementById("clickMe")
    .addEventListener("click",function xyz(){
      console.log("button clicked ",++count);
    })
}

attachEventListeners();
```
- From the above example, the callback function xyz is forming an closure with its outer scope.
- So now, when we call the function attachEventListners(), it will form a closure with count and remembers where the count is present.

### Going deep through dev tools
- Using same example from the above.
- When we go to the elements in the devtools, we can see our button there.
- Click on that button tag and see the event listeners on the button in the event listeners tab.
- In that event listeners tab, we can see the click event listener that we attached.
- And in that click event listener we had an handler which is the callback function xyz that we passed to the event listener.
- And in that handler it has the scopes, which is the same lexical scope that the function carries.
- In that scopes, it consists of its parent's environment lexical scope which is the closure and also the parent's environment of its parent which is the global scope.

### Why do we need to remove event listeners (Garbage collection and removeEventListeners)
- Event listeners are heavy in the memory. It may contains the closures.
- Due to this our page will load slow due to all this scopes and callback functions in case of huge event listeners in our page.
- So, good practice is that to free up event listeners when not in use.
- When we free up event listeners all the variables are garbage collected.

## Event Loop
-  Javascript is a synchronous single threaded language and it has only one call stack and can only do one thing at a time.
-  The callstack is present inside the JS engine.
-  All the code of javascript is executed in the call stack.
-  Whenever js code is executed, a global execution context is created an it is pushed into the callstack.
-  In the Global execution context, memory is allocated for our variables and functions and then the code is executed line by line.
-  Incase if we came across any function calls in the code, an execution context for that particular function is created and pushed into the call stack.
-  After that, code in the function execution context is allocated with memory and code is executed.
-  After completion of the execution of that particular execution context, it will be popped out of the call stack and control moves back to the code in the global execution context.
-  After the completion of execution of global execution context, it also popped out of the callstack and completes the program.
-  So, main job of the callstack is execution of the context.

- The JS Enginer is present in the browser.
  `CallStack -inside-> JSEngine -inside-> Browser`.
- Callstack doesnt have the power of running the code after some time. ANything if it enters call stack, it should be executed. So it doesnt have the power of timer.
- So, the things like timers,locations, bluetooth etc.. are handled by the super power called Browser.
- To access the things like timers, location and other external things we need something called web apis which will connect with browser to get the features.
#### WebAPIs
  - These below are the kind of super powers that browsers have and they are provided to us in js engine by providing some access to use all of these.
  -   setTimeout()
  -   DOM APIs for DOM
  -   fetch() 
  -   localStorage
  -   console
  -   location and more
  - We are able to use all this by using the global object called window.
  - It means all this functions are attached to the global window object. (setTimeout or window.setTimeout)

## Event Loop, CallBack Queue and Micro Task Queue
![image](https://user-images.githubusercontent.com/76255797/133112174-b9163d88-442d-43e8-a7c1-bc2d18ddd872.png)

Eg:
```
console.log("Start");
document.getElementById("btn").addEventListener("click",function cb(){
  console.log("Callback")
});
console.log("End")
```
- Whenever we run a js code, Global Execution Context (GEC) is created and pushed into the callstack.
- It goes through the code and allocate memory and then execute code line by line.
- Here when the control goes to the first line, js engine see the console.log and it goes to the console in the window object to hit the web api console method and hit the log to the console in the browser.
- Next control moves to the next line, document.getElementById and call the DOM apis and get the element and then addEventListener which is another super power given to the js engine by the browser through the window object in the form of webAPI which is the DOM API.

- This addEventListener *registers a callback in the webAPIs environment* (where the window object and its methods are present) on an event "click". And then js enginer moves on.
- And next the control goes to the console log end and js engine goes to te console in the window object and hit the web api console method and hit that log message to the console in the browser.
- As program ended, the GEC will also be cleared from the callstack but the event handler callback registered in the web apis environment will stay back in it until we explicitly un registered the event or closed that browser.
- When the user clicks on that button - the event handler is binded to, then that event handler reference is pushed to the callback queue and that callback waits over there for its turn to get executed.
- From then the event loop takes care of the execution of that callback on callstack which is in the callback queue.
  ### Event Loop
  - The job of event loop is continous monitoring of the callback queue and the callstack.
  - If event loops finds that callstack is empty and there is a function waiting in the callback queue, then event loop takes that function and put it in the callstack.
- So when the callstack is empty, the eventloop removes that from the callstack and push it into call stack to make it executed.

 ### Why do we need a callback
 -  Event loop will not pick the callback directly from the webapi environment because, If suppose user/some other fire the events continously, event loop cant manage that many clicks at a time.
    -  If suppose user/some other fire the events continously, then that callbacks will wait in that callback queue. Next event loop will continusly check the callstack and if it is empty then take a callback from the queue and push into the callstack one by one.

### fetch() function
-  fetch is way to call an api and get the response as a promise which can be handled using then & catch or asynchronously.
-  then method will take the callback function and resolve the promise.
```
console.log("Start");
setTimeout(function cbT(){
  console.log("CB Set Time out")
},5000)
fetch("https://api.netflix.com")
.then(function cbF(){
console.log("CB Netflix API Fetch");
});
//some 1000 lines of code
console.log("End");

```
- When the above js code executed, a GEC is created and pushed into the callstack.
- Then allocated memory for the functions & variables and the code is executed line by line.
- When the control is at our first line, js engine see the console.log and it goes to the console in the window object to hit the web api console method and hit the log "Start" to the console in the browser.
- Now it moves to the next line and setTimeout will register this callback function on to the web api environment (where the window object and its corresponding methods are present) and also js engine starts the 5000 ms timer and attaches to it and next js engine moves to the next line.
- And there it encounters the fetch function, then js engine points to the fetch in the window object to hit the web api fetch method for making network calls.
- And it also registers cbF callback function in the web api environment and it will wait for the data to be returned from the server from which we made a network call.
- So once we get the data from the server, the callback function cbF reference will be pushed into a other queue called **Micro Task Queue** which has highest priority than callback function.
  ### Micro Task Queue
   -  It is also similar to the callback queue but only in case of promises and network calls the callback functions will go to the microtask queue.
  -  Again the event loop will take care of pushing the function to callstack. But here if both the callback queue and the micro task queue contains the functions and the callstack is empty, it will consider and give priority to the functions in the micro task queue and push them into call stack first. Because micro task queue functions have high priority than the callback queue.
- Suppose if we get the response from the server immediately, and still the main program execution is not done in the callstack as there are some another 1000 lines need to be executed
- But meanwhile the timer of settimeout callback also expired and the callback function cbT is waiting in the callback queue.
- And now the code is still executing in the callstack and the 2 callback functions cbF in microtask queue and  cbT in callback queue are waiting for execution in callstack.
- And at the same time event loop will continously check the callstack for pushing the callback references into callstack.
- And suppose the execution finished and the last console log end is fired and the global execution context is popped out of the callstack.
- Then event loop finds that callstack is empty and then event loop will push cbF callback from microtask queue first in the callstack and it will be executed and then after its completion and removal from the callstack the event loop will take the cbT callback from the callback queue into callstack and it also executed and then removed from the callback.

### Micro Tasks
- All the callback functions from the promises are called micro tasks.

### Mutation Observer
- Mutation observer will keeps on checking whether there is some mutation on the dom tree or not. If there is some mutation in the DOM tree, it will execute some callback function.

- **Promises and the mutation observer objects will go to the _Micro Task Queue_**
- **Other event listeners, dom apis and other will go to the _Callback Queue_**

- **Callback Queue is also called as Task Queue*
- **Only Asynchronous callbacks are registered in the web apis environment. And other synchronous function we pass inside like map, reduce and filter are not registered in the web api environment.**

### Starvation of functions in the callback queue
- The situation where the callback functions in the micro task queue creates another micro task continously and does not give chance for the functions in callback queue is called as Starvation of functions in the callback queue.


## JS Engine
- Javascript can be run only any type of systems.
- This can be possible due to Javascript Runtime Environment
### Javascript Runtime Environment
  - It is like a big container which has all the things required to run the javascript code.
  - The Javascript runtime environment includes js engine, set of APIs, eventloop, callback queue, micro task queue and someother things required to run js.
  - **JS Engine** is the heart of the Javascript Runtime Environment as it is not possible without JS Engine.
  - Every browser is able to run the js because it contains the JS engine in it.
  - Nodejs is also called as open source javascript runtime which gives us the ablity to run the js outside the browser by using nodejs environment.
  - The APIs may differ from environment to environment based on where it is running.
  - Nodejs JS RE can have some different APIs than the Javascript runtime environment in the Browser and some may be same for both of them like console, setTimeout, etc.. but they may have different implementations for browser and the apis.
### Different JS Engines
  - There are many js/ecma engines. But all these are implementing just in time compilation(JIT) or variations of the idea.(JIT- JIT is often faster because it compiles the code when it is actually called for, the first time it is called or it is a way of executing computer code that involves compilation during execution of a program (at run time) )
  - Some of the popular ECMAScript/JS Engines are Carakan-Opera, Chakra- MS Edge, SpiderMonkey-Firefox, JavascriptCore-Safari, v8-Chrome,Node,Deno,V8.NET and so on.
  - We can also create a js engine by following ECMA(European Computer Manufacturer's Association) script standards.
  #### First JS Engine
    - The first js engine was developed by Brendan Eich who developed the js.
    - This engine was evolved a lot and this was called as the SpiderMonkey now.
- JS is not a machine. It is like program written in low level languages.
- JS Engine will take the js code that we written as input and gives out the machine level code which can be executed by the machines.
- For example V8 engine is written in c++. 
### JS Engine Architecture

- JS Engine takes the code as input and it goes through the 3 major steps.
  - Parsing
  - Compilation & Execution

 #### Parsing
  - The code which we written will be broken into tokens.
  ##### Syntax parser
  - This will take code and convert into AST (Abstract Syntax Tree).
  - It will be done something like below.
  ```
  <!--  JS  -->
  const bestJSCourse = "Namaste Javascript"
  
  <!--   AST -->
    {
    "type": "Program",
    "start": 0,
    "end": 41,
    "body": [
      {
        "type": "VariableDeclaration",
        "start": 0,
        "end": 41,
        "declarations": [
          {
            "type": "VariableDeclarator",
            "start": 6,
            "end": 41,
            "id": {
              "type": "Identifier",
              "start": 6,
              "end": 18,
              "name": "bestJSCourse"
            },
            "init": {
              "type": "Literal",
              "start": 21,
              "end": 41,
              "value": "Namaste Javascript",
              "raw": "\"Namaste Javascript\""
            }
          }
        ],
        "kind": "const"
      }
    ],
    "sourceType": "module"
  }

  ```
  - Later, the AST generated is passed to Compilation phase.
  
### Interpreter
- Our whole Code is executed line by line.
- Fastly executed and less efficiency.
### Compiler
- Our whole code is compiled even before the execution and an optimized version of our code is generated.
- And then the optimized code is executed.
- More efficiency and less speed.

- JS is initially an interpreted language but in today's world most of the modern js engines uses the both the compiler and interpreter. So its purely dependent on the js engine.

### JIT Compilation
- By using this mechanism, the js engines are able to use interpreter along with compiler.
- That means it uses Interpreter and compiler to execute the code.
- AST is given as input to the interpreter, then interpreter will convert the high-level code to machine code line by line and it takes the help of compiler to optimize the code and then it is executed at the same time.
- The job of compiler over here is to optimize the code as much as it can on the *run time* that is why it is called JIT compiler.
- Different JS engines will have different algorithms to perform JIT compilation.
- In some JS engines, there is something called as AOT compilation. Ahead of Time compilation where the compiler takes the piece of code and which is going to be executed next and tries to optimize it as much as it can.
- The execution is done by two major components.
  1. Memory Heap 
  2. Callstack
- Memory Heap is the place where all the variables and functions are stored. It is constantly in sync with callstack, garbage collector and lot of other things.

### Garbage Collector
- It basically tries to free up memory whenever possible like when some variables are not been used, cleared timeout etc..
- It uses an algorithm called Mark & Sweep.

![image](https://user-images.githubusercontent.com/76255797/133243742-14c528e7-020f-4dd1-9e12-d0a33dc6653f.png)


### Mark & Sweep Algorithm
- Any garbage collection algorithm must perform 2 basic operations. 
- One, it should be able to detect all the unreachable objects. 
- Secondly, it must reclaim the heap space used by the garbage objects and make the space available again to the program.
- The above operations are performed by Mark and Sweep Algorithm in two phases:
1. Mark phase
- When an object is created, its mark bit is set to 0(false). 
- In the Mark phase, we set the marked bit for all the reachable objects (or the objects which a user can refer to) to 1(true). 
- Now to perform this operation we simply need to do a graph traversal, a depth first search approach would work for us.
-  Here we can consider every object as a node and then all the nodes (objects) that are reachable from this node (object) are visited and it goes on till we have visited all the reachable nodes.
-  Algorithm
    ```
    Mark(root)
        If markedBit(root) = false then
            markedBit(root) = true
            For each v referenced by root
                 Mark(v)
    ```
2. Sweep phase
- As the name suggests it “sweeps” the unreachable objects i.e. it clears the heap memory for all the unreachable objects. 
- All those objects whose marked value is set to false are cleared from the heap memory.
- Now the mark value for all the reachable objects is set to false, since we will run the algorithm (if required) and again we will go through the mark phase to mark all the reachable objects.
- Algorithm
    ```
    Sweep()
    For each object p in heap
        If markedBit(p) = true then
            markedBit(p) = false
        else
            heap.release(p)
    ```

### Compiler uses some optimizations.
- Optimizations like
  - **Inlining**
    - Inlining is the process of replacing a subroutine or function call at the call site with the body of the subroutine or function being called. This eliminates call-linkage overhead and can expose significant optimization opportunities.
  - **Copy Elision**
    - As copying of object causes overheads of creating a temporary object & then copying it.
    - So to avoid that, modern compilers elide the copying of objects whenever possible. This compiler optimization technique that avoids unnecessary copying of objects is called Copy Elision.
  
  - Inline caching
    - Inline caching is an optimization technique employed by some language runtimes, and first developed for Smalltalk.
    - The goal of inline caching is to speed up runtime method binding by remembering the results of a previous method lookup directly at the call site.
    -  Inline caching is especially useful for dynamically typed languages.

### V8 Js Engine
![image](https://user-images.githubusercontent.com/76255797/133243302-243f2551-85ac-4549-8f53-9aa3bfd0f1f3.png)
- Then generated byte code is executed.


