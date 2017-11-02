Shared Libraries
================

## outbitconsensus

The purpose of this library is to make the verification functionality that is critical to Outbit's consensus available to other applications, e.g. to language bindings.

### API

The interface is defined in the C header `outbitconsensus.h` located in  `src/script/outbitconsensus.h`.

#### Version

`outbitconsensus_version` returns an `unsigned int` with the the API version *(currently at an experimental `0`)*.

#### Script Validation

`outbitconsensus_verify_script` returns an `int` with the status of the verification. It will be `1` if the input script correctly spends the previous output `scriptPubKey`.

##### Parameters
- `const unsigned char *scriptPubKey` - The previous output script that encumbers spending.
- `unsigned int scriptPubKeyLen` - The number of bytes for the `scriptPubKey`.
- `const unsigned char *txTo` - The transaction with the input that is spending the previous output.
- `unsigned int txToLen` - The number of bytes for the `txTo`.
- `unsigned int nIn` - The index of the input in `txTo` that spends the `scriptPubKey`.
- `unsigned int flags` - The script validation flags *(see below)*.
- `outbitconsensus_error* err` - Will have the error/success code for the operation *(see below)*.

##### Script Flags
- `outbitconsensus_SCRIPT_FLAGS_VERIFY_NONE`
- `outbitconsensus_SCRIPT_FLAGS_VERIFY_P2SH` - Evaluate P2SH ([BIP16](https://github.com/outbit/bips/blob/master/bip-0016.mediawiki)) subscripts
- `outbitconsensus_SCRIPT_FLAGS_VERIFY_DERSIG` - Enforce strict DER ([BIP66](https://github.com/outbit/bips/blob/master/bip-0066.mediawiki)) compliance

##### Errors
- `outbitconsensus_ERR_OK` - No errors with input parameters *(see the return value of `outbitconsensus_verify_script` for the verification status)*
- `outbitconsensus_ERR_TX_INDEX` - An invalid index for `txTo`
- `outbitconsensus_ERR_TX_SIZE_MISMATCH` - `txToLen` did not match with the size of `txTo`
- `outbitconsensus_ERR_DESERIALIZE` - An error deserializing `txTo`

### Example Implementations
- [NOutbit](https://github.com/NicolasDorier/NOutbit/blob/master/NOutbit/Script.cs#L814) (.NET Bindings)
- [node-liboutbitconsensus](https://github.com/bitpay/node-liboutbitconsensus) (Node.js Bindings)
- [java-liboutbitconsensus](https://github.com/dexX7/java-liboutbitconsensus) (Java Bindings)
- [outbitconsensus-php](https://github.com/Bit-Wasp/outbitconsensus-php) (PHP Bindings)
