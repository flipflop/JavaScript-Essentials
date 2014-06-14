## 1. JS Namespacing
 ```javascript
if (typeof mynamespace != "object") { var mynamespace = {}; }
mynamespace.component = function() { 
	// component safely nestled within a namespace  
};
 ```

## 2. Get a Class Name from Multiples
 ```javascript
$("#content").attr("class").split(" ")[0];
 ```

## 3. Argument Defaulting
 ```javascript
drawLines : function(lineheight) {
	lineheight = lineheight || "12px"; //default
	displayline(lineheight);
}
 ```

## 4. Toggle Display
 ```javascript
function toggle(obj) {
	obj.style.display = obj.style.display == "none" ? "" : "none";		
}
 ```

## 5. Cross Browser Event Reduction 
 ```javascript
document.onkeydown = function(e) {
	//return the right event	
	e = e || window.event;	
	//get keycode
	var keyCode = e.keyCode || e.which;
}
 ```

## 6. Code Convention for Module Pattern Component
 ```javascript	
// the typical anatomy of a component component.init( config ) 
// initialisation - accepts JSON for configuration options	

component.init // intialisation (optional self invoking), can be used pass through, unload, onDomReady or arbitrarily 
component.addEvents // event handling
component.display // display 
component.destroy // remove component and clean up reference onunload
 ```

## 7. Annonymous Immediately Invoking Function (IFF)
 ```javascript
// avoid global scope
// create a new annonymous function, to use as a wrapper
// from Pro JavaScript Techniques By John Resig
(function() {
	// The variable that would, normally, be global
	var msg = "Thanks for visiting!";
	
	// Binding a new function to a global object
	
	window.onload = function() {
		// Which uses the 'hidden' variable
		alert( msg );
	};
	
// Close off the annonymous function and execute it	
})();
 ```

## 8. Module Pattern Extended

[Reference:]( http://www.wait-till-i.com/2007/07/24/show-love-to-the-module-pattern/ )

 ```javascript
	
var myScript = function(){
  var pub = {};
  var massivelyLongVariableProbablyGerman = 1;
  function thisIsReallyLong(n){};
  function doStuff(n){};
  pub.init = function(){
    doStuff(massivelyLongVariableProbablyGerman);
    thisIsReallyLong(massivelyLongVariableProbablyGerman);
    pub.otherPublic();
  };
  pub.otherPublic = function(){
  };
  return pub;
}();
myScript.init();
 ```

## 9. Hash Table Methods or Handy NVP Data Storage
 ```javascript
var person = {
	drinkBeer : function() {
		alert("drinking...");
	},
	
	burp : function() {
		alert("burping...");
	},
	
	purge : function() {
		alert("purging...");
	}
};

// also
person.drinkBeer();

// or

person["drinkBeer"]();

// this could be a dynamic variable altered at runtime
var methodCall = "drinkBeer";

// call the relevant method	
person[methodCall]();
 ```

## 10. Quick 'n' Dirty ArrayContains
 ```javascript
alert( ['where','are','my', 'keys'].indexOf("keys") != -1 );

//or

if (['where','are','my', 'keys'].indexOf("keys").toString() != -1) {

}

// or

var obj = {};
var arr = [ 'foo', 'bar', 5, obj, 10 ];
console.log( arr.indexOf('bar') ); // prints: 1
 ```

## 11. Front End Performance Tip for string concatenation
 ```javascript
var stuckTogether = ["value1", "value2", "value3"].join(""); // Deprecated: use concat instead (see #34)
 ```

## 12. Module Pattern (public and private members within a namespace)
 ```javascript

jQuery.noConflict()
//Note: ; before parenthesis is deliberate
;(function ( container, document, $, undefined ) { // add in more parameters for context e.g. ( container, document, jQuery, utils ), pass in undefined so it can't be re-assigned (security)

	function createModule()  { // Revealing Module Pattern with execution context passed in arguments
		var localVariable = "local variable",
		myPublicProperty = "public variable",
		init = function() {
		
		}(); // self invoking
		
		function myPrivateMethod() {
			// not in contract list so remains private
		} // end myPrivateMethod

		function myPublicMethod() {
			return "public function";
		} // end myPublicMethod

		var contract = {
			myPublicProperty : myPublicProperty,
			myPublicMethod : myPublicMethod
		}

		// Public interface (properties and methods)
		return contract;

	} // end module

	// Public API (assigns to my namespace)
	container.ModuleName = createModule();

})( window.mynamespace || (window.mynamespace = {}), jQuery, document ); //end mynamespace.ModuleName (create namespace and context)
 ```

## 13. Multi Line Alternative to String Concatenation
 ```javascript

// careful using this with some build tools 

var myString = 	"some really long text repeated\n\
			 	some really long text repeated\n\
				some really long text repeated";
 ```
## 14. Faster Loops
 ```javascript

var itemsLen = items.length; // cache length - prevents evaluation on each loop

for(i=itemsLen; i--;)  { // looping backwards is faster
	//note: loop works in reverse
}
 ```

## 15. Closure to Encapsulate Lost Scope
 ```javascript

var listElements = document.getElementsByTagName("li");

for(var i=0; i < listElements.length; i++) {
    (function(inc) {
      listElements[inc].onclick = function() {
		alert(inc);
    };
  }(i));
}
 ```

## 16. Property Checking
 ```javascript

if ( foo == "bar" || foo == "foobar" || foo == "foo" ) {
 //...
}

// can be written as
if ( foo in { bar:1, foobar:1, foo:1 } ) {
 //...
}
 ```

## 17. jQuery Selector Caching
 ```javascript

var foo = $(".item").bind("click", function(){
	
	foo.not(this).addClass("bar");
		.removeClass("foobar");
		.fadeOut(500);

});
 ```

## 18. Force a Boolean
 ```javascript

function supports_canvas() {
  return !!document.createElement('canvas').getContext;
}

/*
if getContext gives you a "falsey" value, the !! will make it return the boolean value false. Otherwise it will return true.

The "falsey" values are:

false
NaN
undefined
null
"" (empty string)
0
*/
 ```

## 19.  Append an Array to Another Array
 ```javascript

var a = [4,5,6];
var b = [7,8,9];
Array.prototype.push.apply(a, b);

console.log(a); // is: [4, 5, 6, 7, 8, 9]
 ```

## 20. Order an Array and Get Highest or Lowest
 ```javascript
var list = [5,1,7,2,9,4,6,3,8],
	lowestNumber,
	highestNumber;

lowestNumber = list.sort(function(a,b){a = parseFloat(a);b = parseFloat(b);return a - b;})[0]; 
highestNumber = list.sort(function(a,b){a = parseFloat(a);b = parseFloat(b);return a - b;})[list.length-1]; 
console.log(highestNumber);
 ```

## 21. Shuffle an Array
 ```javascript
var list = [1,2,3,4,5,6,7,8,9];
list = list.sort(function() {return Math.random() - 0.5});
console.log(list); // prints something like: 4,3,1,2,9,5,6,7,8
 ```

## 22. SyntaxError (JavaScript 1.5)
 ```javascript
// raised when a syntax error occurs while parsing code in eval()
try {
	eval('1 + * 5'); // will rise a SyntaxError exception
} catch( ex ) {
	console.log( ex.constructor == SyntaxError ); // Prints true
}

// JavaScript 1.7
try {
	eval('1 + * 5');
} catch( ex if ex instanceof SyntaxError ) {
	console.log( 'SyntaxError !' ); // prints: SyntaxError !
}
 ```

## 23. Function Hijacking
 ```javascript

var obj = { // static object  
    // add function, supports adding 2 values  
    add: function(x, y) {  
        return x + y;  
    }  
};  
      
// move the existing function to another variable name  
obj.__add = obj.add;  
      
// override the existing function with your own, to support adding 2 or 3 values  
obj.add = function(x, y, z) {  
    var val = obj.__add(x, y);  
    return z ? val + z : val;  
}
 ```

## 24. Call a function in a parent class
 ```javascript
toto.prototype = new function() {
  this.a = function() {
    Print(456);
  }
};

function toto() {
  this.a = function(){
    Print(123);
    toto.prototype.a.call(this); // or: this.__proto__.a();
  }
}

var o = new toto;
o.a();
/*
prints:
 123
 456
*/
 ```

## 25. Add in Memoization example

[Reference:]( http://unscriptable.com/2009/05/01/a-better-javascript-memoizer/ )

[Reference:]( http://philogb.github.io/blog/2008/09/05/memoization-in-javascript/ )
 

## 26. Inheritance

[Reference]( https://developer.mozilla.org/en/Introduction_to_Object-Oriented_JavaScript )

 ```javascript

// define the Person Class  
function Person() {}  

Person.prototype.walk = function(){  
  alert ('I am walking!');  
};  

Person.prototype.sayHello = function(){  
  alert ('hello');  
};  

// define the Student class  
function Student() {  
  // Call the parent constructor  
  Person.call(this);  
}  

// inherit Person  
Student.prototype = new Person();  

// correct the constructor pointer because it points to Person  
Student.prototype.constructor = Student;  

// replace the sayHello method  
Student.prototype.sayHello = function(){  
  alert('hi, I am a student');  
}  

// add sayGoodBye method  
Student.prototype.sayGoodBye = function(){  
  alert('goodBye');  
}  

var student1 = new Student();  
student1.sayHello();  
student1.walk();  
student1.sayGoodBye();  

// check inheritance  
alert(student1 instanceof Person); // true   
alert(student1 instanceof Student); // true
 ```

## 27. Performant Strings

[Reference:]( http://dev.opera.com/articles/view/efficient-javascript/?page=1 )

 ```javascript

// This example requires the script engine to create 21 new string objects, once for each time the length property is accessed, and once each time the charAt method is called:
var s = '0123456789';
for( var i = 0; i < s.length; i++ ) {
  s.charAt(i);
}

// This equivalent example creates just a single object, and will perform better as a result:
var s = new String('0123456789');
for( var i = 0; i < s.length; i++ ) {
  s.charAt(i);
}
 ```

## 28. Padding a string (without code branching)
 ```javascript

('00' + 3).slice(-3)
// "003"
('00' + 42).slice(-3)
// "042"
('00' + 103).slice(-3)
// "103"
 ```

## 29. isArray()
 ```javascript

arr = 1 // That's a simple integer, of course.
Object.prototype.toString.call(arr) == '[object Array]';
// false
arr = '1' // Just a string.
Object.prototype.toString.call(arr) == '[object Array]';
// false
arr = '[1,2,3]' // Also a string.
Object.prototype.toString.call(arr) == '[object Array]';
// false
arr = {x:1, y:2} // That's an object, no array either!
Object.prototype.toString.call(arr) == '[object Array]';
// false
arr = [1,2,3] // An array, so it should be true.
Object.prototype.toString.call(arr) == '[object Array]';
// true
 ```

## 30. Range
 ```javascript

function range(start, stop) {
  for (var r = []; start < stop; r.push(start++));
  return r;
}
 ```

## 31. Is Array
 ```javascript

if(!Array.isArray) { 
  Array.isArray = function(v){ 
    return Object.prototype.toString.call(v) === '[object Array]'; 
  } 
}
 ```

## 32. Push State & Location Hash
 ```javascript
// Note: don't litter browser history, limit hashbang events
if (history.pushState) {
	history.pushState(null, '', '#', data);
} else {
	location.hash = data;
}
 ```

## 33. Convert to an Integer (instead of Math.floor) - possibly a faster alternative
 ```javascript

~~((image.width / image.height))
 ```

## 34. JavaScript Templates (also executes quickly - easy to read)
 ```javascript

var tmpl = ''.concat(
  '<div>',
    '<span>foo<span>',
  '</div>'
);
 ```

## 35. Quick indexOf in an Array

[Reference:]( http://www.javascriptturnsmeon.com/the-tilde-operator-in-javascript/ )

 ```javascript

var foo = [1, 2, 3, 4, 5];

if (!!~a.indexOf(5)) { //!! is used to reverse the boolean value to a positive
	console.log("found five");
}

 ```

## 36. Get a property from an Object (utilities)
 ```javascript

function splat (fn) {
  return function (list) {
    return Array.prototype.map.call(list, fn)
  }
}

function get (attr) {
  return function (object) { return object[attr]; }
}

var inventories = [
  { apples: 0, oranges: 144, eggs: 36 },
  { apples: 240, oranges: 54, eggs: 12 },
  { apples: 24, oranges: 12, eggs: 42 }
];

var inventory = {
  "apples": 0,
  "oranges": 144,
  "eggs": 36
};

console.log(get('oranges')(inventory));
console.log(splat(get('oranges'))(inventories));
 ```

## 37. Reverse a string
 ```javascript
function reverse(s) {
    return s.split("").reverse().join("");
}
 ```
 
## 38. JavaScript Truncation Operator
 ```
3.1|0 == 3

3.9|0 == 3

-10.9|0 == 10
 ```
 
## 39. Quick charAt in String
 ```
"foo"[2]
// returns "o"
 ```
 
 
 

