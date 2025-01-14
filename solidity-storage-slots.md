### Storage slots in Solidity

**Why do we care?** Because many smart contracts are upgradeable or make delegate calls, and if slots are mismanaged, they may get overridden or cause certain calls to access the incorrect variable. 
- The EVM stores values in "slots" of 32 bytes (256 bits)
- The solidity compiler will read these values from raw memory, and then cast them to the correct types. It's still possible to access a "bytes32" slot as a "string" or an "int128" value, the compiler may just yell if you try to do this. But with some trickery (for example, using assembly) it is possible, and more importantly, if the compiler incorrectly thinks a variable is the wrong type (like after a botched upgrade), it will run with it and cast the storage slot to the assumed type.
- Almost all slots are assigned in ascending order (first assigning slot 0, then slot 1, and so forth), so the first few slots are where the majority of storage mismatch issues will happen

[Solidity Docs - Layout of State Variables in Storage](https://docs.soliditylang.org/en/latest/internals/layout_in_storage.html#layout-of-state-variables-in-storage)

### Slot packing

- Sometimes if variables are small enough in length, the compiler will pack them together. There are exceptions, for example that structs and arrays will always occupy a new slot:
> For each variable, a size in bytes is determined according to its type. Multiple, contiguous items that need less than 32 bytes are packed into a single storage slot if possible, according to the following rules:
> - The first item in a storage slot is stored lower-order aligned.
> - Value types use only as many bytes as are necessary to store them.
> - If a value type does not fit the remaining part of a storage slot, it is stored in the next storage slot.
> - Structs and array data always start a new slot and their items are packed tightly according to these rules.
> - Items following struct or array data always start a new storage slot.

_copied shamelessly from the [solidity docs](https://docs.soliditylang.org/en/latest/internals/layout_in_storage.html#layout-of-state-variables-in-storage)_

### Types

- **mappings**: Store their values at a "random" slot via hashing. **The mapping declaration itself will "occupy" one slot** which is left blank, and then that slot will be used to "salt" the mapping key you're requesting to get it's slot.
  - if `exampleMapping` is declared as the first variable, it's at slot `0`. The slot for `exampleMapping[42069]`, it's at slot `keccak256(abi.encode(42069,0)`, where the `0` comes from `exampleMapping`'s slot
    - See [this image](https://miro.medium.com/max/1400/1*YKIFfJIaAlHpPrtPMXeCbA.png) from [this medium post](https://medium.com/coinmonks/solidity-tutorial-all-about-mappings-29a12269ee14) 
  - mapping **declarations** consume one full slot in memory (and then one more for every element in the mapping, but because those slots are hashes they are highly unlikely to ever have collisions. We can say it's impossible™️)
- **Dynamic arrays**: Store their values similarly to mappings (see above), with one key difference - instead of each element being stored at a "random" slot (based on hashing), the first element is stored at a hash, then following elements in the array are stored at the next hash
  - for `exampleDynArray` at slot `1`, the slot of value `exampleDynArray[0]` is `keccak(1)` (since it is at slot 1). Then, the slot of `exampleDynArray[n]` is at `keccak(1)+n`.
  - If the values are less than or equal to 16 bytes in my personal noteslength, they may share storage slots
    - 16 bytes is because we can't fit more than one of anything longer than 16 bytes in a single storage slot. The solidity compiler won't try to break up a single value across multiple storage slots, it will just leave the unused portions of the slots blank (zeroes)

### Inheritance

- When a contract inherits another contract, the first storage slots are occupied by the base-most contract's storage slots, then the next base-most contract occupies the following slots and so on. 
  - So, the base contract may get storage slots 0, 1, and 2, then the next contract up the inheritance tree gets storage slots starting with 3, and so on.
- "base-most-ness" is determined by the [C3 linearization order](https://en.wikipedia.org/wiki/C3_linearization) of the contract.

### Check your storage slots

If you are using OpenZeppelin's [upgrades plugin for hardhat](https://www.npmjs.com/package/@openzeppelin/hardhat-upgrades), you can verify that your proxy upgrade will preserve correct storage by attempting an upgrade using `upgradeProxy` or just run the validations with `validateUpgrade`. If a storage gap is not being reduced properly, you will see an error message indicating the expected size of the storage gap.

Alternatively, you can manually check your storage slots using `hardhat-storage-layout`,

0. Setup a hardhat project for your solidity code.
1. Download [`hardhat-storage-layout` plugin](https://www.npmjs.com/package/hardhat-storage-layout) by running `npm install hardhat-storage-layout` or `yarn add --dev hardhat-storage-layout`  in your project repo
2. Put this line in the top of your hardhat.config.js: `require('hardhat-storage-layout');`
3. Run `npx hardhat compile`. Make sure your contract actually compile before moving on to next step.  
5. Run `npx hardhat check` or `yarn hardhat check`. The storage layout of every contract should be displayed
6. **Note: to check changes to contract storage**, you will need to recompile them and then run `npx hardhat check` again.

#### Assembly `.slot` method

You can also check the storage slot of an object by using the assembly method `.slot`. [I didn't read this but here's an article about it](https://dev.to/web3_ruud/advance-soliditymastering-storage-slot-c38). 

### Resources:

- ["All About Solidity Data Locations — Storage" by Jean Cvllr](https://betterprogramming.pub/all-about-solidity-data-locations-part-i-storage-e50604bfc1ad)
- ["Ethereum In depth" by OpenZeppelin](https://blog.openzeppelin.com/ethereum-in-depth-part-1-968981e6f833/) - check out all 7 parts!
- ["Writing Upgradeable Contracts" from the OpenZeppelin Docs](https://docs.openzeppelin.com/upgrades-plugins/1.x/writing-upgradeable) - Good explanation of how to manage storage slots within a contract meant to be upgraded
