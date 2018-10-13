# Swift Cheat Sheet

Notes taken from [The Swift Programming Language](https://developer.apple.com/library/ios/documentation/swift/conceptual/Swift_Programming_Language/TheBasics.html#//apple_ref/doc/uid/TP40014097-CH5-XID_467).

## Topics

- [The Basics](#the-basics)
- [Basic Operators](#basic-operators)
- [Strings and Characters](#strings-and-characters)
- [Collection Types](#collection-types)
- [Control Flow](#control-flow)
- [Functions](#functions)
- [Closures](#closures)
- [Enumerations](#enumerations)
- [Classes & Structures](#classes--structures)
- [Properties](#properties)
- [Methods](#methods)
- [Subscripts](#subscripts)
- [Inheritance](#inheritance)
- [Initialization](#initialization)
- [Deinitialization](#deinitialization)
- [Automatic Reference Counting](#automatic-reference-counting)
- [Optional Chaining](#optional-chaining)
- [Type Casting](#type-casting)
- [Nested Types](#nested-types)
- [Extensions](#extensions)
- [Protocols](#protocols)
- [Generics](#generics)
- [Access Control](#access-control)

## The Basics

### Constants & Variables

  * Declaring Constants & Variables

      ```swift
      // Constant
      let maximumNumberOfLoginAttempts = 10

      // Variable
      var currentLoginAttempt = 0
      var x = 0.0, y = 0.0, z = 0.0
      ```

  * Type Annotations

    ```swift
    var welcomeMessage: String
    var red, green, blue: Double
    ```

    * Rare that you need to write type annotations
      * If you provide an initial value, Swift can infer the type to be used
  * Naming Constants and Variables
    * Constant/variable names can contain almost any character, including Unicode:

      ```swift
      let π = 3.14159
      let 你好 = "你好世界"
      let  = "dogcow"
      ```

    * If const/var is reserved Swift keyword, surround with back ticks (\`), avoid if you can
  * Printing Constants & Variables

    ```swift
    println(friendlyWelcome)
    println("Current value \(friendlyWelcome)")
    ```

### Comments

```swift
// this is a comment
/* multiple lines comment */
/* /* nested multilines supported */ */
```

### Semicolons

```swift
// No semicolon, unless for multiple statements on a single line
let cat="hello"; println(cat)
```

### Integers

  * Whole numbers with no fractional component, signed or unsigned
  * Swift provides signed & unsigned integers in 8, 16, 32 and 64 bits
    * Follow naming convention similar to C, e.g.
      * UInt8
      * Int32
  * Integer Bounds

    ```swift
    let minValue = UInt8.min // 0
    let maxValue = UInt8.max // 255
    ```

  * Int
    * If you don't need specific size, use Int, same size with current platform's native word size
      * 32-bit platform, Int = Int32
      * 64-bit platform, Int = Int64
    * Unless you need to use specific size, always use Int, for codes consistency and interoperability.
    * On 32-bit platform Int values: -2,147,483,648 => 2,147,483,648, large enough
  * UInt
    * When you specifically need unsigned integer, else Int is preferred
    * A consistent use of Int aids code interoperability, avoids the need to convert to different number types, matches integer type inference as described in Type Safety and Type Inference

### Floating Point Numbers

  * Numbers with a fractional component, e.g. 3.14159
  * Represent a much wider range of values than integer types
  * Can store numbers much larger/smaller than can be stored in an Int
  * Types:
    * Double
      * 64-bit floating point number
        * Use it when floating-point values must be very large or particularly precise
    * Float
      * 32-bit floating point number
        * Use it when floating point values do not require 64-bit precision
  * Double has a precision of at least 15 decimal digits, and Float 6 decimal digits

### Type Safety and Type Inference

  * Type safe language
    * Encourages you to be clear about types of values
    * Type checking, compile errors if there is a mismatch
  * Type Inference
    * Does not mean you nave to specify the type of every constant/variable
    * Enables a compiler to deduce the type of a particular expression automatically by examining the values you provide
    * Because of type inference, Swift requires fewer type of declarations than C or Objective-C

    ```swift
    let meaningOfLife = 42    // Inferred as Int
    let pi = 3.14159          // Infered as double, Swift always chooses Double rather than Float
    let anotherPi  = 3 + 0.14 // Also inferred as double
    ```

### Numeric Literals

  * All of these integer literals have a decimal value of 17:

    ```swift
    let decimalInteger = 17
    let binaryInteger = 0b10001   // 17 in binary notation
    let octalInteger = 0o21       // 17 in octal notation
    let hexadecimalInteger = 0x11 // 17 hexa decimal notation
    ```

  * Floating-point literals can be decimal or hexadecimal.They must have a number on both sides of the decimal point
    * Optional exponent, indicated by and uppercase/lowercase e for decimal floats or an p for hexadecimal floats
    * For decimal numbers with an exponent of exp, the base number is multiplied by 10exp:

      ```swift
      1.25e2  // = 1.25 x 102 = 125.0
      1.25e-2 // = 1.25 x 10-2 = 0.0125
      ```

    * For hexadecimal numbers with an exponent of exp, the base is multiplied by 2exp:

      ```swift
      0xFp2 // means 15x22 = 60.0
      0xFp2 // means 15x2-2 = 3.75
      ```

    * All of these floating numbers have a decimal value of 12.1875

      ```swift
      let decimalDouble = 12.1875
      let exponentDouble = 1.21875e1
      let hexDouble = 0xC.3p0
      ```

  * Numeric literals can contain extra formatting to make them easier to read
    * Padded with extra zeroes or contain underscores
    * Not affecting the value:

      ```swift
      let paddedDouble = 000123.456
      let oneMillion = 1_000_000
      let justOverOneMillion = 1_000_000.000_000_1
      ```

### Numeric Type Conversion

  * Overview
    * Use Int for most of the cases
    * Use others only when needed
    * Use others to catch any accidental value overflows & implicitly documents the nature of data being used
  * Integer Conversion
    * Compilation error if a number does not fit into a variable integer type

      ```swift
      let cannotBeNegative: UInt8 = -1
      ```

    * Because of limited range of values, you must opt in to number type conversion on a case-by-case basis
    * Opt-in approach prevents hidden conversion errors
    * To convert:

      ```swift
      * let twoThousand: UInt16 = 2_000
      * let one: UInt 8 - 1
      * let twoThousandAndOne = twoThousand + UInt16(one)
      ```

    * SomeType(ofInitialValue) => default in Swift and pass in an initial value
      * UInt16 has initialiser that accepts a UInt8 value
      * You can't pass in any type here, it has to be a type which UInt16 provides an init
      * Extending inits to cover other types covered in Extensions
  * Integer & Floating Point Conversion
    * Conversion between integer to floating point has to be explicit:

      ```swift
      let three = 3
      let floatNumber = 0.14
      let pi = Double(three) + floatNumber
      let intPi = Int(pi) // 3
      ```

    * Rules for combining numeric constants/variables are different than numeric literals

      ```swift
      let c = 3 + 0.14 // is fine
      ```

      * Because their type is inferred only at the point they are evaluated by the compiler

### Type Aliases

  * Define alternative name for an existing type
  * When you want to refer to an existing type by a name, that is contextually more appropriate
  * When working with data of a specific size from an external source

    ```swift
    typealias AudioSample = UInt16
    var maxAmplitudeFound = AudioSample.min // UInt16.min = 0
    ```

### Booleans

  * Bool

    ```swift
    let orangesAreOrange = true
    ```

  * Type safety prevents this:

    ```swift
    let i = 1
    if i { // error }
    if i == 1 { // fine }
    ```

### Tuples

  * Group multiple values into a single compound value
  * Values do not have to be the same type as each other

    ```swift
    let http404Error = (404, "Not found")
    let (statusCode, statusMessage) = http404Error
    let (justStatusCode, _) = http404Error
    println("Status code is \(http404Error.0), message: \(http404Error.1)")
    let http200Status = (statusCode: 200, description: "OK")
    println("Status code: \(http200Status.statusCode)")
    ```

  * Useful to return values of  functions, by returning a tuple with two distinct values, each of a different type the function provides more useful info about its outcome
  * Note
    * Tuples useful for temporary groups of related values, not suited for creation of complex data structures
    * If data structure likely to persist beyond a temp scope, model it as a class or structure.

### Optionals

  * Use optional where a value may be present
  * If there is a value, it equals to x, or there isn't a value at all
  * Note
    * Optionals don't exist in C/Obj-C. Nearest is to return nil.
    * Only works for objects, doesn't work for structures, basic C types, and enums.
    * Usually Obj-C methods return a special value NSNotFound to indicate absence of a a value
    * Swift optionals let you indicate the absence of a value for any type at all

      ```swift
      let possibleNumber = "123"
      let convertedNumber = possibleNumber.toInt()  // converted number is inferred to be of type "Int?" or "optional Int"
      ```

      * Because toInt might fail
      * Optional Int is written as Int?
  * nil
    * Set an optional variable to a valueless by assigning to nil

      ```swift
      var serverResponseCode: Int? = 404 // 404
      serverResponseCode = nil  // no value
      ```

    * nil cannot be used with non optional constants/variables
    * If your variables/constants may not have any value, use optional
    * Default to nil

      ```swift
      var surveyAnswer: String? // nil
      ```

    * Note
      * Swift's nil is different from Objective-C's.
      * In Objective-C nil is a pointer to a nonexistent object
      * In Swift it is not a pointer, it is an absence value of a certain type
      * Optionals of any type can be set to nil, not just object types
  * If statements & Forced Unwrapping

    ```swift
    if convertedNumber != nil {
      println("Coverted value: \(convertedValue)!"))
    }
    ```

    * Trying to use ! to access non-existent optional value will trigger an error
  * Optional Binding
    * To find out whether an optional contains a value, if so make the value available as a temporary constant or variable
    * Can be used in if/while statement

      ```swift
      if let constantName = someOptional {
        // statements
      }
      ```

  * Implicitly Unwrapped Optionals
    * Sometimes it is clear that an optional will always have a value
    * To remove the need to check and unwrap optional's value every time it is accessed

      ```swift
      let assumedString: String! = "Implicitly unwrapped"
      let implicitString: String = unassumedString

      if assumedString != nil { println(assumedString) }

      if let definiteString = assumedString { ... }
      ```

    * If you try to access an implicitly unwrapped optional when it does not contain value, it will trigger runtime error, same with optional

### Assertions

  * Some cases, not possible for code to continue, use assertions end code execution, to provide an opportunity to debug

    ```swift
    let age = -3
    assert(age >=0, "A person's age cannot be less than 0)
    ```

  * When to use Assertions
    * An integer subscript index is passed to a custom subscript implementation, but the subscript index value could be too low or too high
    * Value passed to a function, check for invalid value
    * An optional value is currently nil, but a non-nil value is essential for subsequent code to execute
  * Assertion cause app to terminate, an effective way to check conditions before app is published

## Basic Operators

### Overview

  * Operator is a special symbol or phrase that you use to check, change or combine values
  * Supports most standard C operators, and improves several capabilities to eliminate common coding errors
    * Assignment (=) does not return a value, to prevent mistakenly used for ===
    * Arithmetic operators (+, -...) detect and disallow value overflow to avoid unexpected result
    * You can opt-in to value overflow behaviour using Swift's overflow operator in "Overflow Operators"
    * C lets you perform remainder(%) operator on floating numbers
    * Provides two range operators a...<b and a...b

### Terminology

```swift
// Unary
prefix: !b
postfix: i++

// Binary
2 + 3

// Ternary
a ? b : c
```

### Assignment Operator

  ```swift
  let b = 10
  let (x,y) = (1,2)
  if x = y { // invalid }
  ```

  * Does not allow value to be overflow
  * You can option to value overflow behaviour by using

    ```swift
    a &+ b
    ```

  * Addition operator also supported for string "hello " + "world"
  * Two Character values, one char, one String, can be added together

    ```swift
    let dog :Character = ""
    let cow: Character = ""
    let dogCow = dog + cow
    // dogCow is equal to "
    ```

### Arithmetic Operators

  * Overview
    * Addition (+)
    * Substraction (-)
    * MUltiplication (*)
    * Division (/)
  * Remainder Operator
    * Works out how many multiples b will fit inside a and returns the value that is left over (remainder)
    * Known as modulo operator, its behaviour in Swift for negative numbers, strictly speaking a remainder rather than a modulo operation
    * Formula:

      ```swift
      a % b
      a = (b × some multiplier) + remainder
      ```
    * Example:

      ```swift
      9 % 4 = 1
      -9 % 4 = -1
      9 % -4 = 1
      ```

  * Floating-Point Remainder Calculations
    * Unlike the remainder operator in C or Obj-C, it also works on floating-point numbers:

      ```swift
      8 % 2.5 // = 0.5
      ```

  * Increment & Decrement Operators
    * ++ and ---

      ```swift
      var i = 0
      ++i // i = 1
      ```

    * If used as prefix, it increments the variable before returning its value
    * If used as suffix, it increments the variable after returning its value

      ```swift
      var a = 0
      let b = ++a // b = 1
      let c = a++ // a = 2, but c = 1
      ```

  * Unary Plus Operator

    ```swift
    let three = 3
    let minusTree = -three    // -3
    let plusTree = -minusTree // 3
    ```

    * Prepended without any space
  * Unary Plus Operator
    * Returns the value without any change

      ```swift
      let minusSix = -6
      let alsoMinusSix = +minusSix // -6
      ```

### Compound Assignment Operators

  * +=, -=

    ```swift
    var a = 1
    a += 2 // a = a + 2
    ```

  * Does not return a value

### Comparison Operators

  * Supports all standard C comparison operators

    ```swift
    a == b
    a != b
    a > b
    a < b
    a >= b
    a <= b
    ```

  * Swift also provides two identity operators === and !==
    * Test two object references both refer to the same object instance

### Ternary Conditional Operator

  * question ? answer1 : answer2

### Nil Coalescing Operator

  * a ?? b
  * Unwraps an optional a if it contains a value or returns a default value b if a is nil
  * a is always an optional type
  * Shorthand for

    ```swift
    a != nil ? a! : b
    ```

### Range Operators

  * Closed Range Operator
    * a..b
    * Defines a range that runs from a to be, and includes the values of a and b

    ```swift
    for index in 1...5 { ... }
    ```

  * Half-Open Range Operator

    ```swift
    a..<b
    ```

    * Defines a range that runs from a to b, but does not include b
    * Useful when work with zero-based lists, such as arrays

      ```swift
      let names = ["Anna", "Alex", "Brian", "Jack"]
      let count = names.count
      for i in 0..<count {
        println("Person \(i + 1) is called \(names[i])")
      }
      ```

### Logical Operators

  * Logical Not Operator (!a)
    * Inverts Boolean value, true becomes false and vice versa
  * Logical AND Operator (a && b)
  * Logical OR Operator (a || b)
  * Combining Logical Operators

    ```swift
    if enteredDoorCode && passedRetinaScan || hasDoorKey || knowsOverridePassword
    ```

  * Explicit Parantheses

    ```swift
    if (enteredDoorCode && passedRetinaScan) || hasDoorKey || knowsOverridePassword {
    ```

## Strings and Characters

### Overview

  ```swift
  "hello world"
  ```

  * Represented by String, a collection of values of Character type
  * Unicode compliant
  * Swift's string is bridged seamlessly to Foundation's NSString, the entire NSString API is available to call on any String value you create, in addition to the String features described later on.
  * You can also use String value with any API that requires NSString instance
  * More info, check Using Swift with Cocoa & Obj-C

### String Literals

```swift
let someString = "Some string literal value"
```

### Initializing an Empty String

```swift
var emptyString = ""
var anotherEmptyString = String()

emptyString == anotherEmptyString

if emptyString.isEmpty { ... }
```

### String Mutability

```swift
let constantString = "hello"
constantString += " world"   // compilation error
```

### String Are Value Types

  * String value is copied when it is passed to a function or method or
    * when it is assigned to a constant or a variable
  * New copy is created, passed and assigned not the original version
  * Note
    * Different from NSString in Cocoa, it is also pass by reference
  * Behind the scenes, Swift's compiler optimises string usage, so copying only takes place when necessary

### Working with Characters

  * Strings are collection of characters

    ```swift
    for char in "Dog!" { println(char) }
    ```

  * Create a single character

    ```swift
    let yenSign: Character = "¥"
    ```

### Concatenating Strings & Characters

  ```swift
  var welcome = "string1" + "string2"
  welcome.append("!")
  ```

### String Interpolation

  ```swift
  let multiplier = 3
  let message = "\(multiplier) times 2.5 is \(Double(multiplier) * 2.5)"
  ```

### Unicode

  * An international standard for encoding, representing, and processing text in different writing systems
    * Represent characters from any language in standardised form, and to read/write those chars to and from external source such as text file or web page
  * Unicode Scalars
    * Swift's native String type is built from Unicode scalar values.
    * A unique 21-bit number for a character/modifier such as:
      * U+0061 for LATIN SMALL LETTER A ("a")
      * U+1F425 for FRONT-FACING BABY CHICK ("")
    * Note
      * Unicode scalara is any unicode code point in the range of U+0000 to U+D7FF inclusive or U+E000 to U+10FFFF inclusive.
      * Unicode scalars do not include the Unicode surrogate pair code points, which are code points in the range of U+D800 to U+DFFF inclusive
    * Not all 21-bit Unicode scalars are assigned to a char, some are reserved for future assignment
  * Special Unicode Characters in String Literals
    * \0: null character
    * \\: backslash
    * \t: horizontal tab
    * \n: line feed
    * \r: carriage return
    * \": double quote
    * \': single quote
    * An arbitrary unicode scalar, written as \u{n}, where n is between one and eight hexadecimal digits

      ```swift
      "\u{24}"    // $
      "\u{2665}"  // ♥
      "\u{1F496}" //   - Unicode scalar: U+1F496
      ```

  * Extended Grapheme Clusters
    * Every instance of Swift's Character type represents a single extended grapheme cluster
      * A sequence of one or more Unicode scalars that (when combined) produce a single human-readable character

      ```swift
      let eAcute: Character = "\u{E9}"                         // é
      let combinedEAcute: Character = "\u{65}\u{301}"          // e followed by ́eAcute is é, combinedEAcute is é
      ```

    * To represent many complex script characters as a single character value.
      * Hangul syllables from the Korean alphabet, can be represented as either a precomposed or decomposed sequence

      ```swift
      let precomposed: Character = "\u{D55C}"                 // 한
      let decomposed: Character = "\u{1112}\u{1161}\u{11AB}"  // ᄒ, ᅡ,  precomposed is 한, decomposed is 한
      let enclosedEAcute: Character = "\u{E9}\u{20DD}"        // enclosedEAcute is  é⃝
      ```

### Counting Characters

  ```swift
  let unusualMenagerie = "Koala , Snail , Penguin , Dromedary"
  println("unusualMenagerie has \(countElements(unusualMenagerie)) character
  // prints "unusualMenagerie has 40 characters
  ```

  * Use of extended grapheme clusters for Character values means character count may not be affected

    ```swift
    var word = "cafe" +  "\u{301}"  // café
    countElements(word)             // 4
    ```

  * Note
    * The number of chars in a string cannot be calculated without iterating through the whole string, beware of countElements must iterate over the whole string
    * countElements is not the same with length
      * length is based on the number of 16-bit code units within the string's UTF-16 representation, not the number of Unicode extended grapheme clusters within the string
        * To reflect this fact, the length property from NSString is called utf16Count when it is accessed on a Swift String value

### Comparing Strings

  * String & Character Equality
    * == and !=
    * Two String values (or two Character values) are considered equal if their extended grapheme clusters are canonically equivalent
      * If they have the same linguistic metalling or appearance, even if they are composed from different Unicode scalars behind the scene

    ```swift
    "\u{E9}" == "\u{65}\u{301}" //  é - true
    "\u{41}" == "\u{0410}" // false - latinCapitalLetterA & cyrillicCapitalLetterA different linguistic meaning
    ```

    * Note
      * String and character comparisons in Swift are not locale sensitive
  * Prefix & Suffix Equality
    * hasPrefix, hasSuffix

### Unicode Representations of Strings

  * UTF-8 Representation
    * When written to a file, Unicode scalars are encoded in one of several Unicode-defined encoding forms.
    * Each form encodes the string in small chunks known as code units, which include:
      * UTF-8 encoding form, as 8-bit code units
      * UTF-16
      * UTF-32
    * Several ways to access Unicode representation of strings
      * Iterate with for-in, access each Character values as Unicode extended grapheme clusters.
      * Access a String value in one of the three Unicode-compliant representation
        * Collection of UTF-8 code units (string's utf8 property)
        * Collection of UTF-16 units (utf16 property)
        * Collection of 21-bit Unitcode scalar values, or equivalent to UTF-32 encoding form (unicodeScalars property)
    * Next is an example different presentation of D, o, g, !! (double exclamation mark, U+203c) and (U+1F436)
      * let dogString = "Dog‼"
  * UTF-8 Representation

    ```swift
    for codeUnit in dogString.utf8 {
      print("\(codeUnit) ")
    }
    print("\n")
    // 68 111 103 226 128 188 240 159 144 182
    //  68, 111, 103 = D, o, g
    //  226, 128, 188 = 3-byte UTF-8 representation of DOUBLE EXCLAMATION MARK character
    //  "240, 159, 144, 182 = 4-byte UTF-8 representation of the DOG FACE
    ```

  * UTF-16 Representation

    ```swift
    for codeUnit in dogString.utf16 {
      print("\(codeUnit) ")
    }
    print("\n")
    // 68 111 103 8252 55357 56374
    // 8252 = decimal equivalent of hexadecimal value of 203C which represent Unicode+203C for double Exclamation Mark, this character represented as a single code unit in UTF-16
    //  55357,  56374 = UTF-16 surrogate pair representation of  the DOG FACE
    ```

      * These values are high-surrogate value of U+83D (55357) and low-surrogate value U+DC36 (56374)
  * Unicode Scalar Representation

    ```swift
    for scalar in dogString.unicodeScalars {
      print("\(scalar.value) ")
      println("\(scalar) ") // print the characters
    }
    print("\n")
    // 68 111 103 8252 128054
    // 8252 = decimal of U+203C = double exclamation mark
    // 128054 = decimal of U+1F436 of the dog face character
    ```

## Collection Types

### Overview

  * Arrays and dictionaries in Swift are always clear about the types of values and keys that they can store.
  * You cannot insert a value of the wrong type
  * Swift's array and dictionaries are implemented as generic collections.

### Mutability of Collections

  * If you create a collection and assign it to a variable, it is mutable
  * It is immutable for a constant

### Arrays

  * Overview
    * Swift's Array differ from Objective-C's NSArray or NSMutableArray which can store any kind of object
    * In Swift, the type of values is always made clear, explicitly or through type inference
  * Array Type Shorthand Syntax
    * **Array<SomeType> or [SomeType] (preferred)**
  * Array Literals

    ```swift
    [value 1, value 2, value 3]
    var shoppingList: [String] = ["Eggs", "Milk"]
    ```

  * Accessing and Modifying An Array

    ```swift
    var shoppingList: [String] = ["Eggs", "Milk"]
    shoppingList.count
    shoppingList.isEmpty
    shoppingList.append("Flour")
    shoppingList += ["BakingPowder", "Cheese"] // Add new items to an array

    var firstItem = shoppingList[0] // subscript syntax
    shoppingList[0] = "Six eggs"
    shoppingList[4...6] = ["Bananas", "Apples"] // Shopping list now has 4 items
    shoppingList.insert("Maple Syrup", atIndex: 0)

    let mapleSyrup = shoppingList.removeAtIndex(0)
    let apples = shoppingList.removeLast()
    ```


    * Note
      * Subscript can't be used to append a new item to an array
      * Out of range index, cause runtime error
  * Iterating Over an Array

    ```swift
    for item in shoppingList { println(item) }
    ```

    * Enumerate function

      ```swift
      for (index, value) in enumerate(shoppingList) {
        println("Item \(index + 1): \(value)")
      }
      ```

  * Creating and Initialising an Array

    ```swift
    var someInts = [Int]()
    someInts.append(3)
    someInts = [] // reset to empty Int array
    var xyz = [] // runtime error, cause type unknown
    var threeDoubles = [Double](count: 3, repeatedValue: 2.5) // [2.5, 2.5, 2.5]
    ```


### Dictionaries

  * Overview
    * Swift dictionaries are specific about the types of keys and values
  * Dictionary Type Shorthand Syntax
    * **Dictionary<KeyType, ValueType> or [KeyType: ValueType]** (preferred)
  * Dictionary Literals

    ```swift
    [key 1: value 1, key 2: value 2, key 3: value 3]
    var airports: [String: String] = ["TYO": "Tokyo", "DUB": Dublin"]
    ```

    * If key and values are consistent, you could skip the type definition

      ```swift
      var airports = ["TYO": "Tokyo", "DUB": "Dublin"]
      ```

  * Accessing and Modifying a Dictionary

    ```swift
    airports.count
    airports.isEmpty
    airports["LHR"] = "London"
    airports.updateValue("Dublin International", forKey: "DUB")
    airports["APL"] = nil
    airports.removeValueForKey("DUB")
    ```

  * Iterating Over a Dictionary

    ```swift
    for (airportCode, airportName) in airports { ... }
    for key in airport.keys { ... }
    for value in airport.values { ... }
    ```

    * Swift's Dictionary is an unordered collection
  * Creating and Empty Dictionary

    ```swift
    var namesOfIntegers = [Int: String]() // empty dictionary
    namesOfIntegers[:]                    // reset to empty, once the context is already known
    ```

  * Hash Values for Dictionary Key Types
    * A type must be hash able to be used as dictionary's key type
    * A hash value is an Int value that is the same for all object that compare equal if a == b, a.hashValue == b.hashValue
    * All Swift's basic types are hash able by default
    * Enumeration member values without associated values are hash able by default
    * Note
      * Make custom typ to conform to Hashable protocol
      * To provide hashValue and "==" operator property implementation
      * hashValue not required to be the same across different executions or in different programs

## Control Flow

### For Loops

  * For-In
    * Index is only within the scope of the loop

      ```swift
      for index in 1...5 {
        println("\(index) times 5 is \(index * 5)")
      }
      ```

    * If you don't need the index value

      ```swift
      for _ in 1...power { ... }
      ```

    * You can use for in for array and dictionaries too:

      ```swift
      for name in names { ... }
      for (key, value) in dictionaries { ... }
      ```

    * String character

      ```swift
      for char in "hello" { ... }
      ```

  * For

    ```swift
    for var i = 0; i < 3; ++i { ... }
    ```


### While Loops

  * While

    ```swift
    while [cond] { ... }
    ```

  * Do-While

    ```swift
    do { ... } while [cond]
    ```


### Conditional Statements

  * If

    ```swift
    if [cond]  { ... }
    if [cond] { ... } else { ... }
    if [cond] { ... } else if [cond] { ...  }
    ```

  * Switch

    ```swift
    switch [value] {
      case [value 1]:
      // respond to value 1
      case [value 2], [value 3]:
      // respond to value 2 or 3
      default:
      // otherwise, do something else
    }
    ```

    * default is a must
  * No Implicit Fall through
    * In contrast with switch statements in C and Objective-C, switch statement in Swift do not fall through the bottom of each case
    * Though break is not required in Swift, you can still use a break statement to match and ignore a particular case or to break out from a case before it is completed
    * Body of each case must contain one executable statement
    * To opt-in for fall through behaviour, use the **fallthough** keyword
  * Range matching

    ```swift
    switch count {
      case 1...3:
      // statement here
    }
    ```

  * Tuples
    * You can use tuple to test multiple values in a switch statement

      ```swift
      let somePoint = (1, 1)

      switch somePoint {
        case (0, 0):
          ....
        case (_, 0):
          ...
        case (-2...2, -2...2):
          ...
        default:
          ...
      }
      ```

  * Value Bindings
    * Bind value or values it matches to temporary constants or variables for use in the body of the case, known as value binding

      ```swift
      switch anotherPoint {
        case (let x, 0):
          ...
        case let (x, y):
          ...
        }
      ```

    * Note that on this case the default statement is not required, cause every possible case as been catered for
  * Where
    * To check additional conditions

      ```swift
      case let (x, y) where x == y:
      ```

### Control Transfer Statements

  * Continue
    * Tells a loop to stop what it is doing, and start again at the beginning of the next iteration
  * Break
    * Break In a Loop Statement
    * Break In a Switch Statement
      * Used to match and ignore one or more cases in switch statement
      * Switch does not allow empty case, to deliberately match & ignore a case
  * Fallthrough
    * Switch statements in Swift do not fall through the bottom of each case into the next one
    * To enable fall through the next case use fallthrough keyword

      ```swift
      case abc:
        // fallthrough
      case next:
        // executed again
        // fallthrough
      default:
        // executed again
      ```

    * Fallthrough does not check the next condition
  * Labeled Statements
    * You can nest switch statement inside another loop statement
    * Sometimes it is important to be explicit which statement you want to break/continue
    * You can mark a loop statement or switch statement with a statement label
    * Format:
      * [label name]:  while [condition] { ... }

      ```swift
      gameLoop: while [condition] {
        switch [variable] {
          case [condition]
            break grameLoop
        }
      }
      ```

## Functions

### Defining and Calling Functions

```swift
func sayHello(personName: String) -> String {
  let greeting = "Hello, " + personName + "!"
  return greeting
}

sayHello("Anna")
```

### Function Parameters & Return Values

  * Multiple Input Parameters

    ```swift
    func halfOpenRangeLength(start: Int, end: Int) -> Int {
      return end - start
    }
    println(halfOpenRangeLength(1, 10)) // prints "9"
    ```
      * Functions without Parameters

        ```swift
        func sayHelloWorld() -> String {
          return "hello, world"
        }
        println(sayHelloWorld())
        ```

      * Functions without Return Values

        ```swift
        func sayGoodbye(personName: String) {
          println("Goodbye, \(personName)!")
        }
        sayGoodbye("Dave")
        ```

      * Functions with Multiple Return Values
        ```swift
        func minMax(array: [Int]) -> (min: Int, max: Int) {
          var currentMin = array[0]
          var currentMax = array[0]
          for value in array[1..<array.count] {
            if value < currentMin {
              currentMin = value
            } else if value > currentMax {
              currentMax = value
            }
          }
          return (currentMin, currentMax)
        }

        let bounds = minMax([8, -6, 2, 109, 3, 71])
        bounds.min
        bounds.max
        ```

  * Optional Tuple Return Types
    * -> (Int, Int)?
    * It's different from (Int?, Int?)
    * if let bounds = minMax(...) { ... }

### Function Parameter Names

```swift
fund someFunction(paramName: Int) { ... }
```

    * Param only be used inside the function
  * External Parameter Names
    * Sometimes it is useful to use a different param when you call a function
    * To do that, define an external parameter name for each parameter

      ```swift
      func someFunction(paramExt  paramName: Int) { ... }
      someFunc(paramExt: 2)
      ```

    * Consider using external param names when the purpose of a function's argument are not clear
  * Shorthand External Parameter Names
    * If the local param name the same with external param name, use the hash symbol (#)
    * func someFunction(#paramName: Int)
  * Default Parameter Values
    * Place params with default values at the end of a function's param list.
    * Ensures that all calls to the func use the same order for their non-default args

      ```swift
      func someFunc(paramName: String = " ") { ... }
      ```

  * External Names for Parameters with Default Values
    * Swift provides an automatic external name for any param that has a default value, and it is the same with the paramName just like using the hash symbol

      ```swift
      func someFunc(joiner: String = " ")
      someFunc(joiner: "-")
      ```

    * You can opt out of this behaviour by writing an underscore (_) instead of an explicit external name when you define a parameter
      * Not recommended
  * Variadic Parameters
    * Accepts 0 or more values for a specified type
    * [someType]...

      ```swift
      func average(numbers: Double...) -> Double
      average(1, 2, 3, 4, 5)
      ```

    * At most one variadic param, must be as the last in the parameter list
    * If there are default values as well, place variadic param after all the defaulted parameters
  * Constant & Variable Parameters
    * Function params are constants by default
    * Sometimes it is useful to have a variable copy to work with

      ```swift
      func someFunc(var paramName: String)
      ```

    * Changes made to a variable param do not persist beyond the end of each call, not visible outside the function's body
    * Variable param only exists for the lifetime of that function call
  * In-Out Parameters
    * If you want a function to modify a parameter's value, and want the changes to persist.
    * Use 'inout' keyword at the start of the parameter definition
    * You can only pass a variable not a constant
    * You place an & before a variable's name when you pass it as an argument
    * Can not have default values, and variadic params can not be marked as inout. If you mark it as inout, you can't mark it as var or let

      ```swift
      func someFunc(inout paramName: Int)

      var locName = 3
      someFunc(&locName)
      ```

### Function Types

```swift
// Function Type as a parameter type for another function
func printMathResult(mathFunc: (Int, Int) -> Int, a: Int, b:Int) { ... }
printMathResult(addTwoInts, 3, 5)

// Function Type as Return Types
func someFunc(backwards: Bool) -> (Int) -> Int {
  return backwards ? stepBackward : stepForward
}
```

### Nested Functions

```swift
func chooseStepFunction(backwards: Bool) -> (Int) -> Int {
  func stepForward(input: Int) -> Int { return input + 1 }
  func stepBackward(input: Int) -> Int { return input - 1 }
  return backwards ? stepBackward : stepForward
}
```

## Closures

### Overview

  * Three forms:
    * Global functions are closures that have a name and do not capture any values
    * Nested functions are closures that have name and can capture values from their enclosing function
    * Closure expressions are unnamed closures written in a lightweight syntax that can capture values from their surrounding context
  * Swift closures have clean & clear style with optimisations:
    * Inferring parameter and return types from the context
    * Implicit returns from single-expression closures
    * Shorthand argument names
    * Trailing closure syntax

### Closure Expressions

  * A way to write inline closure in a brief focused syntax
  * The Sorted Function

      ```swift
      let names = ["Chris", "Alex", "Ewa", "Barry", "Daniella"]
      func backwards(s1: String, s2: String) -> Bool { return s1 > s2 }
      var reversed = sorted(names, backwards)
      ```

  * Closure Expression Syntax

    ```swift
    { ([parameters] -> [return type] in
      [statements]
    }
    ```

    * Can use constant, variable and inout parameters.
    * **Default values cannot be provided**
    * Variadic parameters can be used
    * Tuples can also be used as parameter types and return types

      ```swift
      reversed = sorted(names, { (s1: String, s2: String) -> Bool in
        return s1 -> s2
      })
      ```

    * Closure can be written on a single line
  * Inferring Type from Context
    * Because sorting closure is passed as an argument to a function, Swift can infer the types of its parameters and return from the type of the sorted function's second parameter.

      ```swift
      reversed = sorted(names, { s1, s2 in return s1 > s2 })
      ```

    * You never need to write an inline closure in it fullest form when closure is used as a function argument
    * You can still make types explicit to avoid ambiguity for readers
  * Implicit Returns from Single-Expression Closures
    * Single-expression closures can implicitly return the result of their single expression by omitting the return keyword from their declaration:

      ```swift
      reversed = sorted(names, { s1, s2 in s1 > s2 })
      ```

  * Shorthand Argument Names
    * $0, $1, $2
    * You can omit closure's argument list from its definition
    * The in keyword can also be omitted because the closure expression is made up entirely of its body

      ```swift
      reversed = sorted(names, { $0 > $1 })
      ```

  * Operator Functions
    * There's actually an even shorter way to write the closure expression above
    * Swift's String type defines its string specific implementation of the > operator as a function that has two parameters of type String, and returns Bool
    * It matches the function type needed for the sorted function
    * Thus Swift can infer that you want to use its string specific implementation:

      ```swift
      reversed = sorted(names, >)
      ```

### Trailing Closures

  * If closure is long and passed as function's final argument
  * Write outside of (and after) the parentheses of the function call it supports:

    ```swift
    func someFunc(closure: () -> ()) { ... }
    someFunc({  // closure body })
    someFunc() { // trailing's closure body }
    ```

  * If a closure expression is provided as the function's only argument, you provide that expression as a trailing closure, you can omit a pair of parentheses ()

    ```swift
    reversed = sorted(names) { $0 > $1 }
    ```

    * Map example:

      ```swift
        let strings = numbers.map {
          (var number) -> String in

          var output = ""
          while number > 0 {
            output = digitNames[number % 10]! + output
            number /= 10

          }
          return output
        }
      ```

### Capturing Values

  * Closure capture constants and variables from the surrounding context in which it is defined
  * Closure can refer and modify those values even if the original scope no longer exists
  * Simplest form of a closure in Swift is a nested function

    ```swift
    func makeIncrementor(forIncrement amount: Int) -> () -> Int {
      var runningTotal = 0

      func incrementor() -> Int {
        runningTotal += amount
        return runningTotal
      }
      return incrementor
    }

    let incrementByTen = makeIncrementor(forIncrement: 10)
    incrementByTen() // 10
    incrementByTen() // 20
    ```

  * If you assign a closure to a property of a class instance
    * The closure captures that instance by referring to the instance or its members, this will create strong reference cycle
  * Swift uses capture lists to break these strong reference cycles, more info later

### Closures are Reference Types

  * Whenever you assign a function or a closure to a constant or a variable, you are actually setting that constant or variable to be a reference to the function/closure
  * Example above, it is the choice of closure that incrementByTen refers to that is constant, not the contents of the closure itself
  * Meaning if you assign a closure to two different constants/variables, both refer to the same closure

    ```swift
    let alsoIncrementByTen = incrementByTen
    alsoIncrementByTen()
    ```

## Enumerations

### Overview

  * Defines a common type for a group of related values and enables you to work with those values in a type-safe way within your code
  * C enums assign related names to set a of integer values
  * Enums in Swift are more flexible, and do not have to provide a value for each member of the enumeration
  * If a value (raw value) is provided for each enumeration member, the value can be a string, a character, a value, of any integer or floating-point type
  * Adopt many features traditionally supported only by classes, such as:
    * computed properties to provide additional info about enum's current value
    * instance methods
    * define initialisers to provide an initial member value
    * extended to expand their functionality
    * conform to protocols

### Enumeration Syntax

  ```swift
  enum SomeEnumeration {
    // enumeration definition goes here
  }

  enum CompassPoint {
    case North
    case South
    case East
    case West
  }
  ```

  * Unlike C & Obj-C, Swift enumeration members are not assigned with a default integer value when they are created
    * Instead, the different enumeration members are fully fledged values in their own right, with an explicitly defined type of CompassPoint
  * Multiple member values:

    ```swift
    enum Planet {
      case Mercury, Venus, Earth
    }
    ```

  * Each enum defines a brand new type
  * Name should start with a capital letter
  * Singular format

    ```swift
    var directionToHead = CompassPoint.West
    ```

  * Once directionToHead is defined, you can use a shorthand notation

    ```swift
    directionHead = .East
    ```

### Matching Enumeration Values with a Switch Statement

  ```swift
  directionToHead = .South
    switch directionToHead {
      case .North:
        println("Lots of planets have a north")
      case .South:
        println("Watch out for penguins")
      case .East:
        println("Where the sun rises")
      case .West:
        println("Where the skies are blue")
    }
  ```
  * Switch statement must be exhaustive considering an enumeration's members, if .West is omitted, there'll be a compilation error.

### Associated Values

  * Sometimes it is useful to store associated values of other types along with these member values.
  * This enables you to store additional custom info along with the member value, and permit this info to vary each time you use that member in your code.
  * Associated value can be any given type, and the value type can be different for each member of the enumeration
  * Enumerations similar to these are known as **discriminated unions, tagged unions and variants** in other programming language.

    ```swift
    enum Barcode {
      case UPCA(Int, Int, Int, Int)
      case QRCode(String)
    }
    var productBarCode = Barcode.UPCA(8, 85909, 51226, 3)
    productBarCode = .QRCode("ABCDEF")
    ```

    * Switch statement:

      ```swift
      switch productBarcode {
        case .UPCA(let numberSystem, let manufacturer, let product, let check):
          println("UPC-A: \(numberSystem), \(manufacturer), \(product), \(check).")

        case .QRCode(let productCode):
          println("QR code: \(productCode).")
      }

      // prints "QR code: ABCDEFGHIJKLMNOP."
      ```

    * You can place a single var/let before the member name for brevity:

      ```swift
      switch productBarcode {
        case let .UPCA(numberSystem, manufacturer, product, check):
          println("UPC-A: \(numberSystem), \(manufacturer), \(product), \(check).")
        case let .QRCode(productCode):
          println("QR code: \(productCode).")
      }
      // prints "QR code: ABCDEFGHIJKLMNOP.
      ```

### Raw Values

  * Enumeration members can come repopulated with default values (raw values), which are all of the same type

    ```swift
    enum ASCIIControlCharacter: Character {
      case Tab = "\t"
      case LineFeed = "\n"
      case CarriageReturn = "\r"
    }
    ```

  * Raw value has to be unique, raw value for a particular enumeration number is always the same
  * When integers are used for raw values, they auto-increment

    ```swift
    enum Planet: Int {
      case Mercury = 1, Venus, Earth, Mars, Jupiter, Saturn, Uranus, Neptune
    }

    let earthsOrder = Planet.Earth.rawValue // 3
    let possiblePLanet = Planet(rawValue: 2)
    ```

## Classes & Structures

### Overview

  * Swift does not require you to create separate interface implementation files for custom classes and structures

### Comparing Classes and Structures

  * Things in common
    * Define properties to store values
    * Define methods to provide functionality
    * Define subscripts to provide access to their values using subscript syntax
    * Define initializers to setup their initial state
    * Extended to expand their functionality
    * Conform to protocols
  * Classes have additional capabilities that structures do not:
    * Inheritance
    * Type casting
    * Deinitializers
    * Reference counting allows more than one reference to a class instance
      * Structures are always copied when they are passed in your code, they don't use reference counting
  * Definition Syntax
    * Similar between Class & Structure
    * Syntax:

      ```swift
      class SomeClass { ... }
      struct SomeStructure { ... }
      ```

    * When you define a new class or structure, you define a new Swift type.

      ```swift
      struct Resolution {
        var width = 0
        var height = 0
      }

      class VideoMode {
        var resolution = Resolution()
        var interlaced = false
        var frameRate = 0.0
        var name: String?
      }
      ```

  * Class and Structure Instances

    ```swift
    let someResolution = Resolution()
    let someVideoMode = VideoMode()
    ```

  * Accessing Properties

    ```swift
    someResolution.width // 0
    someVideoMode.resolution.width // 0
    someVideoMode.resolution.width = 1280
    ```

    * Note
      * Unlike Obj-C, Swift enables you to set sub properties of a structure property directly.
      * You are able to set resolution.width directly, without the need to set the entire resolution property
  * Memberwise Initializers for Structure Types
    * Use it to initialise member properties of new structure instances
    * Initial values can be passed to the member wise init by name:

      ```swift
      let vga = Resolution(width: 640, height: 480)
      ```

    * Class does not have default member wise initialiser.

### Structures and Enumerations are Value Types

  * A value type, means its value is copied when ascend to a variable or a constant or when it is passed to a function, including all types in Swift, i.e. integers, floating-point numbers, booleans, etc.

### Classes Are Reference Types

  * Reference types are not copied when they are assigned to a variable/constant or when they are passed to a function. Reference to the same instance is used instead.
  * **Identity Operators**
    * Comparing if two objects are the same instance (===)
    * Equal means two instances having the same values (!==)
  * **pointers**
    * A swift constant or variable that refers to an instance is similar to a pointer in C, but is not a direct pointer to an address in memory and does not require you to write an asterisk
    * These references are defined like any other constant/variable in Swift

### Choosing Between Classes and Structures

  * Consider structure if:
    * Primary purpose is to encapsulate a few relatively simple data values
    * Expect that the encapsulated values are copied rather than referenced
    * Any properties stores by the structure a themselves of value types, which would be expected to be copied
    * Does not need to inherit properties or behaviour from another existing type
  * Examples of structures
    * Size of a geometric shape, with width, height properties, both of type Double
    * A way to refer ranges within a series perhaps encapsulating a start and length properties, both of type Int
    * A point in a 3D coordinate system, perhaps encapsulating, x, y, z properties, of type Double

### Assignment and Copy Behavior for Strings, Arrays, and Dictionaries

  * String, Array, Dictionary types are implemented as structures
  * Different from NSString, NSArray, and NSDictionary which are implemented as classes, which are passed by reference.
  * Swift only performs actual copy behind the scenes when absolutely necessary, it manages all value copying to ensure optimal performance

## Properties

### Overview

  * Associate values with a particular class, structure or enumeration
  * Stored properties store constant and variable values as part of an instance
    * Provided only by classes and structures
  * Computed properties are provided by classes, structures and enumerations.
  * Stored and computed properties are associated with instances, but properties can be associated to the type itself, known as type properties
  * You can define property observer, for properties you define or properties that a subclass inherits from its superclass.

### Stored Properties

  * Is a constant or variable that is stored as part of an instance of a particular class or structure

    ```swift
    struct FixedLengthRange {
      var firstValue: Int
      let length: Int
    }

    var rangeOfThreeItems = FixedLengthRange(firstValue: 0, length: 3)  // the range represents integer values 0, 1, and 2
    rangeOfThreeItems.firstValue = 6 // the range now represents integer values 6, 7, and 8
    ```

  * Stored Properties of Constant Structure Instances
    * When an instance of a value type is marked as a constant, so are all of its properties, but not true for classes.

      ```swift
      let someStruct = SomeStruct(x: 0, y: 0)
      someStruct.x = 12 // compile-error
      ```

  * Lazy Stored Properties
    * Property whose initial value is not calculated until the first time it is used
    * Use 'lazy' modifier before its declaration
    * Must always declare lazy as a var
    * Useful for a property that is dependent on outside factors, whose values are not known after an initialisation completes, e.g. computationally expensive

      ```swift
      class DataImporter {
        var fileName = "data.txt"
        // the DataImporter class would provide data importing functionality here
      }

      class DataManager {
        lazy var importer = DataImporter()
        var data = [String]()
        // the DataManager class would provide data management functionality here
      }

      let manager = DataManager()
      manager.data.append("Some data")
      manager.data.append("Some more data")
      // the DataImporter instance for the importer property has not yet been created
      ```

    * DataImporter instance for the importer property is only created when the importer property is first accessed, e.g.
      * manager.importer.fileName
  * Stored Properties and Instance Variables
    * Obj-C provides two ways to store values and references as apart of a class instance
      * In additional to properties, you can use instance variables as a backing store for values store in a property
    * Swift unifies these concepts into a single property declaration
      * It does not have a corresponding instance variable, and the backing store for a property is not accessed directly
      * To simplify and avoid confusion

### Computed Properties

  * Do not store a value, provides a getter and optional setting to retrieve and set other properties/values directly

    ```swift
    struct Point {
        var x = 0.0, y = 0.0
    }
    struct Size {
        var width = 0.0, height = 0.0
    }
    struct Rect {
        var origin = Point()
        var size = Size()
        var center: Point {
            get {
                let centerX = origin.x + (size.width / 2)
                let centerY = origin.y + (size.height / 2)
                return Point(x: centerX, y: centerY)
            }
            set(newCenter) {
                origin.x = newCenter.x - (size.width / 2)
                origin.y = newCenter.y - (size.height / 2)
            }
        }
    }

    var square = Rect(origin: Point(x: 0.0, y: 0.0),
        size: Size(width: 10.0, height: 10.0))

    let initialSquareCenter = square.center
    square.center = Point(x: 15.0, y: 15.0)
    ```

  * Shorthand Setting Declaration
    * If computed property's setting does not define a name for the new value to be set, "newValue" is used:

      ```swift
      set {
        origin.x = newValue.x - (size.width / 2)
        origin.y = newValue.y - (size.height / 2)
      }
      ```

  * Read-Only Computed Properties
    * Has getter but no setter
    * You must declare computed properties, including read only properties as variable properties with 'var' keyword, because their value is not fixed.
    * _You can simplify read-only computed property by removing the get keyword and its braces_:

    ```swift
    struct Cuboid {
      var width = 0.0, height = 0.0, depth = 0.0
      var volume: Double {
        return width * height * depth
      }
    }

    let fourByFiveByTwo = Cuboid(width: 4.0, height: 5.0, depth: 2.0)
    ```

### Property Observers

  * You can add property observers to any stored properties you define, apart from the lazy stored properties
  * Any inherited property by overriding the property within a subclass
  * Note
    * You don't need to define property observers for non-overridden computed properties, because you can observe and respond to changes to their value directly from within the computed property's setter.
  * You have the option to define either or both of these observers on a property
    * willSet - called before the value is stored
      * default param "newValue", you can override
    * didSet - called immediately after the new value is stored
      * default old property param name is "oldValue"
  * Note
    * willSet and didSet are not called when a property is first initialised, only called when its value is set outside the initialisation context
    * If you assign a value to a property within its own didSet observer, the new value will replace the one that you just set

      ```swift
      class StepCounter {
        var totalSteps: Int = 0 {
          willSet(newTotalSteps) { }
          didSet { if totalSteps > oldValue { ... } }
        }
      }
      ```

### Global and Local Variables

  * Capabilities above to observe properties are for both global and local properties
  * Global variables are defined outside any function, method, closure or type context
  * Global constants and variables are always computed lazily, similar to Lazy Stored Properties

### Type Properties

  * For value types (structures and enumerations), you can define stored and computed type properties,
  * For classes, you can define computed type properties only
  * Stored type properties for value types can be variables or constants.
    * Computed type properties are always declared as variable properties in the same way as computed instance properties
  * Type Property Syntax
    * In C and Obj-C, you define static constants and variables associated with a type as global static variables
    * In Swift type properties are written as part of type's definition, with "**static**" keyword for value types, and and "**class**" for class types.

      ```swift
      struct SomeStructure {

        static var storedTypeProperty = "Some value."
        static var computedTypeProperty: Int {
            // return an Int value here
        }
      }

      enum SomeEnumeration {
        static var storedTypeProperty = "Some value."
        static var computedTypeProperty: Int {
            // return an Int value here
        }
      }

      class SomeClass {
        class var computedTypeProperty: Int {
            // return an Int value here
        }
      }
      ```

    * The computed type property are for read-only, but you can define read-write computed type properties with the same syntax for computed instance properties
  * Querying and Setting Type Properties

    ```swift
    println(SomeClass.computedTypeProperty)    // prints "42"
    println(SomeStructure.storedTypeProperty)  // prints "Some value."
    SomeStructure.storedTypeProperty = "Another value.
    ```

    * Setting type property

## Methods

### Overview

  * Functions associated with a particular type
  * Classes, structures and enumerations can define instance and type methods.
  * Major difference from C and Obj-C. In Obj-C, only classes can define methods.

### Instance Methods

```swift
class Counter {
    var count = 0
    func increment() {
        count++
    }
    func incrementBy(amount: Int) {
        count += amount
    }
    func reset() {
        count = 0
    }
}
```
  * Local and External Parameter Names for Methods
    * Function params can have both local and external name, same wit method parameters
      * Methods are just functions associated with a type
      * But the default behaviour is different for functions and methods
    * Methods in Swift similar to Obj-C, name of a method refers to the method's first parameter using a preposition such as "width", "for", "by", e.g. incrementBy(amount:, numberOfTimes). Easy to read as a sentence
    * Swift makes this naming convention easy to write by using a different default approach for method parameters than it uses for functions
      * It gives the **first parameter** name in a method a **local parameter name** by default
      * And gives the **second and subsequent parameter names** both **local and external parameter** names by default

        ```swift
          class Counter {
            var count: Int = 0
            func incrementBy(amount: Int, numberOfTimes: Int) {
              count += amount * numberOfTimes
            }
          }
        ```

      * You can call the method as follows:

        ```swift
        let counter = Counter()
        counter.incrementBy(5, numberOftimes: 3)
        ```

      * Default behaviour as if

        ```swift
        func incrementBy(amount: Int, #numberOfTimes: Int) {
          count += amount * numberOfTimes
        }
        ```
  * Modifying External Parameter Name Behaviour for Methods
    * Use # or add external parameter name for the first param
    * To disable second param onwards, add _
  * The self Property
    * self refers to current instance
    * You don't usually need to declare
    * Unless when a parameter name has the same name as the property of that instance
  * Modifying Value Types from Within Instance Methods
    * Structures and enumeration are value types, which properties of a value type cannot be modified from within its instance methods.
    * You can opt-in to mutating behaviour for that method, the method can also assign a completely new instance to its implicit self property
    * Use "mutating" keyword before the "func" for the method:

      ```swift
      struct Point {
        var x = 0.0, y = 0.0
        mutating func moveByX(deltaX: Double, y deltaY: Double) {
          x += deltaX
          y += deltaY
        }
      }

      var somePoint = Point(x: 1.0, y: 1.0)
      somePoint.moveByX(2.0, y: 3.0)
      ```

    * Note that you cannot call a mutating method on a constant structure

      ```swift
      let fixedPoint = Point(x: 3.0, y: 3.0)
      fixedPoint.moveByX(2.0, y: 3.0) // this will report an error
      ```

  * Assigning to self Within a Mutating Method

      ```swift
      struct Point {
        var x = 0.0, y = 0.0
        mutating func moveByX(deltaX: Double, y deltaY: Double) {
          self = Point(x: x + deltaX, y: y + deltaY)
        }
      }
      ```

    * Mutating methods for enumerations can set the self to a different member of the same enumeration

      ```swift
      enum TriStateSwitch {

        case Off, Low, High
        mutating func next() {
            switch self {
            case Off:
                self = Low
            case Low:
                self = High
            case High:
                self = Off
            }
        }
      }
      var ovenLight = TriStateSwitch.Low
      ovenLight.next()
      // ovenLight is now equal to .High
      ovenLight.next()
      // ovenLight is now equal to .Off"
      ```

### Type Methods

  * You indicate type methods for classes by writing the keyword "class" before the method's fund keyword, and type methods for structures and enumerations by writing the keyword "static" before the method's fund keyword
  * In Obj-C type methods only for classes, in Swift for all classes, structures, and enumerations.

    ```swift
    class SomeClass {
      class func someTypeMethod() {
        // type method implementation goes here
      }
    }

    SomeClass.someTypeMethod()
    ```

  * self refers to type itself
  * Accessing type methods from the same scope, doesn't require a self:

    ```swift
    struct LevelTracker {
        static var highestUnlockedLevel = 1

        static func unlockLevel(level: Int) {
            if level > highestUnlockedLevel { highestUnlockedLevel = level }
        }

        static func levelIsUnlocked(level: Int) -> Bool {
            return level <= highestUnlockedLevel
        }

        var currentLevel = 1
        mutating func advanceToLevel(level: Int) -> Bool {
            if LevelTracker.levelIsUnlocked(level) {
                currentLevel = level
                return true
            } else {
                return false
            }
        }
    }
    ```

## Subscripts

### Overview

  * Classes, structures, enumerations can define subscripts
  * Shortcuts for accessing the member elements of a collection, list or sequence
  * Use subscripts to set/get values by index without the need for separate methods
    * E.g. someArray[index], someDictionary[key]
  * You can define multiple subscripts for a single type
    * Appropriate subscript overload is based on the type of index value passed to the subscript
    * Not limited to a single dimensions
    * You can define multiple input params to suit your custom type's needs

### Subscript Syntax

  * Similar to instance methods, but can be read-write or read-only

    ```swift
    subscript(index: Int) -> Int {
        get {
            // return an appropriate subscript value here
        }
        set(newValue) {
            // perform a suitable setting action here
        }
    }
    ```

    * As with read-only computed properties, you can drop the get keyword:

      ```swift
      subscript(index: Int) -> Int {
          // return an appropriate subscript value here
      }

      struct TimesTable {
          let multiplier: Int
          subscript(index: Int) -> Int {
              return multiplier * index
          }
      }

      let threeTimesTable = TimesTable(multiplier: 3)
      println("six times three is \(threeTimesTable[6])") // prints "six times three is 18
      ```

### Subscript Usage

  * Exact meaning of "subscript" depends on the context which it is used

    ```swift
    var numberOfLegs = ["spider": 8, "ant": 6, "cat": 4]
    numberOfLegs["bird"] = 2
    ```

    * Dictionary type implements its key-value subscripting, takes and receives an optional type

      ```swift
      numberofLegs["bird"] returns a value of type Int?
      ```

### Subscript Options

  * Can take any number of input parameters, and can be of any type
    * Subscripts can also return any type
    * Can you variable parameters, and variadic parameters
    * No in-out params or default parameter values
  * There could be more than one subscript implementations, which subscript to used will be inferred based on the type s of the value or values that are contained in subscript braces, i.e. subscript overloading
  * Support multiple parameters

    ```swift
    struct Matrix {
        let rows: Int, columns: Int
        var grid: [Double]
        init(rows: Int, columns: Int) {
            self.rows = rows
            self.columns = columns
            grid = Array(count: rows * columns, repeatedValue: 0.0)
        }
        func indexIsValidForRow(row: Int, column: Int) -> Bool {
            return row >= 0 && row < rows && column >= 0 && column < columns
        }
        subscript(row: Int, column: Int) -> Double {
            get {
                assert(indexIsValidForRow(row, column: column), "Index out of range")
                return grid[(row * columns) + column]
            }
            set {
                assert(indexIsValidForRow(row, column: column), "Index out of range")
                grid[(row * columns) + column] = newValue
            }
        }
    }
    ```

## Inheritance

### Overview

  * Classes can also add property observers to inherited properties
  * Property observers can be added to any property, stored or computed

### Defining a base class

  * Any class that does not inherit from another class is known s base class
  * Swift classes do not inherit from a universal base class
  * Classes you define without a superclass, are base classes.

    ```swift
    class Vehicle {
        var currentSpeed = 0.0
        var description: String {
            return "traveling at \(currentSpeed) miles per hour"
        }
        func makeNoise() {
            // do nothing - an arbitrary vehicle doesn't necessarily make a noise
        }
    }

    let someVehicle = Vehicle()
    someVehicle.description
    ```

### Subclassing

  * Extending a new class based on an existing class

    ```swift
    class SomeSubclass: SomeSuperClass { ...}
    ```

### Overriding

  * Use override keyword to clearly show the intent or error
    * Compiler will also check if you are overriding any of the superclass methods
  * Accessing superclass Methods, Properties, and Subscripts
    * super.someMethod, super.someProperty, super[someIndex]
  * Overriding methods

    ```swift
    class Train: Vehicle {
        override func makeNoise() {
            println("Choo Choo")
        }
    }
    ```

  * Overring properties
    * To provide your own implementation or to add property observer
  * Overriding property Getters and Setters
    * You can present an inherited read-only property as read-write property
    * You can not present an inherited read-write property as a read only
    * Note
      * If you provide a setter, you need to provide the getter as well
      * If you don't want to modify the inherited property's value within the overriding getter, just return the super class value, i.e. super.someProperty

      ```swift
      class Car: Vehicle {
        var gear = 1
        override var description: String {
          return super.description + " in gear \(gear)"
        }
      }
      ```

  * Overriding property Observers
    * Override the property to add the observers
    * Note
      * You can not add property observers to inherited constant stored properties or inherited read-only computed properties, because these properties cannot be set
      * You can't override both setter and property observer for the same property
      * If you already provide custom setter, observe any value changes from within the custom setter instead
    * Example:

      ```swift
      class AutomaticCar: Car {
        override var currentSpeed: Double {
          didSet {
            gear = Int(currentSpeed / 10.0) + 1
          }
        }
      }
      ```

### Preventing Overrides

  * Mark it as "final", e.g. final var, final fund, final class fund, final subscript

## Initialization

### Overview

  * Unlike Obj-C inits, Swift inits do not return value
  * Instance of class types can also implement a deinitializer

### Setting Initial Values for Stored Properties

  * Classes and structures must set all their stored properties to an init value by the time an instance is created
  * You can store initial value of a stored property in an initialiser, or by assigning default value
  * Note
    * When you assign the default value to a stored property, or sets the initial value within the initializers, the property is set directly without calling property observers.
  * Initializers

    ```swift
    init() {
      // perform some initialization here
    }

    struct Fahrenheit {
      var temperature: Double

      init() {
        temperature = 32.0
      }
    }
    ```

### Customizing Initialization

  * Initialization Parameters

    ```swift
    struct Celsius {
        var temperatureInCelsius: Double
        init(fromFahrenheit fahrenheit: Double) {
            temperatureInCelsius = (fahrenheit - 32.0) / 1.8
        }
        init(fromKelvin kelvin: Double) {
            temperatureInCelsius = kelvin - 273.15
        }
    }
    let boilingPointOfWater = Celsius(fromFahrenheit: 212.0)
    // boilingPointOfWater.temperatureInCelsius is 100.0
    let freezingPointOfWater = Celsius(fromKelvin: 273.15)
    // freezingPointOfWater.temperatureInCelsius is 0.0"
    ```

  * Local & External Parameter Names
    * Initializers do not have an identifying function name, thus the names and types of an init parameters play an important role identifying which init to call.
    * Swift provide an automatic external name to be the same with the local name

      ```swift
      struct Color {

        let red, green, blue: Double
        init(red: Double, green: Double, blue: Double) {
          self.red   = red
          self.green = green
          self.blue  = blue
        }

        init(white: Double) {
          red   = white
          green = white
          blue  = white
        }
      }

      let magenta = Color(red: 1.0, green: 0.0, blue: 1.0)
      let halfGray = Color(white: 0.5)  // without external name will trigger an error
      ```

  * Initializer Parameters Without External Names

      ```swift
      // Use "_" as the external name
      init(_ celsius: Double) {
        temperatureInCelsius = celsius
      }
      Celcius(37.0)
      ```

  * Optional Property Types
    * Optional property types are automatically initialised with a value of nil

      ```swift
      class SurveyQuestion {

          var text: String
          var response: String?
          init(text: String) {
              self.text = text
          }
          func ask() {
              println(text)
          }
      }

      let cheeseQuestion = SurveyQuestion(text: "Do you like cheese?")
      cheeseQuestion.ask()
      cheeseQuestion.response = "Yes, I do like cheese."
      ```

  * **Modifying Constant Properties during Initialization**
    * You can modify the value of a constant property during initialisation
    * Can only be modified in class init, not sub-class init.

### Default Initializers

  * If no init is provided, Swift provide default init, optional parameters will be set to nil, example:

    ```swift
    class ShoppingListItem {
      var name: String?
      var quantity = 1
      var purchased = false
    }

    var item = ShoppingListItem()
    ```

  * Memberwise Initialisers for Structure Types
    * Structure types automatically receive a member wise initialiser if there is no custom initialisers
    * Memberwise initializer is a shorthand way to initialise the member properties of new structure instances
    * Initial values can be passed to the init by name

      ```swift
      struct Size {
         var width = 0.0, height = 0.0
      }

      let twoByTwo = Size(width: 2.0, height: 2.0)
      ```

### Initializer Delegation for Value Types

  * The rules are different for value types and class types.
    * Value types (structures and enumerations) do not support inheritance, so their initialiser delegation process is relatively simple, they can only delegate to another initialiser, class has superclass.
  * self.init can only be called within an initialiser
  * If custom initialiser is defined, you won't have access to the default initialiser

    ```swift
    struct Size {
        var width = 0.0, height = 0.0
    }
    struct Point {
        var x = 0.0, y = 0.0
    }
    struct Rect {
        var origin = Point()
        var size = Size()
        init() {}
        init(origin: Point, size: Size) {
            self.origin = origin
            self.size = size
        }
        init(center: Point, size: Size) {
            let originX = center.x - (size.width / 2)
            let originY = center.y - (size.height / 2)
            self.init(origin: Point(x: originX, y: originY), size: size)
        }
    }

    let basicRect = Rect()              // basicRect's origin is (0.0, 0.0) and its size is (0.0, 0.0)
    let originRect = Rect(origin: Point(x: 2.0, y: 2.0),
size: Size(width: 5.0, height: 5.0))   // originRect's origin is (2.0, 2.0) and its size is (5.0, 5.0)
    ```

  * Note
    * For an alternative way to write this example without defining the init() and init(origin:size:) initializers yourself, see Extensions.

### Class Inheritance and Initialization

  * All of class's stored properties must be assigned to an initial value during initialisation
  * Designated Initializers & Convenience Initializers
    * Designated inits are primary inits for a class
      * Init all properties in that class and calls its superclass chain inits
      * Quite common to have only one
    * Convenience inits, secondary support inits
  * Syntax for Designated and Convenienc initialisers
    * init ([parameters]) { ... }
    * convenience init([parameters]) { ... }
  * Init Chaining
    * Rules to simply relationship between designated & convenience inits
      1. Designated init must call a designated init from its immediate class
      2. Convenience init must call another init from the same class
      3. Convenience init must ultimately call a designated init
    * Simple way to remember:
      * Designated init delegates up
      * Convenience init delegates across
    * ![](iOS%3A%20Swift%20Programming%20(iBook).resources/A662D106-1ACE-41E3-A32B-BA295C62B660.png)
    * More complex example, designated inits act as a funnel:
    * ![](iOS%3A%20Swift%20Programming%20(iBook).resources/8E788FC3-DCC0-437D-93F0-8D16CB1D2AC5.png)
  * Two-Phase Initialization
    * Two phases:
      * Phase 1
        * Each stored property is assigned an initial value
      * Phase 2
        * Each class is given the opportunity to customise its stored properties further before new instance is ready to use
    * Two-phase init prevents property values being accessed before they are initialised, and prevent property values being set to a different value by another initialiser unexpectedly
      * Similar to Obj-C, the main difference during Phase 1, Objc-C assigns zero or null values (0 or nil) to every property.
      * Swift's init is more flexible, lets you set custom initial values, and can cope with types for which 0 or nil is not a valid default value
    * Compiler performs four helpful safety checks:
      * Safety Check 1
        * A designated init must sensor that all the properties introduced by its class are initialised before it delegates up to a superclass init
      * Safety Check 2
        * A designated init must delegate up to a superclass init before assigning a value to an inherited property
        * If it does't the new value the designated init assigns will be overwritten by the superclass
      * Safety Check 3
        * A convenience init must delegate to another init  before assigning a value to any property.
        * If it doesn't the new value the convenience init assigns will be overwritten by its own class designated init
      * Safety Check 4
        * An init cannot call any instances methods, read the values of any instance properties, or refer to self as a value until the first phase of init is complete
  * Phase 1
    * A designated or convenience init is called
    * Memory for a new instance of that class is allocated, the memory is not initialised yet
    * A designated init for that class confirms that all stored properties introduced by that class have a value, the memory for those stored properties is now initialised
    * The designated initialiser hands off to a superclass init to perform the same task for its own stored properties
    * This continues up the class inheritance chain until top chain is reached
    * The final class in the chain has ensured that all its stored properties have a value, instance's memory is considered fully initialised, phase 1 is complete
    * ![](iOS%3A%20Swift%20Programming%20(iBook).resources/35412844-C46F-4742-B664-2BBA53595A36.png)
  * Phase 2
    * Working back down from the top of the chain, each designated initialiser in the chain has the option customise the instance further.
      * Inits are now able to access self and can modify its properties, call its instance methods and so on
    * Finally any convenience inits in the chain have the option to customise the instance to work with self.
    * ![](iOS%3A%20Swift%20Programming%20(iBook).resources/2AFC7723-9E2A-4E1C-9A2D-748DC9696C45.png)
  * Init Inheritance and Overriding
    * **Unlike subclass in Obj-C, Swift subclass do not inherit their superclass init by default**
    * Note
      * Superclass inits are inherited in certain circumstances, only when it is safe and appropriate, more info in the next section
    * If you want to the same init from the superclass, override the init with "override modifier.
    * If you write subclass init that matches superclass convenience init, superclass convenience init can never be called directly by your subclass, as described in Init Chaining
      * **Therefore your subclass is not providing an override of the superclass init**
      * Thus you do not write the override modifier when providing a matching implementation of a superclass convenience initialiser

      ```swift
      class Vehicle {

        var numberOfWheels = 0
        var description: String {
            return "\(numberOfWheels) wheel(s)"
        }
      }

      class Bicycle: Vehicle {
        override init() {
            super.init()
            numberOfWheels = 2
        }
      }
      ```

    * Note
      * Subclasses are only allowed to modify variable superclass properties during initialisation. Subclasses cannot modify inherited constant properties.
  * Automatic Init Inheritance
    * Subclass do not inherit their superclass inits by default, unless certain conditions are met
    * In practice, you do not need to write init overrides in many common scenarios, and can inherit superclass inits with minimal efforts
    * Assuming you provide default values for any new properties you introduce in a subclass, the following two rules apply:
      * Rule 1
        * If your subclass **does not define any designated inits**, it automatically **inherits all its superclass initializers**
      * Rule 2
        * If your subclass provides an implementation of **all its superclass designated initialisers** - either by inheriting them as per rule 1 or by custom implementation, it automatically inherits all of the superclass convenience inits
    * Note
      * A subclass can implement a superclass designated init as subclass convenience init as part of satisfying rule 2
  * Designated and Convenience Inits in Action

    ```swift
    class Food {
        var name: String
        init(name: String) {
            self.name = name
        }
        convenience init() {
            self.init(name: "[Unnamed]")
        }
    }
    ```

    * ![](iOS%3A%20Swift%20Programming%20(iBook).resources/EAC71E1D-8420-452D-95EA-7E9073F9983A.png)

    ```swift
    class RecipeIngredient: Food {
        var quantity: Int
        init(name: String, quantity: Int) {
            self.quantity = quantity
            super.init(name: name)
        }
        override convenience init(name: String) {
            self.init(name: name, quantity: 1)
        }
    }

    let oneMysteryItem = RecipeIngredient()
    let oneBacon = RecipeIngredient(name: "Bacon")
    let sixEggs = RecipeIngredient(name: "Eggs", quantity: 6)
    ```

    * ![](iOS%3A%20Swift%20Programming%20(iBook).resources/DB577B70-0B89-42A4-AD52-8C0D314A2040.png)


    ```swift
    class ShoppingListItem: RecipeIngredient {
        var purchased = false
        var description: String {
            var output = "\(quantity) x \(name)"
            output += purchased ? " ✔" : " ✘"
            return output
        }
    }
    var breakfastList = [

        ShoppingListItem(),

        ShoppingListItem(name: "Bacon"),

        ShoppingListItem(name: "Eggs", quantity: 6),

    ]
    ```

    * ![](iOS%3A%20Swift%20Programming%20(iBook).resources/83B2D621-68B2-4016-88F3-2EAB2DC2E3B0.png)
  * Required Inits
    * To indicate every subclass  must implement that initialiser:

      ```swift
      class SomeClass {
        required init() {
          // initializer implementation goes here
        }
      }
      ```

    * You do not write the override modifier when overriding:


      ```swift
      class SomeSubclass: SomeClass {
        required init() {
          // subclass implementation of the required initializer goes here
        }
      }
      ```

    * You do not have to provide an explicit implementation if the init can be inherited.

### Setting a Default Property Value with a Closure or Function


```swift
class SomeClass {
    let someProperty: SomeType = {
        // create a default value for someProperty inside this closure
        // someValue must be of the same type as SomeType
        return someValue
        }()
}
```

  * Note
    * If you use closure to init a property, remember the rest of the instance has not been initialised yet
    * You cannot access any other properties, and you cannot use "self"

      ```swift
      struct Checkerboard {
          let boardColors: [Bool] = {
              var temporaryBoard = [Bool]()
              var isBlack = false
              for i in 1...10 {
                  for j in 1...10 {
                      temporaryBoard.append(isBlack)
                      isBlack = !isBlack
                  }
                  isBlack = !isBlack
              }
              return temporaryBoard
              }()
          func squareIsBlackAtRow(row: Int, column: Int) -> Bool {
              return boardColors[(row * 10) + column]
          }
      }
      ```


## Deinitialization

### Overview

  * Called immediately before a class instance is deallocated
  * deinit keyword, only for class types

### How Deinitialization works

  * Swift uses ARC to manage memory for the instance, typically you won't need to perform manual cleanup
  * When you are working with your own resources, you probably would, ex.g. create a custom class to open a file/write some data to it, you need to close the file before the class instance is deallocated
  * You are not allowed to call a reinit yourself
  * Superclass deinits are inherited by their subclasses, and called automatically at the end of a subclass deinit. Always called even if subclass does not implement a reinit.

### Deinitializers in Action

```swift
struct Bank {
    static var coinsInBank = 10_000

    static func vendCoins(var numberOfCoinsToVend: Int) -> Int {
        numberOfCoinsToVend = min(numberOfCoinsToVend, coinsInBank)
        coinsInBank -= numberOfCoinsToVend
        return numberOfCoinsToVend

    }

    static func receiveCoins(coins: Int) {
        coinsInBank += coins
    }

}

class Player {
    var coinsInPurse: Int

    init(coins: Int) {
        coinsInPurse = Bank.vendCoins(coins)
    }

    func winCoins(coins: Int) {
        coinsInPurse += Bank.vendCoins(coins)
    }

    deinit {
        Bank.receiveCoins(coinsInPurse)
    }
}

var playerOne: Player? = Player(coins: 100)

println("A new player has joined the game with \(playerOne!.coinsInPurse) coins")
// prints "A new player has joined the game with 100 coins"

println("There are now \(Bank.coinsInBank) coins left in the bank")
// prints "There are now 9900 coins left in the bank

playerOne!.winCoins(2_000)

println("PlayerOne won 2000 coins & now has \(playerOne!.coinsInPurse) coins")
// prints "PlayerOne won 2000 coins & now has 2100 coins"

println("The bank now only has \(Bank.coinsInBank) coins left")
// prints "The bank now only has 7900 coins left

playerOne = nil

println("PlayerOne has left the game")
// prints "PlayerOne has left the game"

println("The bank now has \(Bank.coinsInBank) coins")
// prints "The bank now has 10000 coins
```


## Automatic Reference Counting

### Overview

  * To track and manage your app's memory usage
  * Memory management just works, in a few cases ARC requires more info about the relationship between parts of your code.
  * Reference counting only applies to classes, Structures and Enumerations are value types

### How ARC Works

  * To make sure that instances don't disappear when they are still needed, when you assign a class instance to a property, constant or variable, it makes a strong reference. It does not allow it to be deallocated, as long as strong reference remains.

### ARC In Action

```swift
class Person {
    let name: String
    init(name: String) {
        [self.name][2] = name
        println("\(name) is being initialized")
    }
    deinit {
        println("\(name) is being deinitialized")
    }
}
var reference1: Person?
var reference2: Person?
var reference3: Person?

reference1 = Person(name: "John Appleseed")
// prints "John Appleseed is being initialised"

reference2 = reference1
reference3 = reference1
reference1 = nil
reference2 = nil
reference3 = nil
// prints "John Appleseed is being deinitialized
```

### Strong Reference Cycles Between Class Instances

  * Two class instances holding a strong reference to each other
  * You resolve strong reference cycles by defining some of the relationships between classes as weak or unowned references instead of as strong references.


    ```swift
    class Person {
        let name: String
        init(name: String) { [self.name][2] = name }
        var apartment: Apartment?
        deinit { println("\(name) is being deinitialized") }
    }

    class Apartment {
        let number: Int
        init(number: Int) { self.number = number }
        var tenant: Person?
        deinit { println("Apartment #\(number) is being deinitialized") }
    }
    var john: Person?
    var number73: Apartment?
    john = Person(name: "John Appleseed")
    number73 = Apartment(number: 73)
    ```


  * ![](iOS%3A%20Swift%20Programming%20(iBook).resources/598B95C0-D50B-4ECD-9CD5-126685263ACA.png)


    ```swift
      john!.apartment = number73
      number73!.tenant = john
    ```

  * ![](iOS%3A%20Swift%20Programming%20(iBook).resources/3DCF8042-9FC0-4B33-A406-E4DFEE2D7291.png)

    ```swift
      john = nil
      number73 = nil
      // reference count does not frop to 0

    ```

  * ![](iOS%3A%20Swift%20Programming%20(iBook).resources/EC4DBFFE-F082-4689-B812-9872A63A5417.png)

### Resolving Strong Reference Cycles Between Class Instances

  * Two ways:
    * weak references
      * Use weak reference whenever it is valid for the reference to become nil at some point during its lifetime
    * unowned references
      * When you know that the reference will never be nil once it has been set during initialization
  * Weak References
    * Enable one instance in the reference cycle to refer to the other instance without keeping a strong hold on it
    * Use keyword "weak"
    * Optional, constant not allowed
    * ARC will set to nil when it is deallocated

      ```swift
      class Person {
          let name: String
          init(name: String) { [self.name][2] = name }
          var apartment: Apartment?
          deinit { println("\(name) is being deinitialized") }
      }

      class Apartment {
          let number: Int
          init(number: Int) { self.number = number }
          weak var tenant: Person?
          deinit { println("Apartment #\(number) is being deinitialized") }
      }
      ```

      * ![](iOS%3A%20Swift%20Programming%20(iBook).resources/EC725EFA-13D4-411A-8236-D9A53047D7EE.png)
  * Unowned References
    * Like weak reference, but it is assumed to always have a value
    * Non-optional type
    * Use "unowned" keyword
    * ARC cannot set the reference to nil when it is deallocated
    * Note
      * If you try to access an unowned reference after the instance that it references is deallocated, will trigger a runtime error
      * Use unowned references only when you are sure that the reference refers to an instance

        ```swift
        class Customer {

          let name: String
          var card: CreditCard?
          init(name: String) {
              [self.name][2] = name
          }
          deinit { println("\(name) is being deinitialized") }
        }

        class CreditCard {
          let number: UInt64
          unowned let customer: Customer
          init(number: UInt64, customer: Customer) {
              self.number = number
              self.customer = customer
          }
          deinit { println("Card #\(number) is being deinitialized") }
        }
        ```

    * Note
      * The number property of the CreditCard class is defined with a type of UInt64 rather than Int, to ensure that the number property's capacity is large enough to store a 16-digit card number on both 32-bit and 64-bit systems.

        ```swift
        var john: Customer?
        john = Customer(name: "John Appleseed")
        john!.card = CreditCard(number: 1234_5678_9012_3456, customer: john!)
        ```
      * ![](iOS%3A%20Swift%20Programming%20(iBook).resources/6E29FF73-6FD5-44AC-BFF2-A44366DAD7A0.png)

        ```swift
        john = nil
        // prints "John Appleseed is being deinitialized"
        // prints "Card #1234567890123456 is being reinitialised"
        ```

      * ![](iOS%3A%20Swift%20Programming%20(iBook).resources/64747DE2-441C-43EF-99E2-12B37CEA1E8D.png)
  * **Unowned References and Implicitly Unwrapped Optional Properties**
    * Third scenario which both properties should have a value
    * Combine unowned property on one class with an implicit unwrapped optional property on the other class
    * Enables both properties to be accessed directly without optional unwrapping once init is complete, while avoiding reference cycle

      ```swift
      class Country {

        let name: String
        let capitalCity: City!
        init(name: String, capitalName: String) {
            [self.name][2] = name
            self.capitalCity = City(name: capitalName, country: self)
        }
      }

      class City {
        let name: String
        unowned let country: Country
        init(name: String, country: Country) {
            [self.name][2] = name
            self.country = country
        }
      }

      var country = Country(name: "Canada", capitalName: "Ottawa")
      println("\(country.name)'s capital city is called \(country.[capitalCity.name][3])")
      // prints "Canada's capital city is called Ottawa"
      ```

### Strong Reference Cycles for Closures

  * Can occur if you assign a closure to a property of a class instance, and the body of that closure captures that instance, such as
    * self.someProperty or
    * self.someMethod()
    * Captures self creating a strong reference cycle
  * Closure are reference types, when you assign to a property, you are assigning a reference to that closure
    * Class instance and a closure keeping each other alive
  * Solution to use a "closure capture list"

    ```swift
    class HTMLElement {
        let name: String
        let text: String?

        lazy var asHTML: () -> String = {
            if let text = self.text {
                return "<\(self.name)>\(text)</\(self.name)>"
            } else {
                return "<\(self.name) />"
            }
        }

        init(name: String, text: String? = nil) {
            [self.name][2] = name
            self.text = text
        }

        deinit {
            println("\(name) is being deinitialized")
        }

    }
    var paragraph: HTMLElement? = HTMLElement(name: "p", text: "hello, world")
    println(paragraph!.asHTML())
    // prints "<p>hello, world</p>
    ```

    * ![](iOS%3A%20Swift%20Programming%20(iBook).resources/92D56D5E-0877-48C0-8873-816A21C3CCCC.png)

### Resolving Strong Reference Cycles for Closures

  * Define a capture list as part of the closure's definition
  * Capture list defines the rules to use when capturing one or more reference types within the closure's body
  * You can declare captured reference to be a weak or unknown reference
  * Note
    * Write self.someProperty or self.someMethod, instead of removing the self to help you remember that it's possible to capture self by accident
  * Defining Capture List

    ```swift
    lazy var someClosure: (Int, String) -> String = {
        [unowned self] (index: Int, stringToProcess: String) -> String in
        // closure body goes here
    }
    ```
      * Or

      ```swift
      lazy var someClosure: () -> String = {
        [unowned self] in
        // closure body goes here
      }
      ```

  * Weak and Unknowned References
    * If captured reference will never become nil, it should be captured as an unowned reference, rather than a weak reference

## Optional Chaining

### Overview

  * Process of querying and calling properties, methods, and subscripts on an optional that might currently be nil
  * If the called entity is nil, it will return nil if not the value
  * Multiple queries can be chained together, and fail gracefully if any of the link chain is nil
  * Note
    * Optional chaining in Swift similar to messaging nil in Obj-C, but that works for any type, and that can be checked for success or failure.

### Optional Chaining as an Alternative to Forced Unwrapping

  * Place a question mark (?) after the optional value to chain

    ```swift
    class Person {
        var residence: Residence?
    }

    class Residence {
        var numberOfRooms = 1
    }

    let john = Person()
    let roomCount = john.residence!.numberOfRooms // this trigger a runtime error
    ```

  * Use optional chaining:

    ```swift
    if let roomCount = john.residence?.numberOfRooms {
        println("John's residence has \(roomCount) room(s).")
    } else {
        println("Unable to retrieve the number of rooms.")
    }
    ```

### Defining Model Classes for Optional Chaining

  * Optional chaining can be more than on level
  * Model classes

    ```swift
    class Person {
        var residence: Residence?
    }

    class Residence {
        var rooms = [Room]()
        var numberOfRooms: Int {
            return rooms.count
        }
        subscript(i: Int) -> Room {
            get {
                return rooms[i]
            }
            set {
                rooms[i] = newValue
            }
        }
        func printNumberOfRooms() {
            println("The number of rooms is \(numberOfRooms)")
        }
        var address: Address?
    }

    class Room {
        let name: String
        init(name: String) { [self.name][2] = name }
    }

    class Address {
        var buildingName: String?
        var buildingNumber: String?
        var street: String?
        func buildingIdentifier() -> String? {
            if buildingName != nil {
                return buildingName
            } else if buildingNumber != nil {
                return buildingNumber
            } else {
                return nil
            }
        }
    }
    ```

### Accessing Properties Through Optional Chaining

  * Use optional chaining to access property on optional value or to check if property access is successful

    ```swift
    let john = Person()
    if let roomCount = john.residence?.numberOfRooms {
        println("John's residence has \(roomCount) room(s).")
    } else {
        println("Unable to retrieve the number of rooms.")
    }
    ```

### Calling Methods Through Optional Chaining

  * Use optional chaining to call a method on an optional value or to check whether a method call is successful, even if the method does not define a return value

    ```swift
    * Residence#printNumberOfRooms
    func printNumberOfRooms() {
      println("The number of rooms is \(numberOfRooms)")
    }
    ```

  * Method has no return tip, bbut have an implicit value of Void
    * Means they return a value of () or an empty tubule.
  * If you call this on an optional value with optional chaining, the return type will be Void/ not Void, because the return values are always of an optional type when called with  optional chaining

    ```swift
    if john.residence?.printNumberOfRooms() != nil {
      println("It was possible to print the number of rooms.")
    } else {
      println("It was not possible to print the number of rooms.")
    }
    // prints "It was not possible to print the number of rooms.
    ```

### Accessing SubscriptsThrough Optional Chaining

  * Overview
    * To retrieve and set a value of a subscript on an optional value, and to check if the subscript call is successful
    * Note
      * Place the question mark before the subscript's braces, not after

      ```swift
      if let firstRoomName = john.residence?[0].name " { ... }
      ```

  * Accessing Subscripts of Optional Type
    * If a subscript returns a value of optional type, such as the key subscript of Swift's Dictionary type, place  question mark after the subscript's closing bracket to chain on its optional return value.

      ```swift
      var testScores = ["Dave": [86, 82, 84], "Bev": [79, 94, 81]]
      testScores["Dave"]?[0] = 91
      testScores["Bev"]?[0]++
      testScores["Brian"]?[0] = 72

      // the "Dave" array is now [91, 82, 84] and the "Bev" array is now [80, 94, 81]
      ```

### Linking Multiple Levels of Chaining

  * You can link multiple levels of optional chaining
    * If the type you are trying to retrieve is not optional, it will become optional because of optional chaining
    * If the type you are trying to retrieve is already optional, it will not become more optional because of the chaining
    * Thus if you retrieve an Int through optional chaining, and Int? is always returned


      ```swift
      if let johnsStreet = john.residence?.address?.street {
          println("John's street name is \(johnsStreet).")
      } else {
          println("Unable to retrieve the address.")
      }
      // prints "Unable to retrieve the address.
      let johnsAddress = Address()
      johnsAddress.buildingName = "The Larches"
      johnsAddress.street = "Laurel Street"
      john.residence!.address = johnsAddress

      if let johnsStreet = john.residence?.address?.street {
          println("John's street name is \(johnsStreet).")
      } else {
          println("Unable to retrieve the address.")
      }

      // prints "John's street name is Laurel Street.
      ```

### Chaining on Methods with Optional Return Values

  * Use optional chaining to call a method that returns a value of optional type, and to chain the method's return value if needed


    ```swift
    if let buildingIdentifier = john.residence?.address?.buildingIdentifier() {
        println("John's building identifier is \(buildingIdentifier).")
    }
    // prints "John's building identifier is The Larches."
    if let beginsWithThe =
        john.residence?.address?.buildingIdentifier()?.hasPrefix("The") {
            if beginsWithThe {
                println("John's building identifier begins with \"The\".")
            } else {
                println("John's building identifier does not begin with \"The\".")
            }
    }
    // prints "John's building identifier begins with "The"."

    ```

## Type Casting

### Overview

  * A way to check the type of an instance or
  * To treat that instance as if it is a different superclass/subclass from somewhere else in its own hierarchy
  * Implemented with "**is**" and "**as**" operators.
    * To check the type of a value or cast a value to a different type
  * Also used to check whether a type conforms to a protocol

### Defining a Class Hierarchy for Type Casting

```swift
class MediaItem {
    var name: String
    init(name: String) {
        [self.name][2] = name
    }
}
class Movie: MediaItem {
    var director: String
    init(name: String, director: String) {
        self.director = director
        super.init(name: name)
    }
}

class Song: MediaItem {
    var artist: String
    init(name: String, artist: String) {
        self.artist = artist
        super.init(name: name)
    }
}
let library = [
    Movie(name: "Casablanca", director: "Michael Curtiz"),
    Song(name: "Blue Suede Shoes", artist: "Elvis Presley"),
    Movie(name: "Citizen Kane", director: "Orson Welles"),
    Song(name: "The One And Only", artist: "Chesney Hawkes"),
    Song(name: "Never Gonna Give You Up", artist: "Rick Astley")
]
```

### Checking Type

  * Use type check operator (is) to check whether an instance is a certain subclass type

    ```swift
    var movieCount = 0
    var songCount = 0

    for item in library {
        if item is Movie {
            ++movieCount
        } else if item is Song {
            ++songCount
        }
    }
    ```

### Downcasting

  * Downcast a subclass type with type operator (as)
    * Downcasting can fail, there are two types:
      * as? returns optional value
      * as, attempts to downcast and force-unwraps result as a single compound action

    ```swift
    for item in library {
        if let movie = item as? Movie {
            println("Movie: '\(movie.name)', dir. \(movie.director)")
        } else if let song = item as? Song {
            println("Song: '\(song.name)', by \(song.artist)")
        }
    }
    ```

### Type Casting for Any and AnyObject

  * Swift provide two special type aliases for working with non-specific types
    * AnyObject: an instance of any class type
    * Any: an instance of any type at all apart from function types
  * Note
    * Use Any and AnyObject when you explicitly need the behaviour and capabilities.
    * It is always better to be specific with the types you work with.
  * AnyObject
    * When you work with CocoaAPI, it is common to receive an array of [AnyObject]
    * Because Obj-C does not have an Array of explicitly typed objects
    * Use as to downcast each item in the array

      ```swift
      let someObjects: [AnyObject] = [
        Movie(name: "2001: A Space Odyssey", director: "Stanley Kubrick"),
        Movie(name: "Moon", director: "Duncan Jones"),
        Movie(name: "Alien", director: "Ridley Scott")
      ]

      for object in someObjects {

      let movie = object as Movie
      println("Movie: '\(movie.name)', dir. \(movie.director)")
      }
      ```

      * Shorter version
      ```swift
        for movie in someObjects as [Movie] {
          println("Movie: '\(movie.name)', dir. \(movie.director)")
        }
      ```
  * Any
    * To work with a mix of different types including non-class types

      ```swift
      var things = [Any]()

      things.append(0)
      things.append(0.0)
      things.append(42)
      things.append(3.14159)
      things.append("hello")
      things.append((3.0, 5.0))
      things.append(Movie(name: "Ghostbusters", director: "Ivan Reitman"))
      ```
    * Contains Int, Double, String, (Double, Double), Movie

      ```swift
      for thing in things {
          switch thing {
          case 0 as Int:
              println("zero as an Int")
          case 0 as Double:
              println("zero as a Double")
          case let someInt as Int:
              println("an integer value of \(someInt)")
          case let someDouble as Double where someDouble > 0:
              println("a positive double value of \(someDouble)")
          case is Double:
              println("some other double value that I don't want to print")
          case let someString as String:
              println("a string value of \"\(someString)\"")
          case let (x, y) as (Double, Double):
              println("an (x, y) point at \(x), \(y)")
          case let movie as Movie:
              println("a movie called '\(movie.name)', dir. \(movie.director)")
          default:
              println("something else")
          }
      }
      ```

    * Note
      * The case of a switch statement, use the forced version of type cast operator, as.

## Nested Types

### Overview

  * Enums often created to support a specific class or structure's functionality
  * It can be convenient to define utility classes and structures purely for use within the context of a more complex type
  * Define nested types:
    * Nest supporting enumerations, classes, structures within the definition of the type they support

### Nested Types in Action

```swift
struct BlackjackCard {
    // nested Suit enumeration
    enum Suit: Character {
        case Spades = "♠", Hearts = "♡", Diamonds = "♢", Clubs = "♣"
    }

    // nested Rank enumeration
    enum Rank: Int {
        case Two = 2, Three, Four, Five, Six, Seven, Eight, Nine, Ten
        case Jack, Queen, King, Ace

        struct Values {
            let first: Int, second: Int?
        }

        var values: Values {
            switch self {
              case .Ace:
                  return Values(first: 1, second: 11)
              case .Jack, .Queen, .King:
                  return Values(first: 10, second: nil)
              default:
                  return Values(first: self.toRaw(), second: nil)
            }
        }
    }

    // BlackjackCard properties and methods
    let rank: Rank, suit: Suit
    var description: String {
        var output = "suit is \(suit.toRaw()),"
        output += " value is \(rank.values.first)"

        if let second = rank.values.second {
            output += " or \(second)"
        }

        return output
    }
}

let theAceOfSpades = BlackjackCard(rank: .Ace, suit: .Spades)
println("theAceOfSpades: \(theAceOfSpades.description)")
// prints "theAceOfSpades: suit is ♠, value is 1 or 11
```

### Referring to Nested Types

```swift
  let heartsSymbol = BlackjackCard.Suit.Hearts.toRaw()
  // heartsSymbol is "♡"
```

## Extensions

### Overview

  * Add new functionality to existing class, structure or enumeration type
  * Extend types for which you do not have access to the original source code (retroactive modelling)
  * Extension similar to categories in Obj-C, except it does not have names.
  * Extensions in Swift can:
    * Add computed properties and computed static properties
    * Define instance and type methods
    * Provide new inits
    * Define subscripts
    * Define and use new nested types
    * Make an existing type conform to a protocol
  * Note
    * Extensions can add new functionality, but can not override existing functionality

### Extension Syntax

```swift
extension SomeType {
  // new functionality to add to SomeType goes here
}

// Extend with protocols
extension SomeType: SomeProtocol, AnotherProtocol {
  // implementation of protocol requirements goes here
}
```
  * If you define an extension, the new functionality will be available to all instances, even if they were created before the extension was defined.

### Computed Properties

  * Can add computed properties and computed type properties to existing types:

    ```swift
    extension Double {
        var km: Double { return self * 1_000.0 }
        var m: Double { return self }
        var cm: Double { return self / 100.0 }
        var mm: Double { return self / 1_000.0 }
        var ft: Double { return self / 3.28084 }
    }

    let oneInch = [25.4.mm][4]
    println("One inch is \(oneInch) meters")      // prints "One inch is 0.0254 meters"

    let threeFeet = 3.ft
    println("Three feet is \(threeFeet) meters")  // prints "Three feet is 0.914399970739201 meters

    let aMarathon = 42.km + 195.m
    ```

  * Extensions add new computed properties but they cannot add stored properties, add property observers to existing properties

### Initializers

  * Extensions can add new convenience initialisers to a class, but they cannot add new designated initialisers or deinitializers to a class
  * Designated initialisers and deinitializer must always be provided by original class implementation

    ```swift
    struct Size {
        var width = 0.0, height = 0.0
    }

    struct Point {
        var x = 0.0, y = 0.0
    }

    struct Rect {
        var origin = Point()
        var size = Size()
    }

    let defaultRect = Rect()
    let memberwiseRect = Rect(origin: Point(x: 2.0, y: 2.0), size: Size(width: 5.0, height: 5.0))

    extension Rect {
        init(center: Point, size: Size) {
            let originX = center.x - (size.width / 2)
            let originY = center.y - (size.height / 2)
            self.init(origin: Point(x: originX, y: originY), size: size)
        }
    }

    let centerRect = Rect(center: Point(x: 4.0, y: 4.0),
        size: Size(width: 3.0, height: 3.0))
    ```

### Methods

  * Add new instance methods and type methods to existing types

    ```swift
    extension Int {
        func repetitions(task: () -> ()) {
            for i in 0..<self {
                task()
            }
        }
    }

    3.repetitions({
        println("Hello!")
    })
    ```

  * Mutating Instance Methods
    * Instance methods added with extension can also modify (mutate the instance itself

      ```swift
      extension Int {
        mutating func square() {
          self = self * self
        }
      }
      ```

### Subscripts


```swift
extension Int {
    subscript(var digitIndex: Int) -> Int {
        var decimalBase = 1
        while digitIndex > 0 {
            decimalBase *= 10
            --digitIndex
        }
        return (self / decimalBase) % 10
    }
}
746381295[0]  // returns 5
746381295[1]  // returns 9
746381295[2]  // returns 2
746381295[8]  // returns 7
746381295[9]  // returns 0, as if you had requested:
0746381295[9]
```

### Nested Types

```swift
extension Int {
    enum Kind {
        case Negative, Zero, Positive
    }

    var kind: Kind {
        switch self {
        case 0:
            return .Zero
        case let x where x > 0:
            return .Positive
        default:
            return .Negative
        }
    }
}

func printIntegerKinds(numbers: [Int]) {
    for number in numbers {
        switch number.kind {
        case .Negative:
            print("- ")
        case .Zero:
            print("0 ")
        case .Positive:
            print("+ ")
        }
    }
    print("\n")
}

printIntegerKinds([3, 19, -27, 0, -6, 0, 7])  // prints "+ + - 0 - 0 +"
```

## Protocols

### Overiew

  * Defines a blueprint of methods, properties, and other quirements to suit a particular task or piece of functionality.
  * Does not provide an implementation, only describes what an implementation will look like
  * Can be adopted by a class, structure or enumeration
  * Any type that satisfies the requirements conform to that protocol

### Protocol Syntax

```swift
protocol SomeProtocol {
  // protocol definition goes here
}

struct SomeStructure: FirstProtocol, AnotherProtocol {
  // structure definition goes here
}
class SomeClass: SomeSuperclass, FirstProtocol, AnotherProtocol {
  // class definition goes here
}
```

### Protocol Requirements

  * Getter & setter requirements

    ```swift
    protocol SomeProtocol {
      var mustBeSettable: Int { get set }
      var doesNotNeedToBeSettable: Int { get }
    }
    ```

  * Type property protocol, use "static" keyword for structure or enumeration

    ```swift
    protocol AnotherProtocol {
      class var someTypeProperty: Int { get set }
    }
    ```

  * Protocol with a single instance property requirements:

    ```swift
    protocol FullyNamed {
        var fullName: String { get }
    }
    ```

    * Simple structure conforms to FullyNamed protocol

      ```swift
      struct Person: FullyNamed {

        var fullName: String
      }
      let john = Person(fullName: "John Appleseed")
      // john.fullName is "John Appleseed"
      ```

    * Class conforms to the protocol:

      ```swift
      class Starship: FullyNamed {

        var prefix: String?
        var name: String
        init(name: String, prefix: String? = nil) {
            [self.name][2] = name
            self.prefix = prefix
        }
        var fullName: String {
            return (prefix != nil ? prefix! + " " : "") + name
        }
      }
      var ncc1701 = Starship(name: "Enterprise", prefix: "USS")
      // ncc1701.fullName is "USS Enterprise"
      ```

### Method Requirements

  * Protocol can require specific instance methods or type methods to be implemented
  * Use the same syntax as normal methods, but are not allowed to specify default values for method params.

    ```swift
    protocol SomeProtocol {
        class func someTypeMethod()
    }
    protocol RandomNumberGenerator {

        func random() -> Double

    }
    ```

### Mutating Method Requirements

  * If you mark a protocol instance method requirements as mutating, you do not need to write he mutating keyword when writing an implementation of that method for a class
  * Mutating only used by structures and enumerations

    ```swift
    protocol Togglable {
        mutating func toggle()
    }

    enum OnOffSwitch: Togglable {
        case Off, On
        mutating func toggle() {
            switch self {
            case Off:
                self = On
            case On:
                self = Off
            }
        }
    }

    var lightSwitch = OnOffSwitch.Off
    lightSwitch.toggle()  // lightSwitch is now equal to .On
    ```

### Initializer Requirements

  * Same way as normal inits, but without curly braces or an init body:

    ```swift
    protocol SomeProtocol {
      init(someParameter: Int)
    }
    ```

  * Class implementations of Protocol initialisers requirements
    * You can implement a protocol initialiser requirement on a conforming class as either a designated initialiser requirement  or a convenience initializer.
    * In both cases you must mark the initialiser implementation with the "required" modifier:

      ```swift
      class SomeClass: SomeProtocol {

        required init(someParameter: Int) {
          // initializer implementation goes here
        }
      }
      ```

    * Required modifier ensures that you provide explicit or inherited implementation of the initialiser requirement on all subclasses.
    * Note
      * You do not need to mark protocol init with required modifier on classes marked with the final modifier, because final classes can not be subclassed.
  * Subclass implementation, note the override:

    ```swift
    protocol SomeProtocol {
        init()
    }

    class SomeSuperClass {
        init() {
            // initializer implementation goes here
        }
    }

    class SomeSubClass: SomeSuperClass, SomeProtocol {
        // "required" from SomeProtocol conformance; "override" from SomeSuperClass
        required override init() {
            // initializer implementation goes here
        }
    }
    ```

### Protocols as Types

  * Protocol you create will become a fully-fledged type for use in your code
  * Thus, you can use protocol in many places, including:
    * As a parameter type or return type in a function, method or init
    * As a  type of a constant, variable or property
    * As a type of items in an array, dictionary or other container

    ```swift
    class Dice {
        let sides: Int
        let generator: RandomNumberGenerator
        init(sides: Int, generator: RandomNumberGenerator) {
            self.sides = sides
            self.generator = generator
        }
        func roll() -> Int {
            return Int(generator.random() * Double(sides)) + 1
        }
    }

    var d6 = Dice(sides: 6, generator: LinearCongruentialGenerator())

    for _ in 1...5 {
        println("Random dice roll is \(d6.roll())")
    }
    ```

### Delegation

  * A design pattern that enables a class or structure to hand off (or delegate) some of its responsibilities to an instance of another type
  * Implemented by defining a protocol that encapsulates the delegated responsibilities

  ```swift
  protocol DiceGame {
      var dice: Dice { get }
      func play()
  }

  protocol DiceGameDelegate {
      func gameDidStart(game: DiceGame)
      func game(game: DiceGame, didStartNewTurnWithDiceRoll diceRoll: Int)
      func gameDidEnd(game: DiceGame)
  }

  class SnakesAndLadders: DiceGame {
      let finalSquare = 25
      let dice = Dice(sides: 6, generator: LinearCongruentialGenerator())
      var square = 0
      var board: [Int]
      init() {
          board = [Int](count: finalSquare + 1, repeatedValue: 0)
          board[03] = +08; board[06] = +11; board[09] = +09; board[10] = +02
          board[14] = -10; board[19] = -11; board[22] = -02; board[24] = -08
      }
      var delegate: DiceGameDelegate?
      func play() {
          square = 0
          delegate?.gameDidStart(self)
          gameLoop: while square != finalSquare {
              let diceRoll = dice.roll()
              delegate?.game(self, didStartNewTurnWithDiceRoll: diceRoll)
              switch square + diceRoll {
              case finalSquare:
                  break gameLoop
              case let newSquare where newSquare > finalSquare:
                  continue gameLoop
              default:
                  square += diceRoll
                  square += board[square]
              }
          }
          delegate?.gameDidEnd(self)
      }
  }

  class DiceGameTracker: DiceGameDelegate {
      var numberOfTurns = 0
      func gameDidStart(game: DiceGame) {
          numberOfTurns = 0
          if game is SnakesAndLadders {
              println("Started a new game of Snakes and Ladders")
          }
          println("The game is using a \(game.dice.sides)-sided dice")
      }
      func game(game: DiceGame, didStartNewTurnWithDiceRoll diceRoll: Int) {
          ++numberOfTurns
          println("Rolled a \(diceRoll)")
      }
      func gameDidEnd(game: DiceGame) {
          println("The game lasted for \(numberOfTurns) turns")
      }
  }

  let tracker = DiceGameTracker()
  let game = SnakesAndLadders()
  game.delegate = tracker
  game.play()
  ```

### Adding Protocol Conformance with an Extension

  * You can extend existing type to adopt and conform to a new protocol, even if you do not have access to the source code.
  * Extensions can add new properties, methods, and subscripts to an existing type, and are therefore able to add any requirements that a protocol demand.

    ```swift
    protocol TextRepresentable {
      func asText() -> String
    }

    extension Dice: TextRepresentable {
      func asText() -> String {
        return "A \(sides)-sided dice"
      }
    }
    ```

  * Declaring Protocol Adoption with Extension
    * If a type already conforms to a protocol, but has not adopted that protocol you can make it adopt the protocol with an empty extension:

      ```swift
      struct Hamster {
        var name: String

        func asText() -> String {
          return "A hamster named \(name)"
        }
      }

      extension Hamster: TextRepresentable {}
      let simonTheHamster = Hamster(name: "Simon")
      let somethingTextRepresentable: TextRepresentable = simonTheHamster"
      ```

    * Note
      * Types do not automatically adopt a protocol  by just satisfying its requirements, they must explicitly declare their adoption of the protocol

### Collections of Protocol Types

  * Protocol can be used as the type to be stored in collection as as array/dictionary:

    ```swift
    let things: [TextRepresentable] = [game, d12, simonTheHamster]
    for thing in things {
        println(thing.asText())
    }
    ```

### Protocol Inheritance

  * Protocol can inherit one or more other protocols and can add further requirements on top of the requirements it inherits:

    ```swift
    protocol InheritingProtocol: SomeProtocol, AnotherProtocol {
        // protocol definition goes here
    }

    protocol PrettyTextRepresentable: TextRepresentable {
        func asPrettyText() -> String
    }
    ```

### Class-Only Protocol

  * Limit protocol adoption to class types (and not structures or enumerations) by adding the class keyword to a protocol's inheritance list:

    ```swift
    protocol SomeClassOnlyProtocol: class, SomeInheritedProtocol {
      // class-only protocol definition goes here
    }
    ```

  * Note
    * Use a class-only protocol when the behaviour defined that protocol's requirements assumes or requires that a conforming type has reference semantics rather than value semantics.

### Protocol Composition

  * You can combine multiple protocols into a single protocol composition.
    * protocol<SomeProtocol, AnotherProtocol>

    ```swift
    protocol Named {
        var name: String { get }
    }
    protocol Aged {
        var age: Int { get }
    }
    struct Person: Named, Aged {
        var name: String
        var age: Int
    }
    func wishHappyBirthday(celebrator: protocol<Named, Aged>) {
        println("Happy birthday \(celebrator.name) - you're \(celebrator.age)!")
    }
    let birthdayPerson = Person(name: "Malcolm", age: 21)
    wishHappyBirthday(birthdayPerson)  // prints "Happy birthday Malcolm - you're 21!"
    ```

  * Note
    * Protocol compositions do not define a new, permanent protocol type, rather they define a temporary local protocol that has the combined requirements of all protocols in the composition.

### Checking for Protocol Conformance

  * You can use is and as operators

    ```swift
    @objc protocol HasArea {
      var area: Double { get }
    }
    ```

  * Note
    * You can check protocol conformance only if your protocol is marked with the @objc attribute
    * It indicates that protocol should be exposed to Objective-C Code
    * @objc protocols can be adopted only by classes, not by structures or enumerations


    ```swift
    class Circle: HasArea {
        let pi = 3.1415927
        var radius: Double
        var area: Double { return pi * radius * radius }
        init(radius: Double) { self.radius = radius }
    }

    class Country: HasArea {
        var area: Double
        init(area: Double) { self.area = area }
    }

    for object in objects {
        if let objectWithArea = object as? HasArea {
            println("Area is \(objectWithArea.area)")
        } else {
            println("Something that doesn't have an area")
        }
    }
    ```

### Optional Protocol Requirements

  * These requirements do not have to be implemented by types that conform to the protocol
  * Prefixed by "optional"
  * Optional protocol requirement can be called with optional chaining
  * You can check implementation of an optional requirement by writing a question mark after the name of the requirement
    * someOptionalMethod?(someArgument)
  * Optional property/method requirements will return an optional value
  * Note
    * Optional protocol can only be specified if the protocol is marked with the @objc attribute
    * Even if you are not interoperating with Obj-C you need to mark your protocols with @objc
    * @objc can only be adopted by classes, not structures/enumerations

    ```swift
    @objc protocol CounterDataSource {
        optional func incrementForCount(count: Int) -> Int
        optional var fixedIncrement: Int { get }
    }

    @objc class Counter {
        var count = 0
        var dataSource: CounterDataSource?
        func increment() {
            if let amount = dataSource?.incrementForCount?(count) {
                count += amount
            } else if let amount = dataSource?.fixedIncrement? {
                count += amount
            }
        }
    }

    class ThreeSource: CounterDataSource {
        let fixedIncrement = 3
    }

    var counter = Counter()
    counter.dataSource = ThreeSource()

    for _ in 1...4 {
        counter.increment()
        println(counter.count)
    }

    class TowardsZeroSource: CounterDataSource {
        func incrementForCount(count: Int) -> Int {
            if count == 0 {
                return 0
            } else if count < 0 {
                return 1
            } else {
                return -1
            }
        }
    }

    counter.count = -4
    counter.dataSource = TowardsZeroSource()

    for _ in 1...5 {
        counter.increment()
        println(counter.count)
    }
    // -3
    // -2
    // -1
    // 0
    // 0
    ```

## Generics

### Overview

  * Enables you to write flexible, reusable functions and types that can work with any type, subject to requirements that you define.
  * Avoid duplication and expresses its intent in a clear, abstracted manner
  * Most powerful feature of Swift, much of the Swift standard library is built with generic code.
  * You have been using generics throughoutLanguage Guide
    * Swift's Array and Dictionary types are both generic collections
    * You can create an array of any types

### The Problem That Generic Solve

  * Fixed Type Example

    ```swift
    func swapTwoInts(inout a: Int, inout b: Int) {
        let temporaryA = a
        a = b
        b = temporaryA
    }

    var someInt = 3
    var anotherInt = 107

    swapTwoInts(&someInt, &anotherInt)
    println("someInt is now \(someInt), and anotherInt is now \(anotherInt)")
    // prints "someInt is now 107, and anotherInt is now 3

    func swapTwoStrings(inout a: String, inout b: String) {
        let temporaryA = a
        a = b
        b = temporaryA
    }

    func swapTwoDoubles(inout a: Double, inout b: Double) {
        let temporaryA = a
        a = b
        b = temporaryA
    }
    ```

  * In all 3 functions, it is important that the types a and b are defined to be the same as each other.

### Generic Functions

```swift
func swapTwoValues<T>(inout a: T, inout b: T) {
    let temporaryA = a
    a = b
    b = temporaryA
}
```

  * Comparison

    ```swift
    func swapTwoInts(inout a: Int, inout b: Int)
    func swapTwoValues<T>(inout a: T, inout b: T)

    var someInt = 3
    var anotherInt = 107
    swapTwoValues(&someInt, &anotherInt)
    // someInt is now 107, and anotherInt is now 3

    var someString = "hello"
    var anotherString = "world"
    swapTwoValues(&someString, &anotherString)
    // someString is now "world", and anotherString is now "hello"
    ```

    * Note
      * swapTwoValues inspired by generic function called swap, which is part of Swift standard library, is automatically made available for you to use in your apps

### Type Parameters

  * In the swapTwoValues, the placeholder T is an example of a type parameter.
    * Type parameter specify and name a placeholder type, and are written immediately after the function's name, between a pair of matching angle bracket (such as <T>)
    * Once you specify the type parameter, you can use it to define the type of a function's parameter, function's return type and or as a type annotation within the body of the function
    * You can provide more than one type parameter by writing type parameter name within the angle bracket.
  * Naming Type Parameters
    * Traditional to use single-character name T
    * But, you can use any valid identifier for the type parameter name
    * Complex generic functions, or generic types with multiple parameters, useful to provide more descriptive parameter names.
    * Example:
      * Dictionary uses KeyType and ValueType
    * Note
      * Always give type parameters UpperCamelCase to indicate they are placeholder for a type not a value

### Generic Types

  * Custom classes, structures, and enumerations that can work with any type, similar to Array and Dictionary
  * Example, create a Stack
    * The concept of stack is used by UINavigationController.
    * Call pushViewController:animated and popViewControllerAnimated:
    * Last in, first out
    * ![](iOS%3A%20Swift%20Programming%20(iBook).resources/CC626F62-D041-4B0F-8F78-4DEA2FD8B5D9.png)
  * Integer Stack:

    ```swift
    struct InStack {
        var items = [Int]()
        mutating func push(item: Int) {
            items.append(item)
        }

        mutating func pop() -> Int {
            return items.removeLast()
        }
    }
    ```

  * Generic Stack:

    ```swift
    struct Stack<T> {
        var items = [T]()

        mutating func push(item: T) {
            items.append(item)
        }

        mutating func pop() -> T {
            return items.removeLast()
        }
    }

    var stackOfStrings = Stack<String>()
    stackOfStrings.push("uno")
    stackOfStrings.push("dos")
    stackOfStrings.push("tres")
    ```

### Extending a Generic Type

  * When you extend a generic type, you do not provide a type parameter list as part of the extension's definition.
  * Type parameter list from the original type definition is available within the body of the extension
  * The original type parameter names are used to refer to the type parameters of the original definition

    ```swift
    extension Stack {
        var topItem: T? {
            return items.isEmpty ? nil: items[items.count - 1]
        }
    }
    ```

### Type Constraints

  * Overview
    * To enforce certain type constraints on the types that can be used with generic functions and generic types
    * Type constraints specify a type parameter must inherit from a specific class or conform to a protocol composition
    * Dictionary places a limitation on the types that can be used as keys for a dictionary
    * Keys must be hashable, conform to the Hashable protocol
  * Type Constraint Syntax

    ```swift
    extension Stack {
        var topItem: T? {
            return items.isEmpty ? nil: items[items.count - 1]
        }
    }
    ```

  * Type Constraints in Action
    * Type specific version

      ```swift
      func findStringIndex(array: [String], valueToFind: String) -> Int? {
        for (index, value) in enumerate(array) {
            if value == valueToFind {
                return index
            }
        }
        return nil
      }

      let strings = ["cat", "dog", "llama", "parakeet", "terrapin"]

      if let foundIndex = findStringIndex(strings, "llama") {
        println("Found index: \(foundIndex)")
      }
      ```

      * Generic version

        ```swift
        func findIndex<T: Equatable>(array: [T], valueToFind: T) -> Int? {
          for (index, value) in enumerate(array) {
              if value == valueToFind {
                  return index
              }
          }

          return nil
        }

        let doubleIndex = findIndex([3.14, 0.1, 0.25], 9.3)
        let stringIndex = findIndex(["Mike", "John", "Andrea"], "John")
        ```

### Associated Types

  * Overview
    * When defining a protocol, sometimes, it is useful to declare one or more associated types as part of the protocol's definition.
    * Gives a placeholder name (alias) to a type that is used as part of the protocol
    * Actual type to use for the associated type is not specified until the protocol is adopted
  * Associated Types in Action

    ```swift
    protocol Container {
      typealias ItemType
      mutating func append(item: ItemType)

      var count: Int { get }
      subscript(i: Int) -> ItemType { get }
    }
    ```

    * Int Stack Implementation

      ```swift
      struct IntStack: Container {
          // original IntStack implementation
          var items = [Int]()
          mutating func push(item: Int) {
              items.append(item)
          }

          mutating func pop() -> Int {
              return items.removeLast()
          }

          // conformance to the Container protocol
          typealias ItemType = Int
          mutating func append(item: Int) {
              self.push(item)
          }

          var count: Int {
              return items.count
          }

          subscript(i: Int) -> Int {
              return items[i]
          }
      }
      ```

    * Generic Type Implementation, Swift is able to infer that T refers to ItemAlias in the protocol:

      ```swift
      struct Stack<T>: Container {
          var items = [T]()

          mutating func push(item: T) {
              items.append(item)
          }

          mutating func pop() -> T {
              return items.removeLast()
          }

          // conformance to Container protocol
          mutating func append(item: T) {
              self.push(item)
          }

          var count: Int {
              return items.count
          }

          subscript(i: Int) -> T {
              return items[i]
          }
      }
      ```

### Where Clause

  * Define requirements on the type parameters associated with a generic function or type
  * Define where clauses as part of a type parameter list
  * Where clause allows you to require that an associated type conforms to a certain protocol **and/or** certain taupe parameters an associated types to be the same

    ```swift
    func allItemsMatch<C1: Container, C2: Container where C1.ItemType == C2.ItemType, C1.ItemType: Equatable> (someContainer: C1, anotherContainer: C2) -> Bool {
        if someContainer.count != anotherContainer.count {
            return false
        }

        for i in 0..<someContainer.count {
            if someContainer[i] != anotherContainer[i] {
                return false
            }
        }

        return true
    }

    var stackOfStrings = Stack<String>()
    stackOfStrings.push("1")
    stackOfStrings.push("2")
    stackOfStrings.push("3")

    //var arrayOfStrings = ["1", "2", "3"]
    // Error cause array of String does not conform to Container protocol
    var arrayOfStrings = Stack<String>()
    arrayOfStrings.push("1")
    arrayOfStrings.push("2")
    arrayOfStrings.push("3")

    if allItemsMatch(stackOfStrings, arrayOfStrings) {
        println("All items match.")
    } else {
        println("Not all items match.")
    }
    ```

## Access Control

### Overview

  * Restricst access to parts of your code from code in other source files and modules
  * You can assign specific access levels to individual types (classes, structures, and enumerations), as well as properties, methods, initialisers, subscripts
  * Protocols can be restricted to a certain context, as can global constants, variables and functions
  * Reduces the need to specify explicit access control levels by providing default access levels for typical scenarios
  * Note
    * Various aspics of your code that can have access control (properties, types, functions, etc) are referred as entities

### Modules and Source Files

  * Swift's access control model is base on the concept of modules and source files
  * Module is a single unit code of distributions
    * A framework or application buildt and shipped as a single entity that can be imported by another module with Swift's **import** keyword
    * Each build target (such as an app bundle or framework) in Xcode is treated as a separate module in Swift
  * A source file is a single Swift source code within a module (in effect a single file within an app or framework
    * Though it is common to define individual types in a separate source files, a single source file can contain multiple types, functions, and so on

### Access Levels

  * **Overview**
    * 3 different access levels
      * Public access
        * Entities to be used within any source file from their defining module and also in a source file from another module that imports the defining module
        * When specifying the public interface to a framework
      * Internal access
        * Entities to be used within any source file from their defining module, but not in any source file outside that module
        * When defining an app's or framework's internal structure
      * Private access
        * Restrict the use of an entity to its own defining source file
        * To hide implementation of a specific piece of functionality
  * **Guiding Principle of Access Levels**
    * No entity can be defined in terms of another entity that has a lower (more restrictive) access level
    * Example:
      * A public variable cannot be defined as having an internal or private type, because the type might not be available everywhere that the public variable is used
      * A function cannot have a higher access level than its parameter types and return type
  * **Default Access Levels**
    * Internal access with a few exceptions
  * **Access Levels for Single-Target App**
    * Typically you only need an internal access, unless you want to mark some parts of your code as private in order to hide their implementation details from other app's module.
  * **Access Levels for Framework**
    * Public access, as you are building public facing interface
    * Note
      * Any internal implementation details can still be internal or private.

### Access Control Syntax

  * Syntax

    ```swift
    public class SomePublicClass {}
    internal class SomeInternalClass {}
    private class SomePrivateClass {}

    public var somePublicVariable = 0
    internal let someInternalConstant = 0
    private func somePrivateFunction() {}
    ```

    * Implicit - internal access

      ```swift
      class SomeInternalClass {}              // implicitly internal
      var someInternalConstant = 0            // implicitly internal
      ```

  * Custom Types
    * If you want to specify an explicit access level to a custom type, do at the point that you define the type.
      * The new type can then be used whenever its access level permits.
      * Access level of a type also affects the default access level of type's members (properties, methods, inits and subscripts)
      * If type's access level i private, all its members default level is also private
    * Note
      * A public type defaults to having internal members, not public members
      * If you want type member to be public, you must explicitly mark it as such
      * Ensure API is something you opt-in to publish

      ```swift
      public class SomePublicClass {         // explicitly public class
          public var somePublicProperty = 0 // explicitly public class member
          var someInternalProperty = 0 // implicitly internal class member
          private func somePrivateMethod() {} // explicitly private class member
      }

      class SomeInternalClass {              // implicitly internal class
          var someInternalProperty = 0 // implicitly internal class member
          private func somePrivateMethod() {} // explicitly private class member
      }

      private class SomePrivateClass {       // explicitly private class
          var somePrivateProperty = 0 // implicitly private class member
          func somePrivateMethod() {}         // implicitly private class member
      }
      ```

    * Tuple Types
      * Access level for a tuple type is the most restrictive access level of all types used in the tuple.
      * If members of the tuple comprises of internal and private access, tuple will be private
      * Note
        * Tuple does not have a standalone definition in a way that classes, structures, enums and functions do
        * Tuple type's access is deduced automatically when the tuple is used
    * Function Types
      * Access level for a function type is calculated as the most restrictive access level of the function's parameter types and return type

        ```swift
        func someFunction() -> (SomeInternalClass, SomePrivateClass) {
          // function implementation goes here
        }
        ```

        * Because the function's return type is private, you must mark the function's overall access level with private:

          ```swift
          private func someFunction() -> (SomeInternalClass, SomePrivateClass) {
          // function implementation goes here
          }
          ```

    * Enumeration Types
      * Individual cases of an enums automatically receive the same access level as the enum they belong to
      * Can't specify different access level for individual enum cases

        ```swift
        public enum CompassPoint {
          case North
          case South
          case East
          case West
        }
        ```

    * Raw Values and Association Type
      * The types used for any raw values or associated values in enum must have an access level at least as high as the enum's access level
      * You cannot use a private type as the raw value type of an enumeration with an internal access level for example.
    * Nested Types
      * Nested types within a private type will be private
      * Nested types in a public type or internal type will be internal
      * Explicitly declare public type as public to be public
  * Subclassing
    * Subclass cannot have a higher level access level than its superclass
    * You can override any class member that is visible in a certain access context
      * An override can make inherited class more accessible than its superclass
        * public class A {
        * private func someMethod() {}
        * }
          * internal class B: A {
        * override internal func someMethod() {}
        * }
    * Valid for a subclass member to call a superclass member that has lower access permission, as long as the call takes place within the allowed access level context
      * same source file as the superclass for a private member call
      * within the same module for internal member call

      ```swift
      public class A {
          private func someMethod() {}
      }

      internal class B: A {
          override internal func someMethod() {
              super.someMethod()
          }
      }
      ```

### Constants, Variables, Properties, and Subscripts

  * A contant, variable or property cannot be more public than its type
  * If a class member makes use of a private type, the member must also be declared as private
    * private var privateInstance = SomePrivateClass()
  * **Getters and Setters**
    * Getters and setters for class members (constants, vars, props, subscripts) automatically receive the same access they belong to
    * You can give setter a lower access level than its corresponding getter to restrict the read-write scope of that member.
      * By writing **private(set)** or **internal(set)** before the var or subscript introducer
    * Note
      * This rule apply for stored and computed properties

        struct TrackedString {
            private(set) var numberOfEdits = 0
            var value: String = "" {
                didSet {
                    numberOfEdits++
                }
            }
        }

        var stringToEdit = TrackedString()
        stringToEdit.value = "This string will be tracked."
        stringToEdit.value += " This edit will increment numberOfEdits."
        stringToEdit.value += " So will this one."
        println("The number of edits is \(stringToEdit.numberOfEdits)")
        // prints "The number of edits is 3"

      * You can assign explicit access level for both getter and setter if required, e.g. numberOfEdits getter is public and set is private:

        ```swift
        public struct TrackedString {
            public private(set) var numberOfEdits = 0
            public var value: String = "" {
                didSet {
                    numberOfEdits++
                }
            }
            public init() {}
        }
        ```

### Initializers

  * Custom inits can be assigned access level <= type they initialise
  * Except for required init must have the same access level as the class it belongs to
  * As with functions/methods, types of params cannot be more private than the init
  * **Default Initializers**
    * Default init has the same access level as the type initializes
    * For a public type, the default init is considered internal
      * Declare as public if you need to expose it
  * **Default Memberwise Initializers for Structure Types**
    * Default member wise init for a structure is considered private if any of the structure's stored properties are private
    * Otherwise it is internal

### Protocols

  * If you want to assign an explicit level to a protocol type, do so at the point that you define a protocol
    * Access level of each requirement within a protocol definition is automatically set to the same access level as the protocol
    * Cannot set a different access level than the protocol it supports
    * Ensure that all the protocol's requirements will be visible on any type that adopts the protocol
  * Note
    * If you define public protocol, the protocol's requirements require a public access level for those requirements when they are implemented
  * **Protocol Inheritance**
    * Inherited protocol have the same access level with its parent.
    * You cannot write a public protocol that inherits from an internal protocol
  * **Protocol Conformance**
    * A type can conform to a protocol with a lower access level than the type itself
    * The context type conforms to a  particular protocol is the min of the type's access level and the protocol's access level
      * If a type is public, and protocol is internal, type's conformance to that protocol is also internal
    * Implementation of each protocol requirement has at least the same access level as the type's conformance to that protocol
      * If a public type conforms to a internal protocol, the type's implementation of each protocol requirement must be at least internal
    * Note
      * In Swift as in Obj-C protocol conformance is global, it is not possible for a type to conform to a protocol in two different ways within the same program

### Extensions

  * Any members added in an extension have the same default access level as the type members declared in the original type being extended.
  * **Adding a protocol conformance with an extension**
    * You cannot provide an explicit access level modifier for an extension if you are using that extension to add protocol conformance.
    * Protocol's own access level is used to privde the default access for each of the protocol requirements.

### Generics

  * Access level for a generic type/function is the minimum of the access level of the generic type/function itself and the access level of any type constraints on its type parameters.

### TypeAliases

  * Any type aliases you define are treated as distinct types for the purpose of access control
  * A type alias can have an access level less <= access level of the type it aliases.
  * Note
    * This rule also applies to type aliases for associated types used to satisfy protocol conformances

## References

* [The Swift Programming Language](https://developer.apple.com/library/ios/documentation/swift/conceptual/Swift_Programming_Language/index.html#//apple_ref/doc/uid/TP40014097-CH3-XID_0)
* [Swift - Apple Developer](https://developer.apple.com/swift/)


