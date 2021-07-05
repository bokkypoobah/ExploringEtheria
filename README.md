# ExploringEtheria

See https://bokkypoobah.github.io/ExploringEtheria/.

Exploring [https://etheria.world/](https://etheria.world/). Not affiliated with this project.

<br />

## Etheria Info

GitHub - [https://github.com/cyrusadkisson/etheria/tree/master/contracts](https://github.com/cyrusadkisson/etheria/tree/master/contracts).

Main contracts, copies stored in [other_contracts/](other_contracts/):

* [etheria-1pt2.sol](https://github.com/cyrusadkisson/etheria/blob/master/contracts/etheria-1pt2.sol) deployed to [0xB21f8684f23Dbb1008508B4DE91a0aaEDEbdB7E4](https://etherscan.io/address/0xB21f8684f23Dbb1008508B4DE91a0aaEDEbdB7E4#code) on [Nov-01-2015 01:20:11 AM +UTC](https://etherscan.io/tx/0x572afc6344a779345a57fba7355c9c26b221c1039fa46fd3d5dce180a4e82108)
* [etheria_BlockDefStorage.sol](https://github.com/cyrusadkisson/etheria/blob/master/contracts/etheria_BlockDefStorage.sol) deployed to [0xd4E686A1FBf1Bfe058510f07Cd3936D3D5A70589](https://etherscan.io/address/0xd4e686a1fbf1bfe058510f07cd3936d3d5a70589#code) on [Oct-29-2015 07:04:15 PM +UTC](https://etherscan.io/tx/0x485e7d332f47205a7aaa9768d1b0eb9140fe59d526d349f4425979ed3fc63622)
* [etheria_MapElevationStorage.sol](https://github.com/cyrusadkisson/etheria/blob/master/contracts/etheria_MapElevationStorage.sol) deployed to [0x68549D7Dbb7A956f955Ec1263F55494f05972A6b](https://etherscan.io/address/0x68549D7Dbb7A956f955Ec1263F55494f05972A6b#code) on [Oct-18-2015 07:18:20 PM +UTC](https://etherscan.io/tx/0x48a0c0eb350eba296e43d99a5f3c4394aa2a5da69e5369a58076f40fd32c9c99)
* [EtheriaExchangeV1pt1.sol](https://github.com/cyrusadkisson/etheria/blob/master/contracts/EtheriaExchangeV1pt1.sol) deployed to [0x4f0D14176b396bB4fbdBaB07Ec8f60f1a4204793](https://etherscan.io/address/0x4f0D14176b396bB4fbdBaB07Ec8f60f1a4204793#code) on [Apr-21-2021 05:13:31 AM +UTC](https://etherscan.io/tx/0x2049fe7f7b9cc5b52de88a2434feac62aabb8ad48e86c72e9fb2e99262bcc66b)
* [EtheriaExchangeV1pt2.sol](https://github.com/cyrusadkisson/etheria/blob/master/contracts/EtheriaExchangeV1pt2.sol) deployed to [0x8e5f807e30c7079f835f6b17a3aa320444c66c44](https://etherscan.io/address/0x8e5f807e30c7079f835f6b17a3aa320444c66c44#code) on [Apr-21-2021 05:16:47 AM +UTC](https://etherscan.io/tx/0x33f494d31d7ee220471a188beeda8738d900fa25f90251112b7ee9cc2d5cb629)

<br />

## EtheriaHelper

Deployed to [0x7d0cba86128957633156fbff6a88d9a278ef32e2](https://etherscan.io/address/0x7d0cba86128957633156fbff6a88d9a278ef32e2#code) to query data via web3 in a batches of 33 x 33 = 1,089 records:

```javascript
/**
 *Submitted for verification at Etherscan.io on 2021-07-05
*/

pragma solidity ^0.8.0;

// ----------------------------------------------------------------------------
// Etheria Helper v0.9.0
//
// https://github.com/bokkypoobah/TokenToolz
//
// Deployed to 0x7d0cBA86128957633156FBFF6A88D9A278eF32e2
//
// SPDX-License-Identifier: MIT
//
// Enjoy.
//
// (c) BokkyPooBah / Bok Consulting Pty Ltd 2021. The MIT Licence.
// ----------------------------------------------------------------------------

interface IEtheria {
    function getOwner(uint8 col, uint8 row) external view returns(address);
    function getName(uint8 col, uint8 row) external view returns(string memory);
    function getStatus(uint8 col, uint8 row) external view returns(string memory);
    function getLastFarm(uint8 col, uint8 row) external view returns (uint);
    // function getBlocks(uint8 col, uint8 row) external view returns (int8[5][] memory);
}

contract EtheriaHelper {

    uint private constant SIZE = 33;

    IEtheria public constant etheria = IEtheria(0xB21f8684f23Dbb1008508B4DE91a0aaEDEbdB7E4);

    function owners() external view returns(address[] memory ) {
        address[] memory result = new address[](SIZE * SIZE);
        for (uint8 row = 0; row < SIZE; row++) {
            for (uint8 col = 0; col < SIZE; col++) {
                result[row * SIZE + col] = etheria.getOwner(col, row);
            }
        }
        return result;
    }

    function names() external view returns(string[] memory ) {
        string[] memory result = new string[](SIZE * SIZE);
        for (uint8 row = 0; row < SIZE; row++) {
            for (uint8 col = 0; col < SIZE; col++) {
                result[row * SIZE + col] = etheria.getName(col, row);
            }
        }
        return result;
    }

    function statuses() external view returns(string[] memory ) {
        string[] memory result = new string[](SIZE * SIZE);
        for (uint8 row = 0; row < SIZE; row++) {
            for (uint8 col = 0; col < SIZE; col++) {
                result[row * SIZE + col] = etheria.getStatus(col, row);
            }
        }
        return result;
    }

    function lastFarms() external view returns(uint[] memory ) {
        uint[] memory result = new uint[](SIZE * SIZE);
        for (uint8 row = 0; row < SIZE; row++) {
            for (uint8 col = 0; col < SIZE; col++) {
                result[row * SIZE + col] = etheria.getLastFarm(col, row);
            }
        }
        return result;
    }
}
```

<br />

<br />

Enjoy!

(c) BokkyPooBah / Bok Consulting Pty Ltd - Jul 2021. The MIT Licence.
