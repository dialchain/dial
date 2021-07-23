# Genesis

## Initial Validators
Initial validators are a group of participants which initialize the log:
- they setup the initial treasury (DialDAO)
- they deposit initial liquidity
- they validate each other in a ring by making sure each validator publishes the initial service record of all other validators

## Validator Registration
In order to qualify as a validator, a participant must:
- pay for basic deposit to the DialChain treasury
- register the publishing organization, by sending the registration record for publication to existing validators
- wait for the next block to publish the initial service record
- wait for the next block to start providing services

This is, it takes like 3 blocks to have a new service provider up and running.

# DialChain Log Structure

## DialChain Log Entry (DCLE)
DCLE is a file considered part of the DialChain log. A DCLE respects following rationales:
- contains one or many declarations, eventually from different private keys.
- contains exactly one __publishing declaration__. This asserts the insertion of the file by the force of the signature of the publishing __validator__.
- the publishing declaration contains the antecedent block's hash. This is the proof that the validator consents with the validity of the antecedent block.
- A participant shall never accept a log entry that contains the wrong antecedent block hash.

## Time Window (Block)
A time window can be any sort of time reference (e.g. an earth minute, hour, day or month). For the DialChain, we will select the __EARTH HOUR__ as the reference time window. Time zone synchronized, the time window will start at 00:00:00:000 UTC and end at 23:59:59:999 UTC.

The DialChain block has an unlimited block size. There is no disadvantage to validators as valiidators are paid for every DCLE inserted in the log.

## Finality
The finality of a declaration is provided when the block containing the enclosing DCLE is closed, as after closing all validators can compute the same block hash. This computed block hash is used in each publishing declaration of the subsequent block. The finality transforms each declaration into an assertion.

## Opening Declaration
An opening declaration is produced by each validator as a proof of joining the new block. An opening declaration is a merkle root of all closing assertions produced by all validators in the antecedent block (a.k.a antecedent block hash). This hash is the consent that the publishing validator accepts the antecedent block. This also means the validator acknowledges reception of all log entries of that antecedent block, and that the validator has verified the validity of every single log entry of that antecedent block.

Missing of an opening declaration indicates either of following unavailability states:
- the validator is not active in the current block,
- the validator has nothing to publish yet,
- the validator has left the network  

## Closing Declaration
A closing declaration is a merkle root of all declarations published by a single validator in that block. The closing declaration can be used by another validator to validate possession of all records produced by the signing validator.

### Joining and Leaving a Block
A validator can join and leave the current DialChain block any time within the current time window. In order to leave the DialChain block, a validator must publish his closing declaration. 

### Missing Closing Declaration
Validator will be punished for not publishing the closing declaration, as there will be no way to validate declarations it published. If the network is missing the closing declaration of a validator, a deterministic and algorithmic election process will automatically choose __3 alternative validators__ to revalidate all affected declarations and publish an __Alternative Closing Declaration__. If the validation of any entry fails, it is excluded from the closing entry and from the block. All liabilities resulting from the exclusion of failed entries are covered by the original validator.

If the opening declaration are all computed with the alternative closing declaration, revenue earned for the revalidated entries will be redistributed to the 3 alternative validators.

### Provisional Closing Declaration
Provisional closing declarations allow validators to synchronize their state with other validators during the time window. If for example the time window is an earth day, a validator can share a provisional closing declaration every 12 earth hours, 6 earth hours, every earth hour or every earth minute. A provisional closing declaration can also be shared whenever the validator thinks it is necessary to secure revenue generated so far from an eventual crash.

If at the end of a time window, a validator closing declaration is missing, his last provisional declaration will be used instead. Only transactions produced by that validator and not part of the last provisional closing declaration will need to be revalidated.

### Incremental Validation
Provisional closing declarations also help with incremental validation of entries produced by other validators, as a validator cannot present an entry anterior to a provisional closing declaration.

## Block Hash
The block hash is the merkel root of all available closing assertions of that block.

### Synchronization Window
Each validator has the responsibility to publish its closing record inside the synchronization window. As the computation algorithm allows for an incremental computation of the closing merkel root, there is no special extra time needed to compute the closing assertion.

- The time to compute the closing assertion shall be below a minute after the last millisecond of the time window, independent of the number of entries.
- For a reference time window of __ONE EARTH DAY__, the synchronization window can be __ONE EARTH MINUTE__.

### Recovery Window (Missing Validator)
If at the end of a block some validators are missing, algorithmic selected available validators will generate alternative closing records inside the recovery window. For a reference time window of __ONE EARTH DAY__, the recovery window can be __ONE EARTH MINUTE__.

## Resigning Missing Records
In general, published declarations are always distributed as:
- participant always receives the publishing declaration as a return to the service call.
- participant can share the record with another participant (in the context of a transaction)
- receiving participant will generally have the record validated by another validator. We call this act __Counter Proof of Publication__.

This is why we assume we will generally barely miss published records, even if the validator is down at the closing of the block.

Rejoining the network, a validator will have to resign all entries missing in the antecedent block and re-publish them in the current block.

# Proof of Guarantee Consensus (PoG)
The PoG consensus is only needed for the current time window. After the time window is closed, all validators are unanimous on the state of all declarations inserted in the log.

The PoG consensus allows the validator to cover the monetary value of validated declarations with an equivalent deposit. The validator deposit will be used to repair damages caused by those validated declarations if at the closing of the time window conflicting declarations are discovered.

During the current time window, a validator cannot cover for more than his own deposit. If a validator occurs to have exhausted his deposit inside a time window, that validator will have to delegate further publication requests to validators with available deposit. A single declaration can also be covered by many validators in case the declaration monetary value exceeds the capacity of a single declaration.

## Guarantee Use Case
If for example Paul has a balance of 5 dials, Paul spends 3 dials in a transaction, and Paul spends 3 dials again in a subsequent transaction, this subsequent transaction will be declared conflicting by the network at closing of the block and will be fixed with an automatic transfer of 1 dial from the validator's guarantee deposit to Paul's account to cover the negative balance. This fix is therefore only necessary if by the time of block closing no other positive transaction to Paul's account can help cover the damage.

## Monetary Value of a Declaration
If for example Paul has a balance of 5 dials, Paul spends 3 dials in a transaction, and Paul spends 3 dials again in a subsequent transaction, this subsequent transaction will be declared conflicting by the network at closing of the block and will be fixed with an automatic transfer of 1 dial from the validator's guarantee deposit to Paul's account to cover the negative balance. This fix is therefore only necessary if by the time of block closing no other positive transaction to Paul's account can help cover the damage.

# Treasury Operations
The DialChain Treasury is controlled by all validators. 

## Withdrawal Transactions
Treasury withdrawals are constrained by the nature of the external realm. Major crypto currency network will support multisig wallets. A deterministic algorithm will select a validator ring that sign a withdrawal transaction to the target beneficiary account.

## Sharing maintenance fees to Validators
The sharing of fees to validators occurs automatically, in the subsequent time window. As each validator knows their earnings, and the total earning, algorithmically selected validator will run the accounting and create the earning records for defined set of validators.

# DETOX
Our deterministic transaction ordering and execution protocol helps reduce hazard and opportunistic behavior of market participants, in particular validators.
- With the __unlimited block size__, there is a guarantee each valid declaration will be considered part of the intended time window (block).
- The __publication intent request__ allows a participant to obtain following data from many validators ahead of sending the declaration publication request:
  - a binding publication price,
  - a submission timestamp,
  - an open declaration coverage amount
## Parallel Publication
A participant can decide to have the same declaration parallelly published by many validators, as long as the participant is ready to pay the service fees to each validator. 

Parallel insertion of the same declaration:
  - won't change the effect of that declaration on the DialChain, but
  - will increase the publication chances of the declaration (reducing opportunistic behavior of validators).

## Market Transparency
DETOX increases market transparency and helps mitigate MEV risks. Where MEV stands for [Miner Extractable Value or Maximal Extractable Value](https://blog.chain.link/what-is-miner-extractable-value-mev/).
- Because the price and time of submission is known beforehand, submitting participant can have a certain level of assurance that declaration will be published.
- Sending the intent request to many validators creates competition among validators and helps autoregulate the market. Validator with too many publication requests or lesser coverage budget in the current time window might increase their prices. Higher prices will in turn incentivize and attract new validators.

## Front Running Declarations
The intent request to many validators creates competition among validators and helps autoregulate the market. Validator with too many publication requests or lesser coverage budget in the current time window might increase their prices. Higher prices will in turn incentivize and attract new validators.