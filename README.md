# MAML
MAML is a minimalist interpreted configuration and data file format


The format is inspired by yaml and json, yet aims to provide both well structured data representation as seen in json, and the readability that comes with yaml.

# Variables
There are four variable types

## Booleans
Booleans are types that are simple to use and are easy to understand

They can be one of two values:
| BinaryValue | Representation |
| ------ | ------ |
| 0x00 | false |
| 0x01 | true |

## Strings
Strings are types that are essential to readable configuration

They can be represented in three different formats:
| FormatName | Representation |
| ------ | ------ |
| Character | 'S' |
| String | "String" |
| Multi-line String | \`Multi-line string\` |

## Numbers
Numbers are types that are essential to any file format

They can be represented in a variety of formats:
| FormatName | Representation |
| ------ | ------ |
| Decimal | 23 |
| Hexadecimal | 0x17 |
| Binary | 0b10111 |

## Tables
Tables are where MAML gets it's dynamic nature from.

They are represented with the following syntax:
```
TableName (
    Key = Value
)
```

They may also be represented with this syntax:
```
TableName (
    Value1
    Value2
)
```
Where the Key for Value1 is the decimal number 0 and the Key for Value2 is the decimal number 1

