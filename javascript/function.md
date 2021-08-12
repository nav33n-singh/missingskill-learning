# Function  

</br>

_**IMPORTANT: A function check must be added before calling a function to avoid breaking of program:**_  
>_**function_name && (typeof function_name === "function") && function_name()**_

</br>

* A function is a small block of code comprising statements.
* Functions are first class citizen.
* Functions are nothing but a function object, as everything is an object in js.
* Functions can accept one or many or zero paramenter/s, anything can be a parameter to a js function let it be primitive,non-primitive, or a function.
* Functions can return a value and functions reference also.

## Declaration and Assignment  

* Functions can be declared independently or assigned to a variable.

</br>

### ES5  

```js
//function declaration
    function fn_name(){ //default parameter is undefined
        statement1;
        .
        .
        .
        statementN;
        return some.value; //default return value is undefined.
    }

//function assignment
    var someVariable = function(){  //this kind of functions are called annonymous function
        statement1;
        .
        .
        .
        statementN;
        return some.value;
    }
```

### ES6  
ES6 uses an arrow(=>) operator to assign a function.  
The rest of the properties are the same as ES5 functions.  

```js
    let someVariable = (parameters if any) => {  // () can be ignored if only one parameter passed
        statement1;
        .
        .
        .
        statementN;
        return some.value;
    }
```

### IIFE  

* It stands for **I**mmediately **I**nvoked **F**unction **E**xpression,also called an nameless function(atleat i call it).  

* As the name suggests it gets executed as soon as it is defined.
* It can not be called again as this type of function has no name and no reference.  

```js
    //another type of annonymous function
    ;(function(paramrters if any){  //at start ";" is added to avoid unexpected behaviour
        statement1;
        .
        .
        .
        statementN;
        return some.value;
    })(parameter to be passed)  //  this bracket is a sort of function call.executes function

//This function can be assigned to a variable to store value returned by it
let someVar = (function(){
                return someValue;
})();
```  

## Hoisting

* At runtime ***functions declarations*** get hoisted.
* ***Function assignments*** do not get hoisted.
* This gives rise to another phenomenon knows as overwriting, which I will explain later.

```js
console.log(hello());  //hoisted
console.log(test);     //undefined, As it is just a var declaration that just got hoisted
console.log(test());  // test is not a function

function hello(){     // function declaration
   return "hoisted";
}
var test = function(){     //function assignment
   return "not hoisted";
}
console.log(test());  // not hoisted
```

## Overwriting  

* It is a runtime phenomenon where,  
  _case 1:_ function gets overwritten by variable  
  _case 2:_ variable gets overwritten by function  
  _case 3:_ function gets overwritten by function

### case 1: Variable overwriting function  

```js 
var greeting; // if variable is initialized then it overwrites by function

function greeting(){
  return hello;
  }
greeting = "hello"; //initialized
console.log("type of greeting:",typeof(greeting));  //type of greeting: string
```

### case 2: Function overwriting variable  

```js
var greeting;//if the variable is not initialized then function overwrites it

function greeting(){
  return hello;
  }
  
console.log("type of greeting:",typeof(greeting));// type of greeting: function
```

### case 3: Function overwriting function  

```js
    console.log(greeting());  //hii    functions with same name gets overwritten by later declared function
    function greeting(){
        return "hello";
    }

    function greeting(){
        return "hii";
    }
```

## Function call and Functions reference  

### Function call  

```js
    function somefunction(){
        return "something";
    }

    var somevar = somefunction();//this is a function call
    console.log(somevar); // something 
    console.log("type of somevar:",typeof(somevar)); //string
```

### Cascading function call  
  
```js
    function toplayer(){
        function middlelayer(){
            function bottomlayer(){
                return "HOT!!!";
            }
            bottomlayer;
        }
        middlelayer;
    }
    var temperature = toplayer()()(); //this is called cascading function call
    /*
    explanation:
    [toplayer()]()()
        ^
    [middlelayer()]()
        ^
    [bottomlayer()] = > return "HOT!!!"
    */
    console.log("temperature is:", temperature);  //temperature is: HOT!!!
```

### Function reference

```js
    function somefunction(){
        return "something";
    }
    var somevar = somefunction;  //this is function refrence
    console.log(somevar);   // [Function: somefunction]
    console.log("type of somevar:",typeof(somevar));  //function
```

## Function parameter  

* Function parameters are values passed to function as an argument.
* There are two ways to pass a parameter to a function, i.e.  
   _case 1:_ pass by value (primitive types)  
   _case 2:_ pass by refrence(arrays,objects,functions)  
   _case 3:_ Actually,this is not any case,but parameters can be passed directly without declaration.called _**inline parameters**_.  

### case 1: pass by value

```js
    function add(a,b){  //at runtime function will declare two variables "a" and "b" at functional scope both
        return a + b;   //inheriting properties of passed parameter.here i.e. primitive and primitive is always copy by 
    };                  // value.
    let a = 5;  // primitive type
    let b = 7;  //primitive type
    add(a,b);
```  

### case 2: pass by refrence

#### Passing Object as parameter  

```js
    function object(obj){              // the parameter passed to this function is copy by refrence type hence any change 
        obj.type = "pass by refrence"; //made to parameter will alter the actual object also.
    } 
    
    const object1 = {
        name:"object"
    };
    console.log(object1); // {name:"object"}  before calling function object
    
    object(object1);
    console.log(object1); // {name:"object",type:"pass by refrence"}   after calling function object
```

#### Passing functions reference as parameter

```js
    function print(param){   //takes function "add"s refrence as parameter
        console.log(param(5,2));   // passes inline parameter to add and calling it
    }
    function add(a,b){
        return a + b;
    }
    print (add);  // 7
```

### case 3: Inline parameters

#### Passing primitive type as an inline parameter

```js
    function inline(param){
        return a;
    }
    inline(100);
    console.log(inline); //100
```

#### Passing an inline function as a parameter

```js
    function hello(a){       //passed refrence to inline function
        return "hello " + a();
    }

var greeting = hello(function(){return "world !!";}); //passed inline function as parameter

console.log(greeting); // hello world !!
```

## Function scope

* In js functions are block-scoped.
* Code inside the functional block can not be accessed from outside function.
* functions can not be accessed outside their scope.
* local variable given preference    

```js
    {//<block scope>
        function time(){//<functional scope>
            var night = false;
            return "day";
            function name(){
                return "value";
            }
        //</functional scope>
        }
        name();//name is not defined
        night = true; // night is not defined //outside functional scope
    //</block scope>
    }
    time(); //time is not defined  // outside block scope
```

## Function Classifications  

### 1. Pure function  
   If a function does not alter the actual value of parameters passed to it then that function is called a pure function.

```js
    //pure function
    function pure(obj)
    {   let inside = {};
        inside.name = pure.name;
        inside.type = pure.type;
        inside.behaviour = "non-hostile";
        return inside;
    }
    let param = {
        name:"function",
        type:"pure"
    };
    let result = pure(param);
    console.log("returned object:",result);  //returned object: { name: 'pure', type: undefined, behaviour: 'non-hostile' }
    console.log("passed object:",param);  //passed object: { name: 'function', type: 'pure' }
```  

### 2. Higher-order function  
   If a function takes function reference as a parameter and/or return function reference then that function is called a higher-order function.  

```js
//higher order function
    function highOrder(a){   // accepts "invocation" function refrence as parameter
        let b = "hello ";
        let c = a();
        function concat(){
            return b + c;
          }
    return concat;          // returns "concat"  function refrence as value
    }
    
    
function invocation(){
    return "world !!";
    }

let message = highOrder(invocation)();

console.log(message);    //hello world !!
    }
```