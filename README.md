# **`Pizza`**

> Peripheral EOSIO smart contracts for interacting with Pizza

## Dependencies

- [`sx.uniswap`](https://github.com/stableex/sx.uniswap)

## Quickstart

```c++
#include <sx.pizza/pizza.hpp>
#include <sx.uniswap/uniswap.hpp>

// user input
const asset quantity = asset{10000, symbol{"EOS", 4}};
const uint64_t pair_id = 1; // EOS/USDT pair

// get pizza info
const auto [ reserve_in, reserve_out ] = pizza::get_reserves( pair_id, quantity.symbol );
const uint8_t fee = pizza::get_fee();

// calculate out price
const asset out = uniswap::get_amount_out( quantity, reserves_in, reserves_out, fee );
// => "2.6500 USDT"
```

## Table of Content

- [STATIC `get_reserves`](#static-get_reserves)
- [STATIC `get_fee`](#static-get_fee)

## STATIC `get_reserves`

Get reserves for a pair

### params

- `{name} pair_id` - pair id
- `{symbol} sort` - sort by symbol (reserve0 will be first item in pair)

### returns

- `{pair<asset, asset>}` - pair of reserve assets

### example

```c++
const name pair_id = "eos2usde";
const symbol sort = symbol{"EOS", 4};

const auto [reserve0, reserve1] = pizza::get_reserves( pair_id, sort );
// reserve0 => "4638.5353 EOS"
// reserve1 => "13614.8381 USDE"
```

## STATIC `get_fee`

Get total fee

### returns

- `{uint8_t}` - total fee (trade + protocol)

### example

```c++
const uint8_t fee = pizza::get_fee();
// => 30
```