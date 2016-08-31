# pyethereum client

### Core Mod

#### Files affected
 - [/ethereum/config.py](https://github.com/ethereumproject/pyethereum/blob/develop/ethereum/config.py)
 - [/ethereum/blocks.py](https://github.com/ethereumproject/pyethereum/blob/develop/ethereum/blocks.py)

```Exponential difficulty timebomb period``` is defined on [lines 45-47 in config.py](https://github.com/ethereum/pyethereum/blob/ca0e3a556fe420c2b4e4c6621d99e6028142297e/ethereum/config.py#L45)

```
45      # Exponential difficulty timebomb period
46	    EXPDIFF_PERIOD=100000,
47	    EXPDIFF_FREE_PERIODS=2,
```

```period_count``` is defined on [lines 76 in blocks.py](https://github.com/ethereum/pyethereum/blob/ca0e3a556fe420c2b4e4c6621d99e6028142297e/ethereum/blocks.py#L76) which is used to 'arm' the bomb

```
62  # Difficulty adjustment algo
63  def calc_difficulty(parent, timestamp):
64      config = parent.config
65      offset = parent.difficulty // config['BLOCK_DIFF_FACTOR']
66      if parent.number >= (config['METROPOLIS_FORK_BLKNUM'] - 1):
67          sign = max(len(parent.uncles) - ((timestamp - parent.timestamp) // config['METROPOLIS_DIFF_ADJUSTMENT_CUTOFF']), -99)
68      elif parent.number >= (config['HOMESTEAD_FORK_BLKNUM'] - 1):
69          sign = max(1 - ((timestamp - parent.timestamp) // config['HOMESTEAD_DIFF_ADJUSTMENT_CUTOFF']), -99)
70      else:
71          sign = 1 if timestamp - parent.timestamp < config['DIFF_ADJUSTMENT_CUTOFF'] else -1
72      # If we enter a special mode where the genesis difficulty starts off below
73      # the minimal difficulty, we allow low-difficulty blocks (this will never
74      # happen in the official protocol)
75      o = int(max(parent.difficulty + offset * sign, min(parent.difficulty, config['MIN_DIFF'])))
76      period_count = (parent.number + 1) // config['EXPDIFF_PERIOD']
77      if period_count >= config['EXPDIFF_FREE_PERIODS']:
78          o = max(o + 2 ** (period_count - config['EXPDIFF_FREE_PERIODS']), config['MIN_DIFF'])
79      # print('Calculating difficulty of block %d, timestamp difference %d, parent diff %d, child diff %d' % (parent.number + 1, timestamp - parent.timestamp, parent.difficulty, o))
80      return o
```
##Option 1

The modification to remove "the bomb" is to remove lines 76-78. 
var o is calculated on [line 75] (https://github.com/ethereum/pyethereum/blob/ca0e3a556fe420c2b4e4c6621d99e6028142297e/ethereum/blocks.py#L75). This value can be returned instead of evaluating if the period has exceeded the EXPDIFF_FREE_PERIODS count which 'arms' the bomb. 
```o = max(o + 2 ** (period_count - config['EXPDIFF_FREE_PERIODS']), config['MIN_DIFF'])``` adds 'the bomb' number for a period. without this difficulty will adjust normally 
Remove the code in config.py for clean up purposes.

##Option 2
By modifying the values in config.py the "fuse" on "the bomb" can be adjusted.
