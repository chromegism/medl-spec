# medl-spec
The specification for the MEDL (Minimal Explicit Data Language)... language.

## 1. Introduction
MEDL is a human-readable, explicity typed data format. Its goal is to represent structured data with the bare minimum of types and syntax: `string`, `int`, `float`, `bool`, `list`, and `map`. No computation or implicit type coercion is allowed.

## 2. Data types
### Primitives
**String:**
Unicode text, enclosed in quotes. Supports the escape characters of `\"`, `\n`, `\r`, `\t`, `\0`, and of course `\\`.

**Int:**
Signed 64 bit integers. No fractional component.

**Float:**
Decimal numbers with fractional components. Supports exponent notation with `e`. For example: `43.6e8`.

**Bool:**
Either `true` or `false`.

### Composites
**List:**
An ordered sequence of items. They may be of any type, including other lists or maps.

**Map:**
Unordered key-value associations. Keys are always strings, and follow the same notation as identifiers. Values can be of any type.

Data Type | Example           | Notes
----------|-------------------|------
String    | `"hello"`         |
Int       | `654`             |
Float     | `64.9e-5`         |
Bool      | `true` or `false` |
List      | `key[list]:`      |
Map       | `key[map]:`       | 



## 3. Syntax
**Key-value**: `key[type]: value`

**Keys** must start with an alphabetic character, and can contain alphanumeric or underscore characters. They must not contain whitespace.

**Types** follow the same rule as keys.

**Semicolons** are not accepted as valid.


**Lists** start with `- [type]: value`. The number of dashes (`-`) indicates the indentation level, and whitespace between these and the type is ignored.

**Maps** follow the same rules as Key-value pairs, and use dashed, as lists do, to indicate indentation.


**Comments** begin with a `#` and span from their beginning to the end of the line

**Whitespace** between tokens is ignored, however there must not be whitespace within a key or value, unless it is a string. Entries are ended with new lines.

## 4. Semantics
**Type annotations** are necessary for all key-value pairs. Missing types will result in a parsing error.
**Type mismatches** will result in a parsing error.
Lists *preserve* order, whereas Maps do not.
Strings are **UTF-8**.
**Empty Lists/Maps** are allowed.

## 5. Example
```
keyA[string]: "Value1"
keyB[int]: 1234
keyC[float]: 76.5
keyD[string]: "value but with space :)"

list1[list]:
- [string]: "a"
- [string]: "b"
- [bool]: true

keyE[string]: "hi"

# test comment
map1[map]:
- mapkey1[string]: "mapvalue1\" \"\\"
- mapkey2[float]: 777
- mapkey3[bool]: true
```
