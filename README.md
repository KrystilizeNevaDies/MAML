# MAML
MAML is a minimalist interpreted configuration and data file format


The format is inspired by yaml and json, yet aims to provide both well structured data representation as seen in json, and the readability that is provided by yaml.

# Variables
There are four variable types:
`Booleans`, `Strings`, `Numbers`, and `Tables`.

The first three types, `Booleans, Strings, and Numbers` are definitive values. Each of these variables must render to a value of that type. 
I.E. null, nil, etc. are not supported.

## Booleans
`Booleans` are types that are useful in binary configuration purposes.
I.E. should X event happen?

They can be one of two values:
| BinaryValue | Representation |
| ------ | ------ |
| 0x00 | false |
| 0x01 | true |

`Booleans` cannot be used as keys in a `Table`.

## Strings
`Strings` are types that contain an ordered collection of characters.

They can be represented in three different formats:
| FormatName | Representation |
| ------ | ------ |
| Character | 'S' |
| String | "String" |
| Multi-line String | \`Multi-line string\` |

## Numbers
`Numbers` are types that represent a set of bits. They have no minimum or maximum value in the file format.
However, the language that parses the format may have a limit.

They can be represented in a variety of formats:
| FormatName | Representation |
| ------ | ------ |
| Decimal | 23 |
| Hexadecimal | 0x17 |
| Binary | 0b10111 |

`Numbers` can be used as keys in `Tables`

## Tables
`Tables` are where MAML gets it's dynamic nature from.

They are represented with the following syntax:
```
TableName [
    Key = Value
]
```

`Table` values may be indexed like so:
```
Settings [
    Port = 80
    HttpPort = 443
]

ServerPort = Settings.Port
```

`Tables` may also be represented with this syntax (Called the array syntax):
```
NumberStrings [
    "zero"
    "one"
]

NumberOneString = NumberStrings.1
```
This syntax automatically assigns `Numbers` as keys starting at 0 to each value


## Dynamic Strings
`Strings`/`Numbers`/`Booleans` are embeddable in other strings' definitions

When an index to a `String`/`Number`/`Boolean` is included in a string with the `{Pointer}` syntax, it is rendered in its definition.

Lets look at some examples:

This file:
```
Config [
  Version = "4.2.3"
  ApplicationName = "App"
]

VersioningMessage = `Hey there,

Welcome to {Config.ApplicationName} version {Config.Version}!

We hope you enjoy your usage.`
```

Renders the `VersioningMessage` variable to be:
```
Hey there,

Welcome to App version 4.2.3!

We hope you enjoy this application.
```
