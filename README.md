# Petram: Chiseled for Clarity

## What is Petram?

Petram is a general-purpose programming language with verbosity as a feature. It aims to be extremely strict, rigid, but still ergonomic and expressive enough to the point where writing code in it becomes effortless.

**<u>Petram IS STILL IN ITS INFANCY!</u>**

I'm still very much in the middle of refining the syntax and capabilities of the langauge, despite having laid the foundational guidelines. There's not even an implementation yet! It'll be an interpreted language first, and later on it will become compiled, though we might still keep the interpreted version around.

## What is the point of Petram?

**None!** While I would love it if this project saw some adoption, I am fully aware that it's quirky and could definitely be seen as counterintuitive by some. Let me list what Petram is ****not****
  
* It is **NOT** a C killer or anything
* It is **NOT** meant to be extremely popular or to replace any existing workflow
* It is **NOT** meant to cater to already existing languages and their syntactical principles.

I'm developing Petram as a passion project for myself first, and others second. I have firm principles on how it should operate and what its purpose is, and I will maintaint its "quirks" as much as possible (within reason, of course).
It's an excercise in language design, lexing, parsing, and integrating into a compiler backed ([QBE tentatively](https://c9x.me/compile/))

## Yeah okay, show me some code examples

```erg
-- hello_world.petra

-- This is a single line comment.
-- The `main` function is the entry point of a program, similar to most others out there.
-- It takes a list of strings as command line arguments, again, similar to most others out there.
-- It returns either nothing (Void) or an Int as per Unix convention.
-- Here, we use Void and print "Hello, World!" to stdout.
func #[main :: args: List<String>]#: Void ->
    #[println :: message: "Hello, World!\n"]#
```

```erg
-- variables.petra

-- Variables are prefixed with a dollar sign `$`, similar to PowerShell, Perl, and PHP.
-- This is to disambiguate locally scoped variables from function parameters or struct fields.

func #[main :: args: List<String>]#: Int ->
    -- There are two types of assignment, inspired by languages such as Go, Jai, and Odin.
    -- The first one is the implicit type inferrence operator `:=`
    $retval := 0

    -- The second one is where you explicitly declare the type of the variable.
    -- Note the separation of the colon `:` from the equals sign `=`
    -- Naturally, variables being what they are, they can be re-assigned, provided their type remains consistent
    $retval: Int = 0

    -- Here's some string interpolation too! Simply use curly braces {} with your variable name to interpolate.
    #[println :: message: "The return value is {$retval}"]#

    -- This will return 0, indicating normal program termination
    return $retval

```

```erg
-- functions.petra

{-
    Here's a multiline comment. We will expand this to allow for documenting arguments and return types.
    This is a regular function definition.

    There are two ways to define a function:
    1. Regular block expressions
    2. Lambda (or single line) functions
-}

func #[add_ints :: first: Int, second: Int]#: Int ->
    return first + second

func #[add_ints_lambda :: first: Int, second: Int]#: Int => first + second

func #[main :: args: List<String>]#: Void ->
    -- Any _expression_ is enclosed in #[]#, same as definitions. This is to disambiguate them from statements.
    -- Also note that when calling functions, you _must_ provide the parameter names. This is similar to Jakt's approach, though admittedly less flexible.
    $first_result := #[add_ints :: first: 1, second: 2] -- $first_result == 3

    $second_result := #[add_ints_lambda :: first: 2, second: 3]# -- $second_result == 5

```

```erg

```
