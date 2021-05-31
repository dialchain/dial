# DialChain White Paper
The DialChain is a distributed log with the main purpose of turning each inserted __declaration__ into an __immutable assertion__. The DialChain is unique in its kind of offering an __unlimited block size__ and a __deterministic ordering and execution protocol__ (__DETOX__).

# Abstract
A declaration can only be published to the log by a validator. Each validator is responsible for declarations it publishes to the log. But because the effect of a declaration can conflict with the effect of another declaration, validation of declarations must be performed prior to their publication into the DialChain log.

__Finality__ turns each declaration into an immutable assertion. Finality is achieved by ensuring that each published declaration is propagated to all validators within a defined time frame called __Time Window (Block)__. All declarations of a closed time window are final and non-conflicting with each other. 

The DialChain uses an __earth day__ to contain a block, meaning that one would have to wait for the end of the day to achieve finality. 

Our __Proof of Guarantee (PoG)__ consensus ensures that a validator, during the day will covers damages caused by its publication of a conflicting declaration. At the end of the day, any residual conflict is jointly covered by all validators. With __PoG__, consumer of a declaration (e.g., payee) will not need to wait for the finality of that declaration.

The DialChain is unique in its kind of offering an unlimited block size and a deterministic ordering and execution protocol. This might sound negligeable at first but will later be proven essential for the sustainability of blockchain networks and the adoption of blockchain technology by other industries.

# Terms

## Declaration
A declaration is a formal or explicit statement or announcement. Depending on its intent, a declaration can be signed by zero, one or many participants. Even the process of inserting a file into the DialChain log is a declaration.
Many signatures of the same declaration can be embedded into the same file or provided by external signature files. Our __Universal Data Block Identifier__ makes it easy to reshuffle signed data blocks. This allows for signatures of declarations to occur sequentially or parallelly. 

## Assertion
An assertion is a confident and forceful statement of fact or belief. It is our foundation of trust. Once finalized, a declaration becomes an immutable assertion.

## Finality
Finality is achieved by ensuring that each inserted declaration is propagated to all validators within a defined time frame called __Time Window__. 

With our __Proof of Guarantee__ consensus, consumer of a declaration (e.g., payee) will not need to wait for the finality of that declaration. A simple __Counter Proof of Publication__ will provide the necessary trust to proceed forward with the transaction.

## Participant
A participant is a [decentralized identifier (DID)](https://www.w3.org/TR/did-core/) registered with the DialChain. Despite other blockchain networks, presenting a public key is not sufficient to represent an identity on the DialChain.

## Organization
An organization is a DID controlled by zero or more participants. An organization defines procedures and associated decision (signature) rules.

## Account
An account is a DID that holds an asset. An account can be controlled by either a participant or an organization.

## Validator
A validator is an organization that can publish a declaration to the DialChain by the mean of signing the __declaration__ and sharing the file with all other validators.

## Service Provider
Beside validators, the DialChain will define many other types of service providers.

## Service Record
Service providers publish their service records to the DialChain, including their service addresses and prices.

## Intent Request
An intent request is generally sent by a participant to a service provider to enquire on the price of a service. The response of an intent request is binding for the service provider.

# Economics
An economy is denominated by a set of service providers that together co-lock a certain amount of external securities in the treasury of that economy. The total value locked by that economy is so balanced that:
- No (group of) service provider can abandon the economy with an amount higher than their deposit.
- Revenue retained by the treasury and redistributed to service providers for future activities grows substantially enough to discourage any abandonment of the economy.

## Multiple Economies
The Dial Network can operate multiple economies. What distinguishes economies from each other is the nature of external securities transferred into the economy.
- An economy will allow only established digital currencies to be deposited against native currencies
- Another economy will allow fiduciaries properties to be locked to back emission of native currencies
- A government might start an economy by providing a bridge to the government's treasury, so native currency can be generated/burned against deposit/withdrawal of fiat currency in that account.

## Openness of an Economy
The nature of the economy might (for example government initiated) reduce the openness of the economy. If for example a government condition the deposition of validator initial guaranty, they will have control on who can act as a validator in that economy.

# The Dial Economy
The Dial Native economy is the first one operated by the DIAL Network. It is designed to serve as the model economy. It is open and permissionless.

## Monetary Policy
The Dial economy does not print money. 
- Money emission occurs as counter value to deposited external securities.
- Value is generated by providing services against fees. 

## Dial Treasury
The Dial Treasury is an automatic and permissionless service that maintains accounts used to hold common monetary values of the Dial Network. The Dial Treasury does not print money. All money emitted by the Dial Treasury is backed by external assets.

## Value Generation
Every single service performed by a service provider in the Dial Network is paid for by the requestor of the service. The price of each service is left to the discretion of the service provider. An __intent request__ allows a requestor to collect prices and other execution conditions from different service providers.

## Value Added Tax (VAT)
In order to provide for sustainability, the Dial Network must make sure every present operation is priced with future costs it incurs. For example:

- Each file inserted in the DialChain log will have to be maintained for a substantial amount of time (we presume 50 earth years).
- Each monetary value held by the Dial Network will maintain a sound relationship to the corresponding external asset. For example, the BTC account held by the Dial Treasury will have to maintain a relationship to the corresponding wallets in the Bitcoin network.

The cost of maintaining those assets (log entries, currencies) is paid by the originating participant at the moment of publication of the asset producing declaration into the DialChain log. The Dial Treasury will retain this amount from the revenue of the service provider (in the form of a VAT). This retained revenue will be spent by the Dial Treasury during the lifetime of that asset to pay for the maintenance of that asset. For each block of maintenance of an asset, the corresponding maintenance fee will be distributed to the service providers of the network based on predefined distribution keys; sample key is the proportion of revenue generated during the block (e.g. earth day).

# Liquidity Service
The liquidity service of the DialChain is a service provided by the Dial Treasury that allows the mapping of external monetary values into the Dial Network. Those values are generally denominated L-XXX, where XXX is the denomination known in the world outside of Dial. E.g.: L-BTC, L-ETH. Beside fees collected by the Dial Treasury for the maintenance of those underlying records, the value of an L-BTC (Liquid Bitcoin) is a one-to-one mapping of the value of a Bitcoin.

## Exposing an External Monetary Asset (Liquid-Asset)
In order to expose an external monetary asset to the Dial Network, the Dial Treasury creates an account with the asset realm. e.g.: The Dial Treasury will maintain a wallet in the Bitcoin Network.

### Depositing of Liquid-Assets
If we take the BTC as an example, any participant will simply emit L-BTC by depositing corresponding BTC amount the Bitcoin wallet of the Dial Treasury. The purpose code of the transaction will reference the DialChain account of the depositing participant.

The participant will then have to:
- monitor the Bitcoin network to make sure the transaction is in a block,
- send a declaration of deposition to a DialChain validator that supports the Bitcoin connectivity service.

The DialChain validator will upon receiving the service request:
- verify the availability of fund in the Bitcoin network,
- credit the DialChain account of the depositing participant with the corresponding L-BTC amount (minus service fees)
- publish this declaration of deposition to the DialChain log.

At closing, each validator receiving the operation will verify availability of funds in the Bitcoin Network in the process of validating the closing declaration of the publishing validator.

### Withdrawal of Liquid-Assets
Taking the BTC example, the withdrawal of L-BTC occurs by simply sending a declaration of withdrawal to a validator.

The declaration of withdrawal will carry:
- the target BTC address
- the hash value of a secret

The validator upon reception of the service request will 
- Initiate the Bitcoin transaction
- prepare the bitcoin transaction with the provided hash value
- propagate the BTC transaction to algorithmically selected validators for counter signature (multisig)
- Upon reaching the required multisig quota, last validator will publish the treasury spending transaction to the bitcoin network.

If at closing the withdrawal happens to be conflicting, the treasury will be automatically compensated from the account of signing validators.

### Sample Treasury Accounts
Well known treasury accounts will be:

#### L-BTC
A treasury emitting L-BTC against BTC deposit.

#### L-ETH
A treasury emitting L-ETH against ETH deposit.

#### L-USDC
A treasury emitting USDC against USD.

## DIAL
The DialChain Treasury will be emitting L-DIAL against a basket of deposited crypto currencies like L-BTC, L-ETH, L-MATIC.

The L-DIAL exchange rate at the moment of deposit is defined by a basket holding the 5 most valuable crypto currencies in BTC market capitalizations on the 5 most liquid decentralized exchanges.

Oracles responsible for the provisioning of the DialChain with reference values will be determined at the moment of deployment.

Reference values are always valid for the duration of a block.

# Genesis

## Initial Validators
Initial validators are a group of participants which initialize the log:
- they setup the initial treasury
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
A time window can be any sort of time reference (e.g. an earth minute, hour, day or month). For the DialChain, we will select the __EARTH DAY__ as the reference time window. Time zone synchronized, the time window will start at 00:00:00:000 UTC and end at 23:59:59:999 UTC.

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

The PoG consensus allows the validator to cover the monetary value of validated declarations with an equivalent deposit. The validator deposit will be used repair damages caused by those validated declarations if at the closing of the time window conflicting declarations are discovered.

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