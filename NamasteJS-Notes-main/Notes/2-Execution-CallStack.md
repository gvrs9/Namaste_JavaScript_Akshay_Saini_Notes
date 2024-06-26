# Episode 2 : Execution & Call Stack

Everytime you run a program, an execution context is created.
When a variable or function is encountered, it is stored in the memory area.

#### This execution context is created in two phases.

1. Memory Creation Phase
2. Code Execution Phase

```js
var n = 2;

function square(num) {
  var ans = num * num;
  return ans;
}

var square2 = square(n);
var square4 = square(4);
```

Now first, for this entire code, when we run it, a <strong>Global</strong> execution context is created.

### In the first phase (memory creation)

- First, <strong>Js</strong> skims(goes or scans) through the whole js code line by line and memory allocation takes place.
- Memory is allocated to variables and functions.
- For variable name(which is key) it assigns a value of <strong>undefined</strong>
- For the function name(which is key) it assigns the entire function code as value.

```js
n:undefined
square:{...entire-code...}
square2:undefined
square4:undefined

```

### In the second phase (code execution)

- <strong>Js</strong> once again skims(goes or scans) through the whole code line by line and it executes the code now.
- The variable name is replaced with its actual assigned value from code. So now n:2
- Skips over function code as there is nothing to assign/execute there.
- <strong>We encounter a function call in square2 and the function gets invoked. So a brand new local EC is created inside the code part of global EC and this will have the same 2 components: Memory and Code.</strong>
- In the local EC, ans and num are both undefined (in first phase). Then, the n value in global EC is passed to num, replacing undefined. num is the parameter and n is the argument.
- ans = num\*num (calculated in code part of local EC and returned) replaces undefined in local EC (memory part) and the final value is returned from local and is assigned to square2 var in global.
  After returning, local EC is removed form global EC and control goes back to global at the place/line at which the function invocation happened which lead to creation of that local execution context.
- One more fun. call is met. Same thing happens here.
  Once square4 value is replaced from undefined to 16, global EC will also be deleted.

To manage all these EC, a call **stack** is created. Everytime code is run, the EC is pushed in. So first global EC is pushed. Then e1 EC(for square2) is pushed, and then after
value returned, is popped. Similarly e2 EC(for square4) is pushed, and then popped and finally Global is also popped and stack is empty.

> Call Stack maintains the order of execution of execution contexts

#### Call stack aka Execution control stack, program stack, control stack, runtime stack ad machine stack.

#### The Execution Contexts (Global and Locals) are pushed into the Call Stack and popped once the control goes back to the previous EC and so on until the call stack gets empty.
