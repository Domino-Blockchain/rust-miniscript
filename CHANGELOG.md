# 7.0.0-rc1 - March 14, 2022

- Changed the ToPublicKey trait to support x-only keys.
- Add `PsbtExt` trait for psbt operations
  - `Psbt::update_desc` adds information from a descriptor to a psbt. This figures
    out the type of the descriptor and adds corresponding redeem script/witness script
    and tap tree information
- Support for `tr` descriptors with miniscript leaves and multi_a fragment
- Add `derived_descriptor` API to Descriptor so that users no longer need to use
`translate` APIs.
- Update `DescriptorTrait`: `script_code` and `explicit_script` can now fail because
  of taproot descriptors
- Add `PreTaprootDescriptor` and `PreTaprootDescriptorTrait` to support non-failing versions
  of `script_code` and `explicit_script` for non taproot descriptors
- Overhaul the interpreter API to provide simpler APIs `iter(prevouts)` and `iter_assume_sig()`
  so that it no longer takes a closure input.
- Add interpreter support for taproot transactions.
# 6.0.1 - Aug 5, 2021

- The `lift` method on a Miniscript node was fixed. It would previously mix up
  the `X` and `Y` argument of an `andor` fragment.

# 6.0.0 - Jul 29, 2021

- bump `rust-bitcoin` to 0.27
- several bugfixes

# 5.0.0 - Jan 14, 2021

- Remove `PkCtx` from the API
- Move descriptors into their own types, with an enum containing all of them
- Move descriptor functionality into a trait
- Remove `FromStr` bound from `MiniscriptKey`and `MiniscriptKey::Hash`
- Various `DescriptorPublicKey` improvements
- Allow hardened paths in `DescriptorPublicKey`, remove direct `ToPublicKey` implementation
- Change `Option` to `Result` in all APIs
- bump `rust-bitcoin` to 0.26

# 4.0.0 - Nov 23, 2020

- Add support for parsing secret keys
- Add sortedmulti descriptor
- Added standardness and other sanity checks
- Cleaned up `Error` type and return values of most of the API
- Overhauled `satisfied_constraints` module into a new `Iterpreter` API

# 3.0.0 - Oct 13, 2020

- **Bump MSRV to 1.29**

# 2.0.0 - Oct 1, 2020

- Changes to the miniscript type system to detect an invalid
  combination of heightlocks and timelocks
     - Lift miniscripts can now fail. Earlier it always succeeded and gave
       the resulting Semantic Policy
     - Compiler will not compile policies that contain at least one
     unspendable path
- Added support for Descriptor PublicKeys(xpub)
- Added a generic psbt finalizer and extractor
- Updated Satisfaction API for checking time/height before setting satisfaction
- Added a policy entailment API for more miniscript semantic analysis

# 1.0.0 - July 6, 2020

- Added the following aliases to miniscript for ease of operations
	- Rename `pk` to `pk_k`
	- Rename `thresh_m` to `multi`
	- Add alias `pk(K)` = `c:pk_k(K)`
	- Add alias `pkh(K)` = `c:pk_h(K)`
- Fixed Miniscript parser bugs when decoding Hashlocks
- Added scriptContext(`Legacy` and `Segwitv0`) to Miniscript.
- Miscellaneous fixes against DoS attacks for heavy nesting.
- Fixed Satisfier bug that caused flipping of arguments for `and_v` and `and_n` and `and_or`

