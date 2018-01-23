[tags]: / "reflection,dead-code-elimination"

# Invoke object method by string

To invoke method by it's name you will need to 

This snippet shows how to use a string as a variable identifier using reflection.

## Implementation
```haxe
class MyClass {
    public function new () {}
    @:keep public function printName() {
        trace("MyClass printName is invoked");
    }
}
```

## Usage
```haxe
class Test {
    static function main() {
        trace("Haxe is great!");
        var myObject = new MyClass();
        var f = Reflect.field(myObject, "yo");
        Reflect.callMethod(myObject, cast f, []);
    }
}
```

Haxe has [dead code elimination](https://haxe.org/manual/cr-dce.html) (DCE). This compiler feature identifies and eliminates all unused code during compilation. In the example above, the method `printName()` is used by reflection and has no direct call in the code. Such code deleted in compile time by DCE. To keep after compilation switch off DCE or mark this such method by `@:keep` [metadata](https://haxe.org/manual/cr-metadata.html) to the `myField` field.

**Tip:** Haxe has a wonderful type system, use this as much as possible. Reflection can be a powerful tool, but it's important to know it can be error prone, since the compiler can never validate if what you're doing makes sense and is also harder to optimize.

> **More information:**
> 
> * [Reflection documentation](http://haxe.org/manual/std-reflection.html)  
> * [Reflect API Documentation](http://api.haxe.org/Reflect.html)  
>
> Author: [Alexey](https://github.com/alexey-kolonitsky)



