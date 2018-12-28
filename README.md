# YAML

For most software developers, JSON is easy to understand. YAML, on the other hand, is sometimes a little bit unintuitive (my guess: YAML has some ambiguities that JSON has not). This document tries to shed some light on those "problems".

## Links

* [Official website](https://yaml.org/)
* [YAML 1.2 Spec](https://yaml.org/spec/1.2/spec.html)

## Advantages over JSON

YAML is a superset of JSON. Meaning: every valid JSON document can also be written in YAML without losing any information.

YAML has some bells and whistles that JSON documents don't have. The most important advantage is (IMHO):

**Support for comments (pure JSON does *not* allow for comments).**

## Sequences

**Sequences** in YAML lingo are **lists**.

```yml
- Mark McGwire
- Sammy Sosa
- Ken Griffey
```

JSON equivalent:

```json
[ "Mark McGwire", "Sammy Sosa", "Ken Griffey" ]
```

## Mappings

**Mappings** in YAML lingo are **objects**.

```yml
hr:  65    # Home runs
avg: 0.278 # Batting average
rbi: 147   # Runs Batted In
```

JSON equivalent:

```json
{
    "hr": 65,
    "avg": 0.278,
    "rbi": 147
}
```

## Documents

YAML allows you to have multiple "documents" inside a single file/stream.

Documents are separated by `---`.

```yaml
---
- Mark McGwire
- Sammy Sosa
- Ken Griffey

---
- Chicago Cubs
- St Louis Cardinals
```

## Strings and Quotes

YAML doesn't differentiate between strings and scalars in general. However, YAML allows for single and double quotes.

Double quotes allow escape sequences like `\n`.

Single quotes are useful for forcing a string when the first characters would have another meaning otherwise (like `"` or `#`).

```yml
- Some string
- 'Also some string'
- "Yet another\nstring"
- '"Howdy!" he cried.' # Single quote use case 1
- '# Not a ''comment''.' # Single quote use case 2
```

## Multiline Strings

### Literal Style

In **literal** style (`|`), newlines are preserved.

```yml
|
  \//||\/||
  // ||  ||__
```

becomes:

    \//||\/||
    // ||  ||__

### Folded Style

In **folded** style (`>`), newlines are replaced with spaces - unless it ends an empty or a more-indented line.

```yml
>
  Mark McGwire's
  year was crippled
  by a knee injury.
```

becomes:

    Mark McGwire's year was crippled by a knee injury.

```yml
>
  Sammy Sosa completed another
  fine season with great stats.

    63 Home Runs
    0.288 Batting Average

  What a year!
```

becomes:

```
Sammy Sosa completed another fine season with great stats.

    63 Home Runs
    0.288 Batting Average

What a year!
```
