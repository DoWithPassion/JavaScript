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
- ```
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

