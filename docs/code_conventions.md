# C++ Conventions #

None of these conventions are hard and fast, and there exist exceptions throughout the library.
However, the conventions below should be followed whenever reasonable.


## Classes and Structs ##

* Class names are capitalized.

* Class methods are camel-cased e.g. `obj.doThing(...)` not `obj.do_thing(...)`.

* Private class data members are underscore spaced and end in an underscore.
  For example, `last_energy_` or `curr_index_`.

## File Layout ##

* Each header file should primarily contain one class definition, although other
closely related helper classes may be included.

* Except for class definitions, function declarations, and very short inline functions (i.e. one, perhaps
two lines), all other code goes either at the end of a header
file or in a separate .cc file.

## Formatting ##

* Code should be idented using 4 spaces for each indent level ("soft tabs"). This guarantees
the code will look consistent in text editors regardless of tab stop settings.

* Code should be no more than 80 characters wide. Possible exceptions include long string literals or
if breaking over two lines makes code hard to reason about/debug.

* Braces following function or class declarations, etc., should be on their own line and 
  be indented to the same level as the enclosed code. For example:

        Real
        absSqrt(Real x)
          {
          if(x >= 0)
              return sqrt(x);
          else
              return sqrt(-x);
          }

* The return type of functions and class methods appears at the beginning of the line preceding the function name:

        Real
        calculateSomething(const ITensor& A, const ITensor& B);

  Other keywords such as `friend` or `inline` should come after the return type unless disallowed by the compiler
  (such as when the return type is a reference).

## Functions ##

* The preferred order for function arguments is:
    1. Regular (pass-by-value, such as `int j`) and const reference (such as `const MPO& H`) arguments.
    2. Non-const reference or pointer arguments.
    3. Arguments with defaults (required to come last anyway).

</br>

[[Back to Main|main]]
