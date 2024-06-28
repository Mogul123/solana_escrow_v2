# escrow-scripts

scripts that can be used to interact with an [escrow-program](https://github.com/paul-schaaf/solana-escrow)


## Commands

All available commands can be found in the `package.json` file. Start by going into your escrow program repo and building your program with
```
cargo build-bpf
```
This command will output the location of your executable (ending with `.so`). Copy it and execute the following script from this repo to start up the validator you'll need for the other scripts.
```
npm run setup-validator <EXECUTABLE_LOCATION>
```

If you need to call `solana-test-validator` from a specific folder, go into that folder and execute the following command instead. Note that the `r` flag will reset the validator if there was a validator started in that folder before.
```
./solana-test-validator -r --mint E2F3fsS1HpsLb2VpEgsA5ztfo83CWFWW4jWpC6FvJ6qR --bpf-program 4yBTZXsuz7c1X3PJF4PPCJr8G6HnNAgRvzAWVoFZMncH <EXECUTABLE_LOCATION>
```

Now, in another tab, you can start executing the scripts to interact with your escrow program. There are three scripts: `setup`, `alice`, and `bob`. `setup` initializes SOL accounts as well as the necessary token accounts for Alice and Bob. `alice` executes Alice's transaction and `bob` executes Bob's transaction. Start by installing the necessary dependencies.
```
npm install
```

You can then run the following command to setup and run the two transactions.
```
npm run all
```
But you don't have to execute all three at once. For example, you can run
```
npm run setup-alice
```
to run everything up to bob's transaction. See the `package.json` file for more.



## Logging compute costs
Since there is not package / tool that tracks the consumed compute units when need to find those in the logs of the solana validator.
For this run in a new tab after executing `npm run all`
```solana logs --url localhost
```

### Extracting compute units out of the logs
Use the following regex: `consumed (\d+) of` to extract the compute units.
You can use e.g. https://regex101.com. Then extract the matches found and paste them into an excel to sum up the compute units

**Output from regeex matching**
```
match,group,is_participating,start,end,content
1,1,yes,1322,1326,2919
2,1,yes,1869,1873,4500
3,1,yes,2416,2420,4500
4,1,yes,2843,2847,4491
5,1,yes,3387,3391,2919
6,1,yes,3933,3937,4500
7,1,yes,4480,4484,4500
8,1,yes,4907,4911,4491
9,1,yes,5454,5458,4498
10,1,yes,5718,5722,4643
11,1,yes,6286,6290,2875
12,1,yes,6445,6449,8481
13,1,yes,7075,7079,4728
14,1,yes,7417,7421,4728
15,1,yes,7759,7763,3098
16,1,yes,7965,7970,23373
```


**Solana Log Expected output:**

```
Streaming transaction logs. Confirmed commitment
Transaction executed in slot 177:
  Signature: 4hAR7dkexPuJyxo9SDVPZM8Mui3Re76VGW7tiQtdq5L3NMhacVNGocGbAepjtaGymGGy7SFwa3QZsAQaZuhp2ZGF
  Status: Ok
  Log Messages:
    Program 11111111111111111111111111111111 invoke [1]
    Program 11111111111111111111111111111111 success
Transaction executed in slot 177:
  Signature: 5CFahPcygohbvupZNAyM4b13QZ3bEfm1hXYweJHESJE8XtLrD6sRtmbm52Fnro1GY4J1y1EmsRHxCo6YQhQ5vybC
  Status: Ok
  Log Messages:
    Program 11111111111111111111111111111111 invoke [1]
    Program 11111111111111111111111111111111 success
Transaction executed in slot 177:
  Signature: 5RgZ5gr7LC7X9diMzmcfSDfy54DyHt8wQBfXboeryapca56tfA1KoxFhnKUBxcunXJtfrUj9Yt1vZGDbJkgBykzE
  Status: Ok
  Log Messages:
    Program 11111111111111111111111111111111 invoke [1]
    Program 11111111111111111111111111111111 success
Transaction executed in slot 177:
  Signature: 3SwAT5gkMfh36nW7SxS3bKsPo8GHMNkaaNwJRkvcBhKmUjudRzTckdopM9j4MrFQuLucHDWhgvhx11mBneudAZ3n
  Status: Ok
  Log Messages:
    Program 11111111111111111111111111111111 invoke [1]
    Program 11111111111111111111111111111111 success
    Program TokenkegQfeZyiNwAJbNbGKPFXCWuBvf9Ss623VQ5DA invoke [1]
    Program log: Instruction: InitializeMint
    Program TokenkegQfeZyiNwAJbNbGKPFXCWuBvf9Ss623VQ5DA consumed 2919 of 399850 compute units
    Program TokenkegQfeZyiNwAJbNbGKPFXCWuBvf9Ss623VQ5DA success
Transaction executed in slot 178:
  Signature: 4z2NJiFcYDBrcLr86amswh1dZw96z9LPSExgiJpETqXEZFW2f4cUi6MbTGXYmsqmtgyZeJw9QCVcNSUsjz2WJFb1
  Status: Ok
  Log Messages:
    Program 11111111111111111111111111111111 invoke [1]
    Program 11111111111111111111111111111111 success
    Program TokenkegQfeZyiNwAJbNbGKPFXCWuBvf9Ss623VQ5DA invoke [1]
    Program log: Instruction: InitializeAccount
    Program TokenkegQfeZyiNwAJbNbGKPFXCWuBvf9Ss623VQ5DA consumed 4500 of 399850 compute units
    Program TokenkegQfeZyiNwAJbNbGKPFXCWuBvf9Ss623VQ5DA success
Transaction executed in slot 179:
  Signature: 4nGBhrodDquVpMEmoFqZFde8y5cp14RKzfDvDqPYnjPzJXUbuSLjJooC7ZNkjk1yx8dSni8Q4XZJ8oTjfNnMv1U6
  Status: Ok
  Log Messages:
    Program 11111111111111111111111111111111 invoke [1]
    Program 11111111111111111111111111111111 success
    Program TokenkegQfeZyiNwAJbNbGKPFXCWuBvf9Ss623VQ5DA invoke [1]
    Program log: Instruction: InitializeAccount
    Program TokenkegQfeZyiNwAJbNbGKPFXCWuBvf9Ss623VQ5DA consumed 4500 of 399850 compute units
    Program TokenkegQfeZyiNwAJbNbGKPFXCWuBvf9Ss623VQ5DA success
Transaction executed in slot 180:
  Signature: 4sEKNAMaNQvrXgMrkdA6fBG78a9n24u9pV9oWnBUUUXii3kzaGsBK8opTDFZzP3bxqo5UGkR7ySySbMHq41Kvcug
  Status: Ok
  Log Messages:
    Program TokenkegQfeZyiNwAJbNbGKPFXCWuBvf9Ss623VQ5DA invoke [1]
    Program log: Instruction: MintTo
    Program TokenkegQfeZyiNwAJbNbGKPFXCWuBvf9Ss623VQ5DA consumed 4491 of 200000 compute units
    Program TokenkegQfeZyiNwAJbNbGKPFXCWuBvf9Ss623VQ5DA success
Transaction executed in slot 181:
  Signature: 4ghYySe5sCXGAqaAirHQEVpKs82an935wJTmtUsEmmbVWMAdYzxpmPzBaJ5x96t13iemYyyZNzJvAy76adHi5ERM
  Status: Ok
  Log Messages:
    Program 11111111111111111111111111111111 invoke [1]
    Program 11111111111111111111111111111111 success
    Program TokenkegQfeZyiNwAJbNbGKPFXCWuBvf9Ss623VQ5DA invoke [1]
    Program log: Instruction: InitializeMint
    Program TokenkegQfeZyiNwAJbNbGKPFXCWuBvf9Ss623VQ5DA consumed 2919 of 399850 compute units
    Program TokenkegQfeZyiNwAJbNbGKPFXCWuBvf9Ss623VQ5DA success
Transaction executed in slot 182:
  Signature: HTwdcV3d1dWm8pbtzUL3xr3SuEyJe96VZ3UduKopd3HJKsyXknW9UcQvc6Mveq4wMPNQb3fseaSYTT31PxRvMej
  Status: Ok
  Log Messages:
    Program 11111111111111111111111111111111 invoke [1]
    Program 11111111111111111111111111111111 success
    Program TokenkegQfeZyiNwAJbNbGKPFXCWuBvf9Ss623VQ5DA invoke [1]
    Program log: Instruction: InitializeAccount
    Program TokenkegQfeZyiNwAJbNbGKPFXCWuBvf9Ss623VQ5DA consumed 4500 of 399850 compute units
    Program TokenkegQfeZyiNwAJbNbGKPFXCWuBvf9Ss623VQ5DA success
Transaction executed in slot 183:
  Signature: 3ycYVJ8tabwUyXbGSUg3iyozmWaUV41WGq2NT1uWwbnWDrLs3w2rDHzSj5RJpsRfrykrps3spttizUq2N4RsTs7z
  Status: Ok
  Log Messages:
    Program 11111111111111111111111111111111 invoke [1]
    Program 11111111111111111111111111111111 success
    Program TokenkegQfeZyiNwAJbNbGKPFXCWuBvf9Ss623VQ5DA invoke [1]
    Program log: Instruction: InitializeAccount
    Program TokenkegQfeZyiNwAJbNbGKPFXCWuBvf9Ss623VQ5DA consumed 4500 of 399850 compute units
    Program TokenkegQfeZyiNwAJbNbGKPFXCWuBvf9Ss623VQ5DA success
Transaction executed in slot 184:
  Signature: 5V8HeyqBdKnDECvoJDvDkjMpNDqEpxpbJUp3gpP3oTaKHrLWG6LzDkXRp7d5wPkqpbakmdisyBdBa73q6keXdxG9
  Status: Ok
  Log Messages:
    Program TokenkegQfeZyiNwAJbNbGKPFXCWuBvf9Ss623VQ5DA invoke [1]
    Program log: Instruction: MintTo
    Program TokenkegQfeZyiNwAJbNbGKPFXCWuBvf9Ss623VQ5DA consumed 4491 of 200000 compute units
    Program TokenkegQfeZyiNwAJbNbGKPFXCWuBvf9Ss623VQ5DA success
Transaction executed in slot 196:
  Signature: 4yweXAt7Kx2Fw4NHkCe9Rb1163SVHdj6cCBEd5zZswj4XLGD8c9SGhSBYg7wmsiyDuKhMo7bRG3NBCJFbxUSWf5N
  Status: Ok
  Log Messages:
    Program 11111111111111111111111111111111 invoke [1]
    Program 11111111111111111111111111111111 success
    Program TokenkegQfeZyiNwAJbNbGKPFXCWuBvf9Ss623VQ5DA invoke [1]
    Program log: Instruction: InitializeAccount
    Program TokenkegQfeZyiNwAJbNbGKPFXCWuBvf9Ss623VQ5DA consumed 4498 of 999850 compute units
    Program TokenkegQfeZyiNwAJbNbGKPFXCWuBvf9Ss623VQ5DA success
    Program TokenkegQfeZyiNwAJbNbGKPFXCWuBvf9Ss623VQ5DA invoke [1]
    Program log: Instruction: Transfer
    Program TokenkegQfeZyiNwAJbNbGKPFXCWuBvf9Ss623VQ5DA consumed 4643 of 995352 compute units
    Program TokenkegQfeZyiNwAJbNbGKPFXCWuBvf9Ss623VQ5DA success
    Program 11111111111111111111111111111111 invoke [1]
    Program 11111111111111111111111111111111 success
    Program 4yBTZXsuz7c1X3PJF4PPCJr8G6HnNAgRvzAWVoFZMncH invoke [1]
    Program log: Instruction: InitEscrow
    Program log: Calling the token program to transfer token account ownership...
    Program TokenkegQfeZyiNwAJbNbGKPFXCWuBvf9Ss623VQ5DA invoke [2]
    Program log: Instruction: SetAuthority
    Program TokenkegQfeZyiNwAJbNbGKPFXCWuBvf9Ss623VQ5DA consumed 2875 of 985138 compute units
    Program TokenkegQfeZyiNwAJbNbGKPFXCWuBvf9Ss623VQ5DA success
    Program 4yBTZXsuz7c1X3PJF4PPCJr8G6HnNAgRvzAWVoFZMncH consumed 8481 of 990559 compute units
    Program 4yBTZXsuz7c1X3PJF4PPCJr8G6HnNAgRvzAWVoFZMncH success
Transaction executed in slot 209:
  Signature: 2hVv7obozD8SD37i8TjsJZgscAcmvmcuep3w75kMdL8XhVCQXThJodkiGfqbMa8wb9n86MGiGgssinNRyqvbnYFt
  Status: Ok
  Log Messages:
    Program 4yBTZXsuz7c1X3PJF4PPCJr8G6HnNAgRvzAWVoFZMncH invoke [1]
    Program log: Instruction: Exchange
    Program log: Calling the token program to transfer tokens to the escrow's initializer...
    Program TokenkegQfeZyiNwAJbNbGKPFXCWuBvf9Ss623VQ5DA invoke [2]
    Program log: Instruction: Transfer
    Program TokenkegQfeZyiNwAJbNbGKPFXCWuBvf9Ss623VQ5DA consumed 4728 of 194192 compute units
    Program TokenkegQfeZyiNwAJbNbGKPFXCWuBvf9Ss623VQ5DA success
    Program log: Calling the token program to transfer tokens to the taker...
    Program TokenkegQfeZyiNwAJbNbGKPFXCWuBvf9Ss623VQ5DA invoke [2]
    Program log: Instruction: Transfer
    Program TokenkegQfeZyiNwAJbNbGKPFXCWuBvf9Ss623VQ5DA consumed 4728 of 187168 compute units
    Program TokenkegQfeZyiNwAJbNbGKPFXCWuBvf9Ss623VQ5DA success
    Program log: Calling the token program to close pda's temp account...
    Program TokenkegQfeZyiNwAJbNbGKPFXCWuBvf9Ss623VQ5DA invoke [2]
    Program log: Instruction: CloseAccount
    Program TokenkegQfeZyiNwAJbNbGKPFXCWuBvf9Ss623VQ5DA consumed 3098 of 180203 compute units
    Program TokenkegQfeZyiNwAJbNbGKPFXCWuBvf9Ss623VQ5DA success
    Program log: Closing the escrow account...
    Program 4yBTZXsuz7c1X3PJF4PPCJr8G6HnNAgRvzAWVoFZMncH consumed 23373 of 200000 compute units
    Program 4yBTZXsuz7c1X3PJF4PPCJr8G6HnNAgRvzAWVoFZMncH success
```
