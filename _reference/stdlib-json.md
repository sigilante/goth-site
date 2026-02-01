---
title: JSON Module
---

# JSON Module Reference

`stdlib/json.goth` — pure-Goth JSON parser and serializer.

```goth
use "stdlib/json.goth"
```

## Value Representation

JSON values are tagged 2-tuples `⟨tag, payload⟩`. The tag is an integer that discriminates the JSON type:

| Tag | JSON type | Payload type | Example |
|-----|-----------|--------------|---------|
| 0 | null | `0` (unused) | `⟨0, 0⟩` |
| 1 | boolean | `Bool` | `⟨1, ⊤⟩` |
| 2 | number | `F64` | `⟨2, 3.14⟩` |
| 3 | string | `String` | `⟨3, "hi"⟩` |
| 4 | array | `[n]Json` | `⟨4, [...]⟩` |
| 5 | object | `[n]⟨String, Json⟩` | `⟨5, [⟨"k", v⟩]⟩` |

Use the constructors below rather than building tuples directly.

## Constructors

| Function | Signature | Description |
|----------|-----------|-------------|
| `jsonNull` | `() → Json` | `jsonNull ⟨⟩` |
| `jsonBool` | `Bool → Json` | `jsonBool ⊤` |
| `jsonNum` | `F64 → Json` | `jsonNum 42.0` |
| `jsonStr` | `String → Json` | `jsonStr "hello"` |
| `jsonArr` | `[n]Json → Json` | `jsonArr [jsonNum 1.0, jsonStr "two"]` |
| `jsonObj` | `[n]⟨String, Json⟩ → Json` | `jsonObj [⟨"key", jsonNum 1.0⟩]` |

```goth
let obj = jsonObj [
  ⟨"name", jsonStr "Goth"⟩,
  ⟨"version", jsonNum 1.0⟩,
  ⟨"features", jsonArr [jsonStr "arrays", jsonStr "tuples"]⟩,
  ⟨"stable", jsonBool ⊤⟩
]
```

## Type Predicates

Each returns `Bool` by checking the tag:

| Function | True when |
|----------|-----------|
| `isNull` | tag = 0 |
| `isBool` | tag = 1 |
| `isNum` | tag = 2 |
| `isStr` | tag = 3 |
| `isArr` | tag = 4 |
| `isObj` | tag = 5 |

```goth
isStr (jsonStr "hi")    # ⊤
isNum (jsonStr "hi")    # ⊥
```

## Extractors

Extract the payload directly. These are **unsafe** — the caller must check the tag first (or use `jsonGet`/`jsonIndex` which return Options).

| Function | Signature | Returns |
|----------|-----------|---------|
| `asBool` | `Json → Bool` | Boolean payload |
| `asNum` | `Json → F64` | Number payload |
| `asStr` | `Json → String` | String payload |
| `asArr` | `Json → [n]Json` | Array payload |
| `asObj` | `Json → [n]⟨String, Json⟩` | Object entries |

```goth
let j = jsonNum 42.0 in asNum j    # 42.0
```

## Object and Array Access

| Function | Signature | Description |
|----------|-----------|-------------|
| `jsonGet` | `String → Json → ⟨Bool, Json⟩` | Lookup key in object; returns Option |
| `jsonIndex` | `ℤ → Json → ⟨Bool, Json⟩` | Index into array; returns Option |
| `jsonKeys` | `Json → [n]String` | All keys of an object |
| `jsonValues` | `Json → [n]Json` | All values of an object |
| `jsonLen` | `Json → ℤ` | Length of array or object (0 for others) |

Results follow the Option convention: `⟨⊤, value⟩` on success, `⟨⊥, 0⟩` on miss.

```goth
let r = parseJson "{\"x\":10,\"y\":20}"
in let json = r.1
in let xOpt = jsonGet "x" json
in if xOpt.0 then asNum xOpt.1 else 0.0
# 10.0
```

## Parsing

```goth
╭─ parseJson : String → ⟨Bool, Json, String⟩
```

Returns a Result triple:

- **Success:** `⟨⊤, jsonValue, ""⟩`
- **Failure:** `⟨⊥, 0, errorMessage⟩`

The parser is a recursive descent parser that handles:

- Strings (with escape sequences `\"`, `\\`, `\/`, `\n`, `\t`, `\r`, `\b`, `\f`, `\uXXXX`)
- Numbers (integers, floats, scientific notation)
- Booleans (`true`, `false`)
- Null (`null`)
- Arrays (nested, heterogeneous)
- Objects (nested)
- Whitespace between tokens

```goth
let r = parseJson "[1, \"two\", true, null]"
in if r.0 then toJson r.1 else "parse failed"
# [1,"two",true,null]
```

Trailing content after a valid JSON value is an error:

```goth
parseJson "42 extra"
# ⟨⊥, 0, "trailing content at position 3"⟩
```

## Serialization

| Function | Signature | Description |
|----------|-----------|-------------|
| `toJson` | `Json → String` | Compact JSON string |
| `showJson` | `Json → String` | Alias for `toJson` |

Output is compact (no whitespace). Strings are escaped correctly for JSON.

```goth
toJson (jsonObj [⟨"a", jsonNum 1.0⟩, ⟨"b", jsonArr [jsonBool ⊤]⟩])
# {"a":1,"b":[true]}
```

## Introspection

| Function | Signature | Description |
|----------|-----------|-------------|
| `jsonType` | `Json → String` | Returns `"null"`, `"bool"`, `"number"`, `"string"`, `"array"`, or `"object"` |

```goth
jsonType (jsonStr "hi")     # "string"
jsonType (jsonArr [])       # "array"
```

## Roundtrip Example

Parse JSON, serialize it, re-parse, and verify stability:

```goth
use "stdlib/json.goth"

╭─ main : () → String
╰─ let input = "{\"a\":1,\"b\":[2,3],\"c\":{\"d\":true},\"e\":null}"
   in let r1 = parseJson input
   in if ¬(r1.0) then "parse error"
   else let serialized = toJson r1.1
   in let r2 = parseJson serialized
   in if ¬(r2.0) then "re-parse error"
   else let serialized2 = toJson r2.1
   in if strEq serialized serialized2
      then "PASS: " ⧺ serialized
      else "FAIL"
```

## Notes

- **Encoding:** `\uXXXX` escape sequences in input are replaced with `?` (full Unicode hex decoding is not implemented).
- **Number formatting:** Numbers are serialized via Goth's `toString`, so `1.0` may render as `1` and `0.5` as `0.5`.
- **Performance:** Array building during parsing uses `⧺ [val]` (snoc), which is O(n) per append. Acceptable for typical JSON sizes but not ideal for very large arrays.
