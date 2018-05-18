The terminal interface to the oracle
=============


####New question oracle
This oracle asks a true/false question about the future. Eventually, the answer to this question will get recorded on the oracle, and will be accessible to the smart contracts.
```
api:new_question_oracle(Start, Question).
```
This returns the OID, which is necessary for making markets.

####New governance oracle
This oracle updates the variables that define the blockchain protocol. 
```
api:new_governance_oracle(GovName, GovAmount).
```
This returns the OID for this oracle.

You can look up current governance values like this:
```
trees:dict_tree_get(governance, GovName).
```

####See existing oracles
```
oracles:all().
```
returns a list like [{Question1, Oracle1}, {Question2, Oracle2}...].
You can use this to find out the OID for an oracle.

#### look up an oracle by id
```
trees:dict_tree_get(oracles, ID).
```

The order of things stored in the oracle datastructure is defined in [the records.hrl file](https://github.com/zack-bitcoin/amoveo/blob/master/apps/amoveo_core/src/records.hrl#L62)

####Bet in an oracle
type is one of the atoms in this list: [true, false, bad]
You can either bet that the answer to the question is true or false, or you can bet that it is a bad question.
```
api:oracle_bet(OracleID, Type, Amount).
```
Type is either 1, 2, or 3.
1 = true
2 = false
3 = bad question

####Close an oracle
If the oracle has had the same output state for a long enough period of time, then this is how anyone can close the channel and end the betting period.
```
api:oracle_close(OracleID).
```

###Oracle Shares
Collect shares purchased in an oracle
```
api:oracle_winnings(OracleID).
```

####Oracle unmatched
If you had unmatched trades sitting in the order book when the oracle closed, this is how you get your money back.
```
api:oracle_unmatched(OracleID).
```

#### Markets
read about how to launch a market on a single full node here:
[market](commands_market.md)