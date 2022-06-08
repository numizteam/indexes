# Indexes
Contracts for [TIP4.3](https://github.com/everscale-org/docs/blob/main/src/standard/TIP-4/3.md).
Compiled by [TON-Solidity-Compiler](https://github.com/tonlabs/TON-Solidity-Compiler) `v0.58.2` and [TVM-linker](https://github.com/tonlabs/TVM-linker) `v0.14.51`

### Example of `IndexBasis` deployment
```solidity
function deployIndexBasis(TvmCell codeIndex, address collection, uint128 value) private pure {
    string stamp = "nft";
    TvmBuilder salt;
    salt.store(stamp);
    TvmCell code = tvm.setCodeSalt(codeIndex, salt.toCell());
    TvmCell stateInit = tvm.buildStateInit({
        contr: IndexBasis,
        varInit: {_collection: collection},
        code: code
    });
    new IndexBasis{stateInit: stateInit, value: value}();
}
```

### Example of `Index` deployment
```solidity
function deployIndex(TvmCell codeIndex, address nft, address collection, address owner, uint128 value) private pure {
    string stamp = "nft";
    TvmBuilder salt;
    salt.store(stamp, collection, owner);
    TvmCell code = tvm.setCodeSalt(codeIndex, salt.toCell());
    TvmCell stateInit = tvm.buildStateInit({
        contr: Index,
        varInit: {_nft: nft},
        code: code
    });
    new Index{stateInit: stateInit, value: value}();
}
```