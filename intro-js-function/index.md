## function() {};
========
### I have a name
```
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
```
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
```
function functionName(){
    //noop
}

//works only in Firefox, Safari, Chrome, and Opera
alert(functionName.name); //"functionName"
```
========
[FunctionDeclarationHoisting01](Ch07/FunctionDeclarationHoisting01.htm)
```
sayHi();
function sayHi(){
    alert("Hi!");
}
```
========
[FunctionDeclarationsErrorExample01](Ch07/FunctionDeclarationsErrorExample01.htm)
```
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
```
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
```
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
```
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
========
[ClosureExample02](Ch07/ClosureExample02.htm)
```
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
========
[ThisObjectExample01](Ch07/ThisObjectExample01.htm)
```
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
========
[ThisObjectExample02](Ch07/ThisObjectExample02.htm)
```
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
========
[ThisObjectExample03](Ch07/ThisObjectExample03.htm)
```
var name = "The Window";
var object = {
    name : "My Object",
    getName: function(){
        return this.name;
    }
};
alert(object.getName());     //"My Object"
alert((object.getName)());   //"My Object"
alert((object.getName = object.getName)());   //"The Window" in non-strict mode
```

