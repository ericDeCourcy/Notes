### Storage slots in Solidity

**Why do we care?** Because many smart contracts are upgradeable or make delegate calls, and if slots are mismanaged, they may get overridden or cause certain calls to access the incorrect variable. 
- The EVM stores values in "slots" of 32 bytes (256 bits)
- The solidity compiler will read these values and cast them to the correct types. Keep in mind, it's still possible to access a "bytes32" slot as a "string" or an "int128" value. The compile may just yell if you try to do this without some trickery. But with trickery it is possible
- Almost all slots are assigned in ascending order (first assigning slot 0, then slot 1, and so forth), so the first few slots are where the majority of storage mismatch issues will happen

[Solidity Docs - Layout of State Variables in Storage](https://docs.soliditylang.org/en/latest/internals/layout_in_storage.html#layout-of-state-variables-in-storage)

### Types

- **mappings**: Store their values at a "random" slot via hashing. The mapping declaration itself will "occupy" one slot which is left blank, and then that slot will be used to "salt" the mapping key you're requesting to get it's slot.
  - if `exampleMapping` is declared as the first variable, it's at slot `0`. The slot for `exampleMapping[42069]`, it's at slot `keccak256(abi.encode(42069,0)`, where the `0` comes from `exampleMapping`'s slot
    - See [this image](https://miro.medium.com/max/1400/1*YKIFfJIaAlHpPrtPMXeCbA.png) from [this medium post](https://medium.com/coinmonks/solidity-tutorial-all-about-mappings-29a12269ee14) 
  - **mapping declarations consume one full slot in memory** (and then some more, but because those are hashes they are highly unlikely to ever have collisions. We can say it's impossible™️)
- **Dynamic arrays**: Store their values similarly to mappings (see above), with one key difference - instead of each element being stored at a "random" slot (based on hashing), the first element is stored at a hash, then following elements in the array are stored at the next hash
  - for `exampleDynArray` at slot `1`, the slot of value `exampleDynArray[0]` is `keccak(1)` (since it is at slot 1). Then, the slot of `exampleDynArray[n]` is at `keccak(1)+n`.
  - If the values are less than 16 bytes in length, they may share storage slots

### Inheritance

- When a contract inherits another contract, the first storage slots are occupied by the base-most contract's storage slots, then the next base-most contract occupies the following slots and so on. 
  - So, the base contract may get storage slots 0, 1, and 2, then the next contract up the inheritance tree gets storage slots starting with 3, and so on.
- "base-most-ness" is determined by the C3 linearization order of the contract.

### Resources:

- ["All About Solidity Data Locations — Storage" by Jean Cvllr](https://betterprogramming.pub/all-about-solidity-data-locations-part-i-storage-e50604bfc1ad)
- ["Ethereum In depth" by OpenZeppelin](https://blog.openzeppelin.com/ethereum-in-depth-part-1-968981e6f833/) - check out all 7 parts!
