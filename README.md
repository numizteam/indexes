# Indexes
Contracts for [TIP4.3](https://github.com/everscale-org/docs/blob/main/src/Standard/TIP-4/3.md)
Compiled by [TVMCompiler](https://github.com/tonlabs/TON-Solidity-Compiler/tree/a222452e27aacff14fdf2fff356542843a2a8d1c) `v0.58.2` and [TVM-linker](https://github.com/tonlabs/TVM-linker/tree/740f9f62a4e68c9f515667c109b116f265942d72) `v0.14.51`

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