[tags]: / "array, collections, data-structures"

# Using arrays

In Haxe, the `Array` type represents a collection of elements ordered by their index (order number) in the collection.

### Creation

Arrays can be created by using the array syntax (`[]`), or by using a constructor. The constructor requires a type parameter to be passed, which specifies the type of the elements in the array. When the array syntax is used, the casting determines the type of array constructed.

```haxe
// Creating an array using array syntax
var arrayOfStrings:Array<String> = ["Apple", "Pear", "Banana"];
trace(arrayOfStrings);

// Creating an array with float values
var arrayOfFloats = [10.2, 40.5, 60.3];
trace(arrayOfFloats);
```

#### Array comprehension

As an alternative, [array comprehension](https://haxe.org/manual/lf-array-comprehension.html) can be used. This makes it possible to use some programming logic in `for` or `while` expressions:

```haxe
var aInts = [for(i in 0...5) i];
trace(aInts); // [0,1,2,3,4]

var aEvens = [for(i in 0...5) i*2];
trace(aEvens); // [0,2,4,6,8]

var aChars = [for(c in 65...70) String.fromCharCode(c)];
trace(aChars); // ['A','B','C','D','E']         

var x = 1;
var aBits = [while(x < 128) x = x * 2];
trace(aBits); // [2,4,8,16,32,64,128]
```

### Adding elements

An element can be inserted into an array at a desired position, prepended to the start of the array, or appended to the end of the array. Multiple elements can be appended to an array through concatenation.

```haxe
var arrayOfStrings:Array<String> = [];
// Adds "Hello" at index 0, offsetting elements to the right by one position
arrayOfStrings.insert(0, "Hello");
// Prepends "Haxe" to the start of the array
arrayOfStrings.unshift("Haxe");
// Appends "World" to the end of the array 
arrayOfStrings.push("World");
// Appends "foo", "bar" elements to the end of a copy of the array
arrayOfStrings = arrayOfStrings.concat(["foo", "bar"]);
```

### Removing elements

Elements can be removed from an array by removing a specific element of the array, a range of elements in the array, the first element of the array, or the last element of the array.

```haxe
var arrayOfStrings:Array<String> = ["Hi", "Everyone", "Nice", "To", "Meet", "You"];
// Removes first occurence of "Hello" in the array
arrayOfStrings.remove("Hello");
// Removes and returns three elements beginning with (and including) index 0
arrayOfStrings.splice(0, 3);
// Removes and returns first element of the array
arrayOfStrings.shift();
// Removes and returns last element of the array
arrayOfStrings.pop();
```

### Retrieving elements

Array elements can be accessed through array notation, using the index of the element in the array.

```haxe
var arrayOfStrings:Array<String> = ["first", "foo", "middle", "foo", "last"];
// Retrieves first array element
var first = arrayOfStrings[0];
// Retrieves last array element
var last = arrayOfStrings[arrayOfStrings.length - 1];
// Retrieves first occurrence of "foo" string
var firstOccurrence = arrayOfStrings[arrayOfStrings.indexOf("foo")];
// Retrieves last occurrence of "foo" string
var lastOccurrence = arrayOfStrings[arrayOfStrings.lastIndexOf("foo")];
```

### Iteration

The array defines an iterator, and its elements can therefore be iterated over.

```haxe
for (item in arrayOfStrings) {
    // do something
}
```

### Operations

#### Copy

Array elements can be copied into a new array.

```haxe
var arrayOfStrings:Array<String> = ["first", "second", "last"];
var newArrayOfStrings = arrayOfStrings.copy();
newArrayOfStrings.push("best");
trace(arrayOfStrings); // ["first", "second", "last"];
trace(newArrayOfStrings); // ["first", "second", "last", "best"];
```

#### Filter

Array elements can be filtered into a new array with a filtering function. Every array element for which the filtering function returns `true` is added to a new array.

```haxe
var arrayOfStrings:Array<String> = ["first", "second", "last"];
var noEmptyStrings = arrayOfStrings.filter(function (e) return e != "");
```

#### Map

Array elements can be mapped into a new array with a mapping function. The mapping is bijective, and every element from the initial array will have its mapping in the new array.

```haxe
var arrayOfStrings:Array<String> = ["first", "second", "last"];
var upperCaseStrings = arrayOfStrings.map(function (e) return e.toUpperCase());
```

#### Reverse

The order of elements in an array can be reversed.

```haxe
var arrayOfStrings:Array<String> = ["first", "second", "last"];
arrayOfStrings.reverse();
```

#### Slice

A specific range of array elements from a starting index up to (excluding) an end index can be copied to a new array.

```haxe
var arrayOfStrings:Array<String> = ["first", "second", "last"];
var stringsThreeAndFour = arrayOfStrings.slice(1, 2);
``` 

#### Sort

Array elements can be sorted according to a comparison function. The comparison function compares two elements (the predecessor and the successor), and must return an `Int`. A return value of 0 indicates the elements are equivalent, a positive return value gives way to the successor, and a negative return value gives way to the predecessor.

```haxe
var arrayOfStrings:Array<String> = ["first", "second", "last"];
arrayOfStrings.sort(function (a, b) return a.charCodeAt(0) - b.charCodeAt(0));
```

### Displaying contents

Arrays can be prepared for printing by joining the elements together with a separator character, or by using the string representation of the array structure.

```haxe
var arrayOfStrings:Array<String> = ["first", "second", "last"];
// Returns a string of array elements concatenated by separator string
var withSeparator:String = arrayOfStrings.join(" / ");
// Returns a string representation of the array structure
var asStructure:String = arrayOfStrings.toString();
```

> [Array API documentation](http://api.haxe.org/Array.html)
> 
> [Array manual entry](http://haxe.org/manual/std-Array.html)
>
> Author: [Domagoj Štrekelj](https://github.com/dstrekelj)
