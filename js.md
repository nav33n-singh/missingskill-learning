# Javascript

## History

* Netscape communication corporation released _Netscape Navigator_ web browser in 1994.
* Netscape increasing market share has drawn Microsoft's attention.
* Microsoft made an offer to buy Netscape Navigator but got a refusal.
* Microsoft released Inter Explored for free.
* Netscapes market share dropped drastically after that.
* Sun microsystem and Netscape joined hands to fight Microsoft but failed.
* In 1995, Brendan Eich created a new scripting language on demand of Netscape communication corporation and named it Javascript.
* Netscape gone bankrupt and donated javascript to ECMA.

## Tech Debt

* **+** acts as an addition as well as concatenate. sometimes it leads to unexpected behaviour of code
* == ignores datatype check and compares value only.  
  for example: (2 == "2") returns true
* typeof(null) returns "object". while it should return null.

## Control structures

* if else

```js
// if argument passed to if block evaluated to be true then it ececutes else block executes
    if(test === true)
    {
        //execute this
    }
    else{
        //excute this
    }
```

* for loop

```js
//takes 3 arguments ,initial value, test condition, and increment/decrement
for(initialization;test condition;itration)(
    //statement
)
```

* while loop

```js
    while(test -= true){    //exits loop when condition is false
        //execute statement
    }
```


* do while loo

```js
//gets executed at least once
    do{
        //execute statement
        }
        while(true);
    
```