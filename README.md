# repeatJS
A simple, yet highly customizable plugin to handle all of you're client-side repetitive DOM needs. Simple, quick and powerful templating.


# About
repeatJS is a simple repeating templating tool. Is is modeled after ng-repeat and shares some basic syntax, but is not a clone.

* repeatJS requires jQuery and Mustache to run.

## Template
To set up a repeat template, write any element tag you wish to repeat once where you want the repeating to start, this will serve as the template and starting point.

Simply add a repeatJS attribute with a unique value for the reference name for that template, in this case myRepeat. To add variables place the name in double curly brackets {{ name }} .
```html
<p jq-repeat="myRepeat">
    {{ character }} in English {{spelling}}
</p>
```
## Insert
Now that you have a template set up, let's populate the template use $.scope.myRepeat.push()
```javaScript
$.scope.myRepeat.push( { character: 1, spelling: 'one' } )
```
You can add any number of values as arguments you wish and each will create a new element from the template. Values must be supplied as objects with keys corresponding to the variable names used in the template.
```javaScript
$.scope.myRepeat.push({
    character: 1,
    spelling: 'one'
}, {
    character: 2,
    spelling: 'two'
}, {
    character: 3,
    spelling: 'three'
});
```
## Methods
The repeat object can take may methods used for array's and holds as an array of the objects being repeated.

* `$.scope.myRepeat.splice(index [, howMany] [,ToAdd])` functions exactly as a regular array with notable difference. If the index propriety is set a string can be passed as the value of the index.
 * **index**
Type: Number or String
Index of element you wish to manipulate. If the .index property is set, you may pass a string to match to the index array.
 * howMany
Type: Number
Number of repeat objects that will be removed.
Of there are non to be removed, it is not required to use this argument.
 * update
Type: Array
This is the array of repeat objects to add.
If there are none to this is not required.
 * returns
Type: Array
This function will return an array of deleted elements.
* `$.scope.myRepeat.pop()` Will remove and return the last element in the repeat array
* `$.scope.myRepeat.reverse()` Will reverse the repeat array by index number.todo: if .index is a number, will use that. Returns the newly formated array.
* `$.scope.myRepeat.shift()` works the same as regular arrays.
* `$.scope.myRepeat.loop()` will take the last value and insert in the front. .loopUp() does the opposite. Returns the newly formated array.
* `$.scope.myRepeat.indexOf( key, value )` Returns the array index number of the matching element. Mostly used for internals.
  * key
Type: String
The key element to match.
  * value
Type: String
The value of the matching element.
* `$.scope.myRepeat.update( [key,] value, update)` Updates selected value with new data. The selection process is done by matching key, value pairs from the existing objects,
  * key
Type: String
The key of the matching element to update. If no value is given the index will be used.
  * value
Type: String
The value of the matching key to the element to be update.If the index key will be used, this can be the first argument.
  * update
Type: Object
This is the object that will be applied to the matching element.
* `$.scope.myRepeat.__put` is the function that will run when a element is being inserted. This must be a function and must include this.show(), or some other way of un-hiding 'this'.
* `$.scope.myRepeat.__take` is the function that will run when an element is being removes. This must be a function and include this.remove() or some other way to remove 'this'.
* `$scope.myRepeat.__index` is the propriety that defines the object key to use an the index. If this is set, a string can be used inplace of a number for any index reference.