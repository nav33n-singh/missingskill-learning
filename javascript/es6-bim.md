## ES6 built-in methods

### Timer

1. setTimeout: It takes a function and time(in milliseconds) as parameters and executes only once.

```js
    setTimeout(function(){console.log("executed after 3 seconds",3000)});
    setTimeout(function(){console.log("executed after 0 seconds",0)});  //it considers 0 as input time also
```

2. setInterval: It also takes a function and time(in milliseconds) as parameters but it keeps looping after the passed interval. If not handled correctly it causes memory leak.

```js
    let counter = 60;
    let timer = setInterval(function(){
                            if(counter !== 0){
                                console.log("Bomb will explode in",counter,"seconds");
                                counter = counter -1;
                                }
                            else clearInterval(timer);},1000);
```

### Number

1. parseInt: Returns floor integer value from passed parameter if parameter only contains number before decimal else returns NaN.

```js
console.log(parseInt("3453.jb45")) // 3453
console.log(parseInt(5.9)); // 5
console.log(parseInt("nj3533.53j")); //NaN
```

2. parseFloat: Returns float value from passed parameter if parameter only contains number before decimal else returns NaN.

```js
console.log(parseFloat("3453.jb45")) // 3453
console.log(parseFloat(5.943434)); // 5.943434
console.log(parseFloat("nj3533.53j")); //NaN
```

### JSON

* It stands for javascript object notation.
* It is used for transporting data between apps, from frontend to backend and vice-versa.
* In JSON js object keys get converted into a string
* No delimiter allowed after the last element of the object

1. JSON.stringify: Used to convert an object/array into a JSON string.

```js

const object = {
                    brand:"msi",
                    model:"xxyy",
                    ram:"16GB",
                }
const array = [2,4,5,6,8,9];

let json = JSON.stringify(object);
let jsonA = JSON.stringify(array);

console.log(json);  //'{"brand":"msi","model":"xxyy","ram":"16GB"}'
console.log(typeof json);  //string

console.log(jsonA);  //'[2,4,5,6,8,9]'
console.log(typeof jsonA); //string
```

2. JSON.parse: Used to convert a JSON string into a JS object.

```js
    let objstr = '{"brand":"msi","model":"xxyy","ram":"16GB"}';
    let object = JSON.parse(objstr); //{ brand: 'msi', model: 'xxyy', ram: '16GB' }
    console.log(object); //object
```


### String literal

`` preserves spaces and newlines of string inside it.placeholders "${}"can also be used.  

```js
let name = "crime master gogo";
let passion = "drug lord";
let intro = `i am ${name}
and i want to become ${passion}`;
console.log(intro);//"i am crime master gogo
                   //and i want to become drug lord"   

```