### Ergor: Rigor Redefined

## What is Ergor?

Ergor is a general-purpose programming language with verbosity as a feature. It aims to be extremely strict, rigid, but still ergonomic and expressive enough to the point where writing code in it becomes effortless.

### Code example

```erg
{-
    This is a multiline comment.
    We can use this to use docblocks for describing function parameters and return types.
-}
func #[add_two_integers :: a: Int, b: Int]#: Int ->
    return a + b

-- We also have lambda expressions
func #[add_two_integers_lamba :: a: Int, b: Int]#: Int => a + b

func #[divide_two_integers :: dividend: Int, divisor: Int]#: Option<Int, MathError> ->
    if #[divisor == 0]# ->
        #[print :: message: "Divisor must not be 0."]#
        return Option::Error(MathError)
    else ->
        return dividend / divisor

{-
    Here's a moderately complex struct with a constraint.
    A constraint is a mechanism that will not allow you to instantiate a struct if the check fails.
    Constraints is a metadata structure that is accessible from within the struct. You can access it with
    Self::constraints.<field name>
-}
struct #[Square]# ->
    field side_length: Int

    constrain side_length: Int where #[side_length > 0]#
        message: "Side of a square must be greater than 0."

    new #[side_length: Int]#: Self ->
        @side_length = side_length
        -- Constraints are automatically checked here

    method #[calculate_area]#: Int ->
        return @side_length * @side_length

    method #[set_side_length :: new_length: Int]#: Option<(), SizeError> ->
        -- Constraints are automatically checked here too
        match Self::constraints.side_length(new_length) ->
            Option::Some(_) -> 
                @side_length = new_length
                Option::Some(())
            Option::Error(error) -> Option::Error(SizeError)

-- This is a single line comment.
func #[main :: args: List<String>]#: Int ->
    -- Simple variable declaration with type inferrence
    $a := 3

    -- Optional explicit type declaration
    $b: Int = 4
    
    -- Assignment via function call, with implicit and explicit types
    $res := #[add_two_integers :: a: $a, b: $b]#
    $res2: Int = #[add_two_integers_lamba :: a: $a, b: $b]#

    -- Instantiate a struct, which can potentially fail
    match #[Square::new :: side_length: 5]# ->
        Option::Some($square) ->
            #[print :: message: "Square created successfully"]#
        Option::None($error) ->
            #[print :: message: "Error: {$error}"]#

    match #[Square::new :: side_length: -1]# ->
        Option::Some(_) ->
            return 1
        Option::None($error) ->
            #[print :: message: "Error as expected: {$error}"]#

    -- Print the result
    #[print :: message "{$a} + {$b} = {$res}"]#
    return 0
```
