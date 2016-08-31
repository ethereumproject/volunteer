# geth client

### Core Mod

#### Files affected
 - [/core/block_validator.go](https://github.com/ethereum/go-ethereum/blob/5f55d95aea433ef97c48ae927835d833772350de/core/block_validator.go)

```CalcDifficulty``` is defined on [lines 265-312 in block_validator.go](https://github.com/ethereum/go-ethereum/blob/5f55d95aea433ef97c48ae927835d833772350de/core/block_validator.go)

```
func calcDifficultyHomestead(time, parentTime uint64, parentNumber, parentDiff *big.Int) *big.Int {
	// https://github.com/ethereum/EIPs/blob/master/EIPS/eip-2.mediawiki
	// algorithm:
	// diff = (parent_diff +
	//         (parent_diff / 2048 * max(1 - (block_timestamp - parent_timestamp) // 10, -99))
	//        ) + 2^(periodCount - 2)
```

The modification to remove the bomb is to remove lines 299-309, and return [```params.MinimumDifficulty``` on line 296](https://github.com/ethereum/go-ethereum/blob/5f55d95aea433ef97c48ae927835d833772350de/core/block_validator.go#L296) instead of adding the exponential factor.

### Flag settings

```
cmd/utils/flags.go
```

#### Flag Propagation
