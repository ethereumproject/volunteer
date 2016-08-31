# The Bomb

![etc bomb](http://i.imgur.com/w9ZxtuN.jpg)

Public plan for the disposal of 'the bomb', tests, and ice age prevention

The need for a stable code to neutralize the difficulty equation known as 'the bomb' or 'ice age' has been suggested. This code will give the ETC community the option of having a 'switch' to prevent the unwanted effects of high mining time if, so needed.

Branches will be formed on indivdual core projects for bomb disposal. 

##Task 1 
  - Identify the exponential difficulty code in each project

##Task 2
  - Find way to Render the code harmless by deletion or circumvention

##Task 3 
  - Add 'DIEHARD' fork code to accomplish task 2 at a predetermined block number for a universal sync transition
  
###Task 4
  - Testing

------------------

##The Bomb

```block_diff = parent_diff + parent_diff // 2048 * max(1 - (block_timestamp - parent_timestamp) // 10, -99) + int(2**((block.number // 100000) - 2))```

The first part of the algorithm, ```parent_diff + parent_diff // 2048 * max(1 - (block_timestamp - parent_timestamp) // 10, -99)```, is in charge of adjusting the difficulty based on the elapsed time between prior blocks. It makes incrimental adjustments up or down to reach a mean time between blocks of  ~15 sec

The second part of the algorithm , ```+ int(2**((block.number // 100000) - 2))```, is "the bomb". It doubles its difficulty every 100000 block, forever, until the the blocks are to difficult to solve in a reasonible time.


##Option 1
Disabling the second part of the algorithm removes the bomb and ~14 is the target time forever. 

##Option 2
###Kick the Can Method #1  

Change the fuse 

```((block.number // 100000) - 2)``` 

```block.number``` is the current block number

```100000``` sets the pace of the bomb. This is 'the fuse' A larger number would slow the bomb down. 

The ```- 2``` in the algo was origanally set as "the bomb" was not to be engaged until after block 200000.    

###Kick the Can Method #2

Reset the delay

the ```- 2``` in the algo was origanally set as "the bomb" was not to be engaged until after block 200000.Changing this number to a higher number allows the bomb to be delayed. i.e. ```-50``` would reset and delay the bomb from starting until block 50000000


### Research


[ETHEREUM: A SECURE DECENTRALISED GENERALISED TRANSACTION LEDGER](http://gavwood.com/paper.pdf)

HOMESTEAD REVISION

DR. GAVIN WOOD

Section 4.4.4

[EIP #2 ](https://github.com/ethereum/EIPs/blob/master/EIPS/eip-2.mediawiki)

Title: Homestead Hard-fork Changes

Author: Vitalik Buterin <v@buterin.com>

[Human Version](https://www.reddit.com/r/ethereum/comments/4pnjgr/ethereum_blocktime_simulator_discussion_about_the/)

reddit user Giact
