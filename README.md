# ElCrimp

**TODO: Add description**

## Installation

If [available in Hex](https://hex.pm/docs/publish), the package can be installed
by adding `el_crimp` to your list of dependencies in `mix.exs`:

```elixir
def deps do
  [
    {:el_crimp, "~> 0.1.0"}
  ]
end
```

Documentation can be generated with [ExDoc](https://github.com/elixir-lang/ex_doc)
and published on [HexDocs](https://hexdocs.pm). Once published, the docs can
be found at [https://hexdocs.pm/el_crimp](https://hexdocs.pm/el_crimp).

# El-Crimp

[![Build Status](https://travis-ci.org/)](https://travis-ci.org/)

ElCrimp is an implementation of [Crimp](https://github.com/BBC-News/crimp) in Elixir.

Please see the [bbc-news/crimp](https://github.com/BBC-News/crimp) repo for more details.

## Implementations

[![Crimp Lua](https://img.shields.io/badge/Crimp-Lua-00007C.svg)](https://github.com/bbc-news/crimpua)
[![Crimp Ruby](https://img.shields.io/badge/Crimp-Ruby-CC342D.svg)](https://github.com/bbc-news/crimp)

## Usage

```lua
ElCrimp.signature({a = {b = 1}}) -- prints "ac13c15d07e5fa3992fc6b15113db900"
```

## Implementation Details

Under the hood ElCrimp annotates the passed data structure to a nested array of primitives (strings, numbers, booleans, nils, etc.) and a single byte to indicate the type of the primitive:

|  Type   | Byte |
|   :-:   |  :-: |
| String  |  `S` |
| Number  |  `N` |
| Boolean |  `B` |
| nil     |  `_` |
| Array   |  `A` |
| Hash    |  `H` |

You can verify it using the `#notation` function:

```elixir
Notation.notate({a=1})
"1NaSAH"
```

Before signing ElCrimp, uses the `#notation` function to transform the return value of a map to a string.

```elixir
Notation.notate({ a: { b: 'c' } })
"aSbScSAHAH"
```

Please note the List and Map keys are sorted before signing.

```elixir
Notation.notate([3, 1, 2])
"1N2N3NA"
```

key/value tuples get sorted as well.

```elixir
Notation.notate([ b: 3 ])
"3NbSAH"
```

## Changelog

### 1.0.0-0

Initial release.

## Testing

For testing we use ExUnit built into Elixir itself

```sh
mix test
```