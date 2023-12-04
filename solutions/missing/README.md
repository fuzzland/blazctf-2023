```solidity
contract A {
    bool public isSolved;

    function execute_44g58pv() public {
        assembly {
            let s := gas()
            pop(call(s, caller(), 0, 0, 0, 0, 0x20))
            for { let i := exp(0x02, 0x02) } slt(i, extcodesize(caller())) { i := add(i, 0x02) } {
                let l := mload(shr(0x02, call(gas(), caller(), 0, 0, 0, 0x20, 0x20)))
                switch lt(l, mload(0x20))
                case 0 {
                    mstore(mul(0x20, 0x02), l)
                    mstore(0, keccak256(0x20, mul(0x20, 0x02)))
                }
                default { mstore(0, keccak256(0x0, mul(0x20, 0x02))) }
            }
            if eq(mload(0), 0x58898ce26697138ee057566d1fcfbcf1384f625d0aa51e80fbc9c44e6cd8a658) { sstore(0, 1) }
            if gt(sub(s, gas()), 0x60ff) { sstore(0, 0) }
        }
    }
}
```


Challenge Desc:

MerkleTree + EIP1153(TLOAD/TSTORE) + Bytecode + MinimizeContract
https://eips.ethereum.org/EIPS/eip-1153

Deploy:
```
anvil --hardfork cancun
forge create src/Chaotic\ Merkel/Challenge.sol:ChallengeChaoticMerkel --private-key=0xac0974bec39a17e36ba4a6b4d238ff944bacb478cbed5efcae784d7bf4f2ff80
```

Quick Solution:
```
mv script/exploit/ChaoticMerkel.t.solution script/exploit/ChaoticMerkel.t.sol
forge create script/exploit/ChaoticMerkel.t.sol:Solve --private-key=0xac0974bec39a17e36ba4a6b4d238ff944bacb478cbed5efcae784d7bf4f2ff80 --use=./script/exploit/solc-osx
cast send 0xe7f1725E7734CE288F8367e1Bb143E90bb3F0512 "test()"  --private-key=0xac0974bec39a17e36ba4a6b4d238ff944bacb478cbed5efcae784d7bf4f2ff80  --gas-limit=100000

mv script/exploit/ChaoticMerkel.t.sol script/exploit/ChaoticMerkel.t.solution
```


```
Tree
└─ 58898ce26697138ee057566d1fcfbcf1384f625d0aa51e80fbc9c44e6cd8a658
   ├─ e4675068ce90f260cb4fcf35a183cbc76171f5a54e8f0227199878fbe7d92420
   │  ├─ 89410fa1369af97e6d8f3f34d8e46fb278b830f554aa1cceb226fa96e7b42661
   │  │  ├─ 344c26d486fdf6ec156cf0356ebc4286a1162809d0af1736bc9b94da17a369f9
   │  │  │  ├─ a6efd28b29323876b14c71d011841fc6a68a6c900d1d278e25e86b2a1896d5ee
   │  │  │  └─ 309f21ff97e38c7d8c5435c8f7980b25c4b1c4720c9ca18b4419d70dd02d2641
   │  │  └─ 962691749e63af958b7a571dceee79d1bc9c27bb30bcc586e9d7f1950024c337
   │  │     ├─ 61687eafa2fc96f232706c6f8f8f1320eb1259d5d129aaae8c3842a533f1d8e4
   │  │     └─ 77164b80976674ed02afec618b973626fd5d305c6df150b1041d42e07537f4df
   │  └─ f6c39642dc23bca6d853683397ab330df6795246e813dd714bcc96239beb7c28
   │     ├─ bf0cd4820c8b7e2a3021b9e7b9799d7a99fe18427df17415a860e6c7efb24b77
   │     │  ├─ 263cf0996038b75ef2e66972d9a9da0df5eacf9c535d5ef7c7ef649e39c32f49
   │     │  └─ cd4c235f63bc1d560c1b4389e79a5901732c059a0717d1ed848e9c5914fefaf5
   │     └─ 4d15312b8a4c82ea92bbc08bd814e1397a2ae757f975d511ce65708b2901e9c6
   │        ├─ b972f768b362ed9455583e4efbe8c130c3904e1b9be59042e0e62b754417d879
   │        └─ 5f117b6de2e735c498063fa0edd0c2d56e9d8dc8308fbb3c3d510719ceab6acc
   └─ 4ce73a72117cd9cbe0f9f8d3c026b29ce62245a2b8eb21b370d0286e77bf14ef
      ├─ fe5f0039b8516a9a3b620a38933ee9837501b845954ab1a52a876a41d28c853b
      │  ├─ 74867514c11dc7a9215547d6ab476c7b7c62a7cc30bbb036788ceaadbe76e320
      │  │  ├─ fcdd6194e30d12c1f1a621e13862cb9c19160a96e16358b9140650b3dd54c98c
      │  │  └─ 803511394c6f5151454880286edf5b3bf23c886f7e752818c91e5379c8edba5a
      │  └─ 730239b21a857fa6df9e821db8779a908f5eaf9cc1291dd46bc2b0659a2a00d1
      │     ├─ 5632a0f9cec4ce6c1bdcd6460755a39271f4634db0789f952386aca40e678109
      │     └─ 13d1d79d8db70d67fd01bddb4c8ec7691ef778bde4e83ae3ae7a64f242c8f32d
      └─ c30e7c0611d9b5dfdd41146cd1c147c6d392cd9ba5ac6702a7d747e3b9eaf987
         ├─ 5b2f402f04b16271d6f18f161cd4c9ad7ed71ae608fcd112558881821983b9e0
         │  ├─ 43ea48de38f08fa69bff7210795531fb1029b423d89ed03ae5de0963084c9b2a
         │  └─ 7c7e9d49ca739c8eaf851802a24e95eb34d709e465dde42554948796d5670656
         └─ ed87b3ce8af5033afa44e5dc4933f0cb31a289006b013a9f875d7d4fd2736706
            ├─ 533312f6ef3c646155645c03f2099e16c9b243cfcf3592ae8334ea49cfc5b213
            └─ 01969e3b34fb58274a33cdf37bab8173c2681aaefd1010ae9c6076e45424ac65
```

ipfs:
```
npm install multihashes

function hexToUint8Array(hexString) {
  if (hexString.length % 2 !== 0) {
    console.log('Warning: the hex string has an odd number of characters');
    hexString = '0' + hexString;
  }

  var bytes = new Uint8Array(Math.ceil(hexString.length / 2));

  for (let i = 0; i < bytes.length; i++)
    bytes[i] = parseInt(hexString.substr(i * 2, 2), 16);

  return bytes;
}

function uint8ArrayToHex(bytes) {
    let hex = '';
    for(let i=0; i<bytes.length; i++) {
        let current = bytes[i].toString(16);
        if(current.length == 1) {
            current = '0' + current;
        }
        hex += current;
    }
    return hex;
}

 var multihash = require('multihashes')
 let hexString = "12207a0964c9fb7e33d9e5fb6dc6c17d84280dbbfabeb4429f2206529aca0a651222"
 let encoded = multihash.toB58String(hexToUint8Array(hexString))
'QmWZ2kq9CfgKHkXYghaeKM2mcYZxsZP2ibrgXkPK6ivjk5'

uint8ArrayToHex(multihash.fromB58String(encoded))
'12207a0964c9fb7e33d9e5fb6dc6c17d84280dbbfabeb4429f2206529aca0a651222'
```


