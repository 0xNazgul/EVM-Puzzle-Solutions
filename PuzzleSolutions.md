# EVM Puzzle Solutions 
This is of a walkthrough for [Franco Victorio's EVM Puzzles](https://github.com/fvictorio/evm-puzzles). I suggest you try them on your own and then come to this for hints and the answers.

## **Puzzle 1**
**HINT:** Look at the positon of JUMPDEST.
<details>
<summary>Answer</summary>
<p>
You want to give the value of 8 so that when CALLVALUE is given to JUMP it goes to the JUMPDEST to avoid the REVERTs.

You should get a .json output in the solutions folder like so:

```js
{"value":8,"data":"0x"}
```
</p>
</details>

## **Puzzle 2**
**HINT:** Look at the positon of JUMPDEST and what the CODESIZE is.
<details>
<summary>Answer</summary>
<p>
The way SUB works is it takes 2 inputs from the stack since CALLVALUE and CODESIZE are the values latest on the stack it will do CODESIZE - CALLVALUE. The CODESIZE is 10 and JUMPDEST is in postion 6 we need to give a value of 4 to give JUMP the value of 6.

You should get a .json output in the solutions folder like so:

```js
{"value":4,"data":"0x"}
```
</p>
</details>

## **Puzzle 3**
**HINT:** CALLDATASIZE outputs the byte size of the calldata.
<details>
<summary>Answer</summary>
<p>

Since the JUMPDEST is in postion 4 we need to give a calldata that is exactly 4 bytes long: ```0x00000000```.

You should get a .json output in the solutions folder like so:
```js
{"data":"0x00000000","value":0}
```
</p>
</details>

## **Puzzle 4**
**HINT:** XOR is a ^ b while taking:
* a: first binary value.
* b: second binary value. 
<details>
<summary>Answer</summary>
<p>
JUMPDEST is in postion 0A(10) and CODESIZE is 12 we need to find the when 12 ^ CALLVALUE = 10 which is 6.

You should get a .json output in the solutions folder like so:
```js
{"value":6,"data":"0x"}
```
</p>
</details>

## **Puzzle 5**
**HINT:** You need to get EQ to resole as 1(True).
<details>
<summary>Answer</summary>
<p>
To solve this one we need to have EQ resolve as 1 or true. To do that we have the MUL return 0100 or 256 bytes. We can figure this out by simply by taking the square root of 256 which is 16.

You should get a .json output in the solutions folder like so:

```js
{"value":16,"data":"0x"}
```
</p>
</details>

## **Puzzle 6**
**HINT:** Review what CALLDATALOAD is and it's outputs.
<details>
<summary>Answer</summary>
<p>

Since CALLDATALOAD is padded we have to add 0's to the JUMPDEST location, 0a. ```0x000000000000000000000000000000000000000000000000000000000000000a```.

You should get a .json output in the solutions folder like so:

```js
{"data":"0x000000000000000000000000000000000000000000000000000000000000000a","value":0}
```
</p>
</details>

## **Puzzle 7**
**HINT:** You'll need to create a contract that contains a code size of 1.
<details>
<summary>Answer</summary>
<p>

Do this we can put together a contract like so:
```
PUSH1	FF
PUSH1	00
MSTORE	
PUSH1	01
PUSH1	00
RETURN
```                            
This will be a byte code ```0x60FF60005260016000F3```.
You should get a .json output in the solutions folder like so:

```js
{"data":"0x60FF60005260016000F3","value":0}
```
</p>
</details>

## **Puzzle 8**
**HINT:** Again you will need to create a contract only this time you need to also focus on the CALL into the contract.  
<details>
<summary>Answer</summary>
<p>

Do this we can put together a contract like so:
```
PUSH1	FD
PUSH1	00
MSTORE8	
PUSH1	01
PUSH1	00
RETURN
```   
The main difference here is the PUSH1(60FD). FD is the opcode for REVERT which when called into will return 00 because it fails or reverts.
This will be a byte code ```0x60FD60005360016000F3```.
You should get a .json output in the solutions folder like so:

```js
{"data":"0x60FD60005360016000F3","value":0}
```
</p>
</details>

## **Puzzle 9**
**HINT:** Review what LT, CALLDATASIZE and CALLVALUE.
<details>
<summary>Answer</summary>
<p>

To get to the first JUMPI you'll need to send calldata that is longer then 03. Now it can't be a extremly large number because CALLDATASIZE is used again later. Where CALLDATASIZE * CALLVALUE = 08. So with both instances in mind, a CALLVALUE of 2 and a CALLDATASIZE of ```0x00000000``` would solve the puzzle.


You should get a .json output in the solutions folder like so:

```js
{"value":2,"data":"0x00000000"}
```
</p>
</details>

## **Puzzle 10**
**HINT:** Review what GT, ISZERO, and SWAP1.
<details>
<summary>Answer</summary>
<p>

The first and last JUMPDEST are dependent on the value sent. So to figure that we'll look at the second JUMPDEST and it is asking that 0a + CALLVALUE = 25. This would be 15, which is also ok for the first JUMPDEST, 15 < CODESIZE(26). For the MOD to return 0 to pass the ISZERO, the CALLDATASIZE has to be multiple of 3. Simpaly ```0x000000``` would work here.

You should get a .json output in the solutions folder like so:

```js
{"value":15,"data":"0x000000"}
```
</p>
</details>