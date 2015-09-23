# IF plugin for jQuery #
## v 1.0.2 ##

**By Todd Northrop**

This jQuery plugin adds conditional branching to jQuery matched set chaining.

For me personally, I dig this plugin because it was born out of necessity, and not because I saw something on the Web and said, "Hey, cool, I want to build me one of _those_."  It was an original idea.  Maybe something like this existed elsewhere, but I haven't seen it.

## How it Works ##

The IF plugin works by manipulating the jQuery matched set during the chained function call execution. It takes advantage of the fact that jQuery functions typically continue executing along the function chain, even if the matched set is empty that the function call does nothing.

When `.IF()` is executed and evaluates to false, the matched set is emptied, making subsequent function calls in the chain do nothing, and the original matched set is restored when the next `.ELSE()` or `.ENDIF()` is encountered.

The `.ELSE()` function takes an optional argument, making it possible to implement 'else if' functionality.  Here's an example of how it would be used.
```
$( "#myElement" )
   .IF( myVar == "yes" )
      .css( "color", "green" )
      .click( function () { alert( "Yes" ); } )
   .ELSE( myVar == "maybe" )
      .css( "color", "yellow" )
      .click( function () { alert( "Maybe" ); } )
   .ELSE()
      .css( "color", "red" )
      .click( function () { alert( "No" ); } )
   .ENDIF()
   .show();
```
Of course, this may not be the best example from a coding logic standpoint, but at least provides a clear illustration of the usage, making the conditional branching easily recognizable. It also provides a good example of how the JavaScript code can be indented to provide legibility.

## Arguments ##

The `.IF()` and `.ELSE()` functions can take pretty much any type of argument to evaluate, and the normal JavaScript "truthy/falsey" rules apply to determine if the subsequent chained function calls will be executed on the original matched set.

The only except is if a **function** is passed for the argument. In that case, the function is **executed**, with the matched set assigned as the context (the value of 'this'), and the function's return value is used to determine if the `.IF()`/`.ELSE()` succeeds or fails. The demonstrations included in the download package highlight this technique.

## Nesting ##

Yes, you can use nested conditional branching.  The demo page included in the download package contains examples of nesting `.IF()` structures.

## Naming Conventions ##

I wish I could have used the lower-cased `.if()`, `.else()` and `.endif()`, but unfortunately JavaScript does not allow a dot-notation version of a reserved word. Interestingly, it does accept an array-indexed version of a reserved word, like: `$("#myElement")['if']( ... ).css( ... )...etc`. But I think a few jQuery developers might be slightly put-off by that syntax.

I arrived at using an upper-cased version of 'if' after looking at dozens of alternatives, and disliking them all for various reasons. As a rule, I don't like to break with standard naming conventions.

On the plus side, even though all-caps does not match with the camelCase naming standards in jQuery, I don't think there is any standard that prohibits its use either.

Also, by making `.IF()`, `.ELSE()`, and `.ENDIF()` upper-case, the branching logic becomes quite visible and clear when examining code.