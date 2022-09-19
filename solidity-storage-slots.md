### Storage slots in Solidity

**Why do we care?** Because many smart contracts are upgradeable or make delegate calls, and if slots are mismanaged, they may get overridden or cause certain calls to access the incorrect variable. 
- The EVM stores values in "slots" of 32 bytes (256 bits)
- The solidity compiler will read these values and cast them to the correct types. Keep in mind, it's still possible to access a "bytes32" slot as a "string" or an "int128" value. The compile may just yell if you try to do this without some trickery. But with trickery it is possible
- Almost all slots are assigned in ascending order (first assigning slot 0, then slot 1, and so forth), so the first few slots are where the majority of storage mismatch issues will happen

### Types

- **mappings**: Store their values at a "random" slot via hashing. The mapping declaration itself will "occupy" one slot which is left blank, and then that slot will be used to "salt" the mapping key you're requesting to get it's slot.
  - if `exampleMapping` is declared as the first variable, it's at slot `0`. The slot for `exampleMapping[42069]`, it's at slot `keccak256(abi.encode(42069,0)`, where the `0` comes from `exampleMapping`'s slot
    - See [this image](https://miro.medium.com/max/1400/1*YKIFfJIaAlHpPrtPMXeCbA.png) from [this medium post](https://medium.com/coinmonks/solidity-tutorial-all-about-mappings-29a12269ee14) 
