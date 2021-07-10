# JavaScript

## Execution Context
  - Everything in the javascript happens inside an Execution Context.
  - It can be considered as a container in which whole javascript code is executed.
  - It has 2 components in it.
      1. Memory Component
        - It is the place where the variables and functions are stored in the form of key value pairs.
        - It can be also known as **Variable environment**.
      2. Code Component
        - It is the place where our code is executed line by line as it is a single threaded.
        - It can be also known as **Thread of Execution**.
### JavaScript is a Synchronous Single-Threaded Language.
  - As it is a single threaded language, js can execute only one command at a time.
  - Synchronous single threaded means that js can execute one command at a time and in a specific order which means it will only goes to next line if it executed the current line.


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
      - And the **whole execution context of the function is deleted after the control coming to main execution context**. It means when we call the same function another time the again the new execution context is created and the same process is repeated.
     

### Call stack
  - It is a stack which is populated when a program is executed.
  - By using this, javascript is working and managing with all the execution contexts it created.
  - Every time in the bottom of the stack, the global execution context is populated.
  - When a function is invoked a new execution context is put into the stack and control is now to the top of the stack i.e., the function's execution context.
  - After the function returns the value to global execution context, that function is popped from the call stack and the control goes back to the global execution context (as it is the top element in the stack now).
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

### Functions types and their behavior
- In case of the **Normal Functions or Proper Functions**, they are defined somewhere in the program code with the _keyword function_, so the js will load the entire function code into the memory in the **Memory Execution Phase** it self. So even before the line it declared we can access or call the function directly.
- In case of the **Arrow Functions or Anonymous Functions assigned to Variable**, they are defined somewhere in the program code like _variable which is assigned with function_. So js will load the _variable_ into the memory with specifying as undefined instead of the entire function code because here the arrow function is assigned to some variable.


## Shortest JS Code is an Empty JS File
- Even we doesnot write an single line of code in the js file, it will run.
- When we execute that empty js file, the global execution context will be created along with the memory space by js engine even there is nothing to do externally in the file.

### JS engine
- Different browsers or environments use different engines to run the js.
- Chrome uses v8 js engine to run the javascript.
- Firefox uses Spider Monkey js engine
- Chakra Jscript engine is used in edge
- These engines has a responsibility to create this global object, incase of browsers it is known as _window_, in case of node some other object(called global), and wherever you run the code the js program it is different but there will be a global object created.
- And also creates some objects and keywords. Like
### window object
- Which contains huge collection of methods and variables related to the window.
- window object can be used from anywhere globally.
- Its a global object which will be created along with global execution context when we run any program.

#### this variable
- Along with the window object while creation of global execution context, js engine creates a _this_ variable.
- It will points to the window object while the global execution context creation time itself.
- At global level, this===window is true.

#### When ever you create any variables in the global space (not in any functions) they are attached to that global object (_window_ in the browser). 
#### Whenever we try to access any variables or function without any objects (which are declared globally) then the js engine assumes implicitly that it is in the global space.
```
var a=10;
console.log(a);
console.log(window.a);
console.log(this.a);
```
- All the above 3 console statements results the same.

## Scope Chain, Scope & Lexical Environment
- As we discussed above, all the variables that declared in global space will have scope and can be access with in the inner functions also.
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

- So, lets look at the code.
- When we run our code, Initially a global execution context is created and pushed into the call stack and all the variables and functions in the global scope are allocated with the memory.
- Later while the function a is called, it will create another execution context, then memory is created for variable b and function c.
- After that the execution of code in the function begins, b is assigned with the value 10 and call the function c.
- As function invoked, execution context for C is created and again the memory is allocated along with code component.
### Lexical Environment
- Lexical (in hierarchy or in order) means where the specific code is physically present.
   Eg: From the above example, we can say that c is lexically inside function a & function a is lexically inside the global space.
- Wherever an execution context is created, a lexical environment is also created.
- Lexical Enviroment is the local memory along with lexical environment of its lexical parent(where the current lexical env sits).
   Eg: From the above example, lexical enviroment of the function c includes the local execution context memory and the parent lexical enviroment means the function a's execution context memory
   - In the same way, lexical environment of function a  =  local execution context memory space + lexical enviroment of global execution context
   - In case of global lexical environment, the parent lexical enviroment points to null.
 Eg:
 - When we try to print the variable b, first js engine searches within the local lexical environment and as it is not found it will searches in the parent lexical enviroment through some reference to that and so on until it is found or parent lexical enviroment is null.
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
- In this below example, when we print the variable b in the global space outside the funtion a, then first it searches in the current global execution context lexical environment.
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
- As it is not found, then it tries to search for the reference of the parent lexical environment of global lexical environment but it is null. Therefore no more lexical enviroments.
- So as js engine not found b in the global and its parent, it declares and raises that the variable b is _not defined_ (not in the scope).

## Scope Chain
- The way/mechanism of the finding variable or functions through this chain of lexical enviroments and their parent references is known as Scope Chain.
- It is nothing but the chain of all these lexical enviroment and their parent references.
- Finally, js engine first try to find the variable in the local lexical enviroment and if it is not found it moves up to parent level of the scope chain.
- **Chain of the lexical enviroments is known as Scope Chain.**
- In browser *Scope* is lexical enviroment.

## let & const vs var
- Generally, all the variables are hoisted inspite of whether they are declared with let/const/var.
- But in the memory allocation phase, memory will be allocated for let & const variables and also for var variables but the variables declared using var are attached to the Global object but the let/const are attached to some other memory space other than global.
- As the let and const variables are put in some other location than global, they cannot be accessed without assigning some value.
- These let/const variables will not be accessed with window object.
### Duplicate Declaration
- Re-declaration of let/const variables is not allowed and raises syntax error (specifying identifier has already been declared) even before the start of program execution.
- But Re-declaration of var variables is permitted.

### let vs const
- Re-initialization/initialization after declaration is possible incase of the let but incase of the const, re-initialization is not possible and also the value for const variable should be given at the time of declaration itself.
- If we not gave value to const variable at the time of declaration, it will throw syntax error saying that initializer for const variable is missing because the const syntax expects initialization & declaration at the same time.
- If we not try to re-initialize or change the value of const variable after declaration time, it throws Type Error: Assignment to constant variable because const type variable can be reassigned.

### Reference error
- When the js engine tries to access the specific variable inside the memory space but it cannot access it then it raises reference error.

**Whenever possible we need to use const then let or if needed we need to use var**


## Temporal Dead Zone
- The time between when the let/const variables are hoisted & till they are initialized with some value is called Temporal deadzone.
- If we are trying to access that variables which are in temporal dead zone we get reference error specifying that **we cannot access variable before initialization**.
- Which is different error from the error which is caused if we try to access the variable which is not even declared anywhere in the program. (If it is not declared anywhere it will raise the reference error specifying **variable is not defined**).
- Moving all the declarations to the top of the code is best way to avoid temporal deadzone/shrink the temporal deadzone.

## Block Scope & Shadowing

### Block
- Block is also known as compound statement.
```
{

}
```
- Block is used to group the multiple statements.
- This grouping of multiple statements is needed and can be used in a place where javascript expects a single statement.
Eg: Suppose if we take a if condition, it expects only a single statement.
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
- It means what all variables and functions that can be accessed inside a block is called Block Scope.
Eg:
```
{
  var a = 10;
  let b = 20;
  const c = 30;
}
```
- When we take above example code and run it, we can observe that the b & c variables are hoisted at seperate space called block scope.
- But a will be a global scope as we discussed variables declared with var always tied to the scope where they are declared.
- As here, it is not declared in any function and declared in the global execution context so it is hoisted to global space.
- And we can also check that even let and const are declared in global execution context, but they are hoisted in special space called block scope. So let and const variables are called as block scoped variables.

### Shadowing in js

