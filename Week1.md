### ECMA script
* Standard for Javascript

### Javascript
* UTF 16 in Javascript - can use different scripts as variable names
* console.log()
* {} is a block 
* let
* const
* var - even if defined inside a block it is visible outside. The entire top-level script can see it.
* let - Later versions of javascript brought it because var was difficult to scope. Allows more restrictive scoping.
* const - works exactly like let - block level scope . Should be used in most places. Cannot be changed.
* Avoid using var.
* scope of a variable
* Namespaces to restrict how different names are seen to different parts of the code 
* Zero indexing of strings and arrays
* String .length .substring
* Length of a string not clearly defined when it is in unicode
* Template string
  - contained within back ticks ' ' 
  - let st = '${s} World!'
* Operators 
  - 3+4 
  - '3'+'4'
  - '3' + 4 (coersion - converts 4 into a string)
  - '3' * '4' - 12
  - Don't use coersion in production code - creates confusion
  - console.log('3' == 3) outputs true
  - Use Strict equality **===** to avoid coersion. Safer to use for comparisons.

### Strings 
* Strings usually use UTF-16 encoding
* Functions like length can give surprising results on non-ASCII strings
