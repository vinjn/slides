## function() {};
========
### My name is VZ
```javascript
var vz = function() {
    // I'm JS
};
vz();
```
```C++
auto vz = []() {
    // I'm C++11
};
vz();
```
========
### I don't have a name
```javascript
(function() {
    // I'm JS
})();
```
```C++
[]() {
    // I'm C++11
}();
```
========
[FunctionNameExample01](Ch07/FunctionNameExample01.htm)
```javascript
function functionName(){
    //noop
}

//works only in Firefox, Safari, Chrome, and Opera
alert(functionName.name); //"functionName"
```
========
[FunctionDeclarationHoisting01](Ch07/FunctionDeclarationHoisting01.htm)
```javascript
sayHi();
function sayHi(){
    alert("Hi!");
}
```
========
[FunctionDeclarationsErrorExample01](Ch07/FunctionDeclarationsErrorExample01.htm)
```javascript
var condition = true;
//never do this!
if(condition){
    function sayHi(){
        alert("Hi!");
    }
} else {
    function sayHi(){
        alert("Yo!");
    }
}
sayHi();```
========
[RecursionExample01](Ch07/RecursionExample01.htm)
```javascript
function factorial(num){
    if (num <= 1){
        return 1;
    } else {
        return num * factorial(num-1);
    }
}
var anotherFactorial = factorial;
factorial = null;
alert(anotherFactorial(4));  //error!
```
========
[RecursionExample02](Ch07/RecursionExample02.htm)
```javascript
function factorial(num){
    if (num <= 1){
        return 1;
    } else {
        return num * arguments.callee(num-1);
    }
}
var anotherFactorial = factorial;
factorial = null;
alert(anotherFactorial(4));  //24
```
========
[ClosureExample01](Ch07/ClosureExample01.htm)
```javascript
function createFunctions(){
    var result = new Array();

    for (var i=0; i < 10; i++){

        result[i] = function(){
            return i;
        };
    }

    return result;
}
var funcs = createFunctions();
//every function outputs 10
for (var i=0; i < funcs.length; i++){
    document.write(funcs[i]() + "<br />");
}
```
--------
### Why

* `funcs[i]` access variables in `createFunctions()` by reference
* `funcs[i]` access `i` by reference
* Not by value
========
[ClosureExample02](Ch07/ClosureExample02.htm)
```javascript
function createFunctions(){
    var result = new Array();
    for (var i=0; i < 10; i++){
        result[i] = function(num){
            return function(){
                return num;
            };
        }(i);
    }
    
    return result;
}
var funcs = createFunctions();
//every function outputs 10
for (var i=0; i < funcs.length; i++){
    document.write(funcs[i]() + "<br />");
}
```
--------
### Why

* `funcs[i]` access variables in `createFunctions()` by reference
* `funcs[i]` access `num` by value, since function parameter is passed by value
* `num` records the correct value of various `i`
========
[ThisObjectExample01](Ch07/ThisObjectExample01.htm)
```javascript
var name = "The Window";
var object = {
    name : "My Object",
    getNameFunc : function(){

        return function(){
            return this.name;
        };
    }
};
alert(object.getNameFunc()());  //"The Window"
```
--------
### Why

* Every function has a `this`
* Inside `getNameFunc`, `this` equals `object`
* Inside a anonymous function, `this` equals the global `window`.
========
[ThisObjectExample02](Ch07/ThisObjectExample02.htm)
```javascript
var name = "The Window";
var object = {
    name : "My Object",
    getNameFunc : function(){
        var that = this;
        return function(){
            return that.name;
        };
    }
};
alert(object.getNameFunc()());  //"MyObject"
```
--------
### Why

* `that` always equals to `this` of getNameFunc
* Problem solved
========
[ThisObjectExample03](Ch07/ThisObjectExample03.htm)
```javascript
var name = "The Window";
var object = {
    name : "My Object",

    getName: function(){
        return this.name;
    }
};
alert(object.getName());     //"My Object"
alert((object.getName)());   //"My Object"
alert((object.getName = object.getName)()); //"The Window" in non-strict mode
```
========
[BlockScopeExample01](Ch07/BlockScopeExample01.htm)
```javascript
function outputNumbers(count){
    for (var i=0; i < count; i++){
        alert(i);
    }

    alert(i);   //count
}

outputNumbers(5);
```
========
[BlockScopeExample02](Ch07/BlockScopeExample02.htm)
```javascript
function outputNumbers(count){
    for (var i=0; i < count; i++){
        alert(i);
    }
    var i;    //variable re-declared
    alert(i);   //count
}

outputNumbers(5);
```
========
[BlockScopeExample03](Ch07/BlockScopeExample03.htm)
```javascript
function outputNumbers(count){

    (function () {
        for (var i=0; i < count; i++){
            alert(i);
        }
    })();
    
    alert(i);   //causes an error
}

outputNumbers(5);
```
--------
### Why

* Varaible inside a function is private to that function
* You can fake C++ namespace with a function block
========
[PrivilegedMethodExample01](Ch07/PrivilegedMethodExample01.htm)
```javascript
function Person(name){

    this.getName = function(){
        return name;
    };

    this.setName = function (value) {
        name = value;
    };
}

var person = new Person("Nicholas");
alert(person.getName());   //"Nicholas"
person.setName("Greg");
alert(person.getName());   //"Greg"
```
========
[PrivilegedMethodExample02](Ch07/PrivilegedMethodExample02.htm)
```javascript
(function(){

    var name = "";
    
    Person = function(value){                
        name = value;                
    };
    
    Person.prototype.getName = function(){
        return name;
    };
    
    Person.prototype.setName = function (value){
        name = value;
    };
})();

var person1 = new Person("Nicholas");
alert(person1.getName());   //"Nicholas"
person1.setName("Greg");
alert(person1.getName());   //"Greg"
                   
var person2 = new Person("Michael");
alert(person1.getName());   //"Michael"
alert(person2.getName());   //"Michael"
```