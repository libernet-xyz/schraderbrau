# Schraderbrau

[![CI](https://img.shields.io/github/actions/workflow/status/libernet-xyz/schraderbrau/ci.yml?label=CI)](https://github.com/libernet-xyz/schraderbrau/actions/workflows/ci.yml)
[![crates.io](https://img.shields.io/crates/v/starkom-schraderbrau)](https://crates.io/crates/starkom-schraderbrau)
[![license](https://img.shields.io/crates/l/starkom-schraderbrau)](https://github.com/libernet-xyz/schraderbrau/blob/main/LICENSE)

## Overview

Schraderbrau is a ~255-bit prime field and its order is the prime
`0x7ffffffffffffffffffffffffffffffffffffffffffffff90000000000000001`. We call this number `p`.

`p` takes slightly less than 50% of the 256-bit range, leaving the MSB unset so that it can be used
for arbitrary purposes.

## Factors of `p-1`

`p-1`, the greatest integer that fits in a Schraderbrau scalar, is factorized as follows:

$$
2^{64} \cdot 13 \cdot 27241 \cdot 50177 \cdot 994249 \cdot 177649061886023094277927983212050631674349
$$

The 2-adicity of 64 has been chosen to warrant a very large FFT capacity and evaluation domain for
zkSNARK proofs.

## S-box optimization

The factorization of `p-1` does not contain 3, so raising to 3 is a permutation in the field and
$x^3$ can be used as the S-box for algebraic hashes such as [Poseidon][poseidon].

[poseidon]: https://www.poseidon-hash.info/

## Implementation

The implementation is based on the interface from the
[`starkom-ff`](https://crates.io/crates/starkom-ff) crate and uses Montgomery form with four 64-bit
limbs.
