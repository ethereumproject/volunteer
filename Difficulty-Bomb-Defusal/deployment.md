# Deployment Options

### Proposed Deployment (11-08-2016)

<b> Variables </b>

```
A = Activation block number
T = Activation time
C = Number of blocks mined by consenting clients
Q = Number of mined blocks required for quorum
G = Grace period, measured in number of blocks
```

Deployment shall be controlled by hash-power supermajority vote, but the earliest possible activation time is Block number ```A```.

Activation is achieved when ```9,000??? (C)``` of ```10,000??? (Q)``` consecutive blocks in the best chain 
(that is, the one with the most work) have a version number indicating support for the change in difficulty. 
The activation block number will be the ```C'th``` block plus a ```G```-block grace period
to give any remaining miners or services time to upgrade.

Block version numbers are used only for activation; once activation is achieved, 
the difficulty shall be as described in the specification section, regardless of the version number of the block.
