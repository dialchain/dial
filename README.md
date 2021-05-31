# Distributed Immutable Assertions Log (DIAL)
The DialChain is a distributed log with the main purpose of turning each inserted __declaration__ into an __immutable assertion__. The DialChain is unique in its kind of offering an __unlimited block size__ and a __deterministic ordering and execution protocol__ (__DETOX__).

# Abstract
A declaration can only be inserted into the log by a validator. Each validator is responsible for declarations it inserts into the log. But because the effect of a declaration can conflict with the effect of another declaration, validation of declarations must be performed prior to their publication into the DialChain log.

Finality turns each declaration into an __immutable assertion__. __Finality__ is achieved by ensuring that each inserted declaration is propagated to all __validators__ within a defined time frame called __Time Window (Block)__. All declarations of a closed time window are final and non-conflicting with each other. 

The DialChain uses an __earth day__ to contain a block, meaning that one would have to wait for the end of the day to achieve finality. 

Our __Proof of Guarantee__ consensus ensures that the validator, during the day will cover damages caused by the publication of a conflicting declaration. At the end of the day, any residual conflict is jointly covered by all validators.

The DialChain is unique in its kind of offering an unlimited block size and a deterministic ordering and execution protocol. This might sound negligeable at first but will later be proven essential for the sustainability of blockchain networks and the adoption of blockchain technology by other industries.

More on the architecture of the DialChain can be found under [DialChain white paper](./dial.md)

# Rationales
The architecture of current blockchain technologies make them suitable for defined use cases, but unappropriated for others. The bitcoin network is for example a great settlement platform for transactions with high monetary value. Following is a non-exhaustive list of reasons why we are going for a new DialChain architecture:

## Deterministic Ordering of Transactions
No transaction recording/execution system will work at scale, if it cannot provide a guarantee for the time of and order of execution of submitted transactions.

Traditional market maker (banks, brokers, ...) are known to exploit existing asymmetry of information and thereby capitalize on arbitration opportunities.

Despite the decentralized nature of blockchain networks, we are still faced with the situation where a selected miner (or validator) decides on which transactions will be included into block being sealed. Leading to the phenomena known as MEV (Miner Extractable Value).

Our __DETOX__ (deterministic ordering and execution protocol) guarantees that a submitted declaration will be included within the requested time frame.

## Spam Resistance
The DialChain is built on top of a fundamental spam resistance system that makes sure the revenue generated from the publication of a single declaration is sufficient to cover present and future performance required to validate, maintain and retire that declaration.

In order to protect validators (or service provider in general), the DialChain defines a fix price to pay for each service intent request. Recall that the service intent request also returns a binding offer to the requesting participant.

In order to protect the DialChain, each validator can only guarantee publications (inside a block or time window) up to the amount of the validator’s deposit.

The price paid by a participant to publish a declaration has a minimum cap, a file size factor and a validation effort factor. This price is generally substantial enough to have a significant impact on the wallet of a participant generating spammy declarations.

These three factors (a) payment for intent request, (b) payment for publication and (c) limitation of publication coverage to the deposit of the validator’s deposit, all together constitute an effective spam resistance mechanism.

## Sustainability Incentive
Traditional blockchain networks do not reflect on the future cost of current operations. Most blockchain networks are built on the speculation that the appreciation of the underlying crypto currency will motivate miners (validators) to stay in business. This is a risky approach as:
- This __appreciation theory__ does not give miners the necessary accounting tools to legally build provisions for the future maintenance of those files.
- Letting a miner build a position in the miner's balance sheet does not prevent the miner from quitting when yield gets unattractive (due to increase of competition in the networks and among networks).
- Further, the massive growth of the blockchain size (block history) might make the entrance of new validators economically unattractive.

As the DialChain does not plan with future appreciation of the DIAL, reserves needed to maintain a declaration during the lifetime of that declaration is collected from the issuing participant with the publication of that declaration. The collected revenue is held in the DIAL Treasury and distributed to validators for each day of relevance of the concerned record.

## Deterministic Conflict Resolution
In the DialChain network, validators are responsible for declarations they verify and publish to the DialChain. Inside the time window, responsibility is solely backed up with the deposit of the validator. At closing, we assume all validators are verifying all declarations published during that time window. After closing, any residual validator mistake is the common responsibility of all validators. 

Incremental validation is essential to have all validators validate all declarations by the end of the time window. For that purpose, validators also publish a synchronization hash every 10 minutes or on the request of another validator (Sealing what they have done so far).  

A validator that fails to synchronize for 10 minutes will lose all revenue earned during those 10 minutes.
If a validator fails to synchronize the las 10 minutes of a time window (because of a crash), all assertions known from that validator but not part of his last sync will be revalidated by other validators and a deterministic algorithm will accept 3 propositions. Those three will then collect the payment associated with those declarations.

## Security of Validator Nodes
The DialChain requires each validator to have following verifiable properties:
- operate at least 3 nodes distributed among ASes (autonomous systems) and ISPs (Internet service providers), each node with a different DialChain client,
- validate each declaration with at least 2 of 3 signatures,
- separate validator treasury spending key from validator publication keys,
- have three custodians who hold secrets used to operate validator nodes
- required 2 of three signatures to spend values held by the validator treasury

These security properties will allow to keep validator infrastructure simple but solid enough against malicious attacks. As validators make the fundament of the DialChain.

## Validator Diversification
Because of the simplicity of the no-racing validation protocol, operating validator node:
- will not require special hardware components (like ASICS)
- will not require unusual data center skills

This simplicity shall lead to the largest spreading of validators around the world.

Nevertheless, the maintenance cost reimbursed to validators by the DIAL Treasury will be a factor of the revenue brought by the validator during that time window.

## No Validator Dominance
Validator dominance cannot occur as:
- Each validator can validate as many declarations as its guarantee deposit can allow to happen.
- The share of the treasury co-controlled by a validator inside a time window does not go beyond the guaranty deposit of that validator.
- Joining or leaving the DialChain does not require the consent of other validators.

## Participant based Representative Democracy
Beside structural modifications like the extension of the DialChain with additional functions, no other procedure of the DialChain requires voting or decision. When voting is required, all identified DialChain participants are eligible to vote (not only validators). A representative democracy will allow participants to delegate their vote to chain representatives that can carry the vote on their behaves.

## Double Spending
A spending declaration is one that spends or reserves an amount held by the issuing participant. If the declaration is part of a closed block (time window), the earning participant can consider that declaration verified by all participants and final (assertion).

As our block time is an Earth Day (Time Window), earning participant might want to have a faster confirmation (in the next second). Against a lesser fee, earning participant can have a published transaction counter-validated by one or many other validators. This counter-validation will specify a coverage amount (ranging from the fees paid to the total transaction amount).

The DialChain validation logic requires declarations issued by the same participant to be chained. Allowing, while still inside the time window, for quick access to the last validator of a spending declaration inside the time window.

## Programmer Adoption
The integration of the DialChain with existing business applications (like enterprise resource planning systems) is an essential goal toward the mass adoption of the DialChain. With this respect, the DialChain is built on the top of the simplest most use computer idioms like [JSON](https://datatracker.ietf.org/doc/html/rfc8259), [JWS](https://datatracker.ietf.org/doc/html/rfc7515), [DID Core](https://www.w3.org/TR/did-core/).

The DialChain will later introduce TypeScript based code automates to allow for programable declarations.