# Syntax

This document shows some basic syntax of the `jai` language.

* Keep in mind that syntax is not yet final, and can easily differ from this document at any time.
* For now, each `jai` code block is marked as `c++` for syntax highlighting purposes.

## Functions

```c++
main :: () {
	print("Hello, world!");
}
```

## Variable Assignment

TODO

```c++
x = 3.0;
x := 3.0;
x : int;
```

## for

```c++
for 1..3  print("% ", it);
// Output:
// 1 2 3 

for < 1..3  print("%\n", it);
// Output:
// 3 2 1 
```

## cast( )

Type casting  in `jai` is performed by putting `cast(<type>)` in front of the value being cast.

```c++
x := 3;
y := 4.5 + cast(float) x;
```

## enum

Enumerations in `jai` can be declared with the `enum` keyword.

```c++
Animal :: enum {
	DOG,
	CAT,
	ZEBRA,
}
```

## switch

The `switch` statement in `jai` is done with an `if` syntax.

* You can `switch` over all the fundamental types of the language.
* `jai` does not require break statements to exit the `switch`. Each case breaks automatically unless [#through](#through) is applied to it.
* Each `case` is a separate scope.

```c++
the_animal = "Dog";

if the_animal == {
	case: "Dog";
		print("Woof!\n");
	case: "Cat";
		print("Meow!\n");
	case;
		print("Default case!\n");
}

// Output:
// Woof!
```

### #through

The `#through` directive allows control flow to pass on to the next `case` in the [switch](#switch).

```c++
if the_animal == {
	case: "Dog";
		print("Woof!\n");
		#through;
	case: "Cat";
		print("Meow!\n");
	case;
		print("Default case!\n");
}

// Output:
// Woof!
// Meow!
```

### #complete

The `#complete` syntax on the [switch](#switch) allows you to make compilation fail with errors if the [switch](#switch) does not include every value of an [enum](#enum).

* `#complete` only applies to `enum`.

```c++
Animal :: enum {
	DOG,
	CAT,
	ZEBRA,
}

main :: () {
	
	using Animal;
	
	the_animal := DOG;
	
	if #complete the_animal == {
        case: "Dog";
            print("Woof!\n");
        case: "Cat";
            print("Meow!\n");
        case;
            print("Default case!\n");
	}
	
}

// Output may look something like:
// Error: This 'if' was marked #complete but the following enum value was missing:
// ZEBRA,
```
