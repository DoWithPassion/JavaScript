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
- These engines has a responsibility to create this global object, incase of browsers it is known as _window_, in case of node some other object, and wherever you run the code the js program it is different but there will be a global object created.

- And also creates some objects and keywords. Like
### window object
- Which contains huge collection of methods and variables related to the window.
- window object can be used from anywhere globally.
- Its a global object which will be created along with global execution context when we run any program.

#### this variable
- Along with the window object while creation of global execution context, js engine creates a _this_ variable.
- It will points to the window object initially while the creation of global execution context creation time itself.
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

