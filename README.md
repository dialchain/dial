# Distributed Immutable Assertions Log (DIAL)
The DialChain is a distributed log with the main purpose of turning each inserted __declaration__ into an __immutable assertion__. The DialChain can be seen as a log holding __state of tokens__. Tokens can be used to represent digital assets, people, organizations or even real estates, in short everything addressable and therefore tokens are non fungible.

A __time window__ is the lapse of time in which all eligible validators agree on the __state__ of every single __token__ maintained by the Dial network. After a time window is closed, the Dial protoccol assumes every token has a cosistent state across the network (all participants). To guaranty all participants see the same state, a time window closes with a __time window hash__. This is the hash of the state of all non expired tokens existent in the network. This hash is build in two steps: (1) __the neighborhood hash__ documents the state of all tokens maintained by the neighborhood in the target time window. For each token, the token-id and the file content identifier is included. (2) __the time window hash__ is the hash of all neighborhood hashes for that time window. For each neighborhood hash, the neighborhood-hash-id and the neighborhood protocol file content identifier (cid). The resulting file is the time window protocol. The time window protocol is independently signed and published by each neighborhood. The final protocol is the one identical for __51%__ of neighborhoods, as each neighborhood has a __51%__ decision rule. A validator consents with the state of the network by including the hash of the time window __tw-2__ in each publication of time window __tw__.

__Eligible validators__ are the one listed for the target time window. The DialChain is designed to allow __11__ validators per neighborhood. The list of eligible validators for a given time window is always known in advance, as validator must register intention to perform in time winndow __tw__ two time windows in advance __tw-2__.

__Closing__ time window tw occurs during time window tw+1. Closing operations are performed by eligible validators of tw during tw+1. The duration of a time window is __one Earth Hour__. This means a declaration published to the DialChain might need up to 2 earth hours to achieve finality.

__Instant Finality__ is nevetheless provided by the DialChain's __Ephemeral Neighborhood Protocol (ENP)__. ENP secures a deterministic association between each token and a small group of validators (neighborhood) responsible for the guarding of that token in a given time window. This way double spending can only occur with the complicity of all those validators in the host neighborhood. If one validator of the neighborhood has a fraud proof, it can spread a fraud declaration through the neighborhood and the next closes neigborhood. A participant willing to assume finality can request the validity proof from all validators of the target neighborhood. If __at least one of the validators__ returns a fraud declaration, finality shall not be assumed. If all active validators returns a validity proof, finality can be assumed. In presence of a fraud proof, participant must wait for the closing of the time window to check finality.

__Speed of Validation__ occurs by making sure all eligible validators in a neighborhood have the same state of assigned tokens, prior to starting the time window. If less than 51% of eligible validators of a neighborhood are present at any moment during the time window, declaration is also validated by the next closest neighborhood.

The DialChain is unique in its kind of offering an __unlimited block size__ and a __deterministic ordering and execution protocol (DETOX)__. This might sound negligeable at first but will later be proven essential for the sustainability of blockchain networks and the adoption of blockchain technology by other industries. __Unlimited blocksize__ is by no mean an obstacle to scalability, as the DialChain is designed to allow each participant (e.g. mobile phone) to act as a validator. While growing demand for publications will automatically lead to a growing number of validators, ENP will automatically grow the number of neighborhoods as number of validators grow.

__The Maximal Number of Validators__ eligible for a time window will highly depend on the number of tokens maintained by the DialChain and the frequency of of publication request to the network. By controlling the number validators, the DialChain will make sure post window coordination and synchronization operations are kept efficient.

__File Size of the DialChain__ will also be kept down to the essential by enforcing token expiration. In order to keep maintenance reasonable, the Dialchain is built on the principel that each token is fully represented by the last valid declaration. This way, there is no need to include the history of a token in the validation process. Beside having a single file represent each token, the price paid to maintain a token on the DialChain is a factor of the expiration of the token. Enforcing expiration of each token allows the DialChain to constantly prune the chain.

More on the architecture of the DialChain can be found under [DialChain white paper](./dial.md)

# Rationales
The architecture of current blockchain technologies make them suitable for defined use cases, but unappropriate for others. The bitcoin network is for example a great settlement platform for transactions with high monetary value. Following is a non-exhaustive list of reasons why we are going for a new DialChain architecture:

## Deterministic Ordering of Transactions
No transaction recording/execution system will work at scale, if it cannot provide a guarantee for the time and order of execution of submitted transactions.

Traditional market makers (banks, brokers, ...) are known to exploit existing asymmetry of information and thereby capitalize on arbitration opportunities.

Despite the decentralized nature of blockchain networks, we are still faced with the situation where a selected miner (or validator) decides on which transactions will be included into block being sealed. Leading to the phenomena known as MEV (Miner Extractable Value).

Our __DETOX__ guarantees that a submitted declaration will be included within the requested time frame.

## Spam Resistance
The DialChain is open and permissionless, but built on top of a fundamental spam resistance system that makes sure performance of DialChain service providers are remunerated. The same system ensures revenue generated from the publication of a single declaration is sufficient to cover present and future performance required to validate, maintain and retire that the underlying token.

The price paid by a participant to publish a declaration has a minimum cap, a file size factor and a validation effort factor. This price is set substantial enough to have a significant impact on the wallet of a participant generating spammy declarations.

## Sustainability Incentive
Traditional blockchain networks do not reflect on the future cost of current operations. Most blockchain networks are built on the speculation that the appreciation of the underlying crypto currency will motivate miners (validators) to stay in business. This is a risky approach as:
- This __currency appreciation based theory__ does not give miners the necessary accounting tools to legally build provisions for the future maintenance of those files.
- Letting a miner build a position in the miner's balance sheet does not prevent the miner from quitting when yield gets unattractive (due to increase of competition in the network and among networks).
- Further, the massive growth of the blockchain file size (block history) might make the entrance of new validators economically unattractive.

As the DialChain does not plan with future appreciation of the DIAL, reserves needed to maintain a declaration during the lifetime of that declaration is collected from the issuing participant with the publication of that declaration. The collected revenue is held in the DIAL Treasury and distributed to validators for each hour of relevance of the concerned record.

## Validator Diversification
Because of the simplicity of the no-racing validation protocol, operating validator node:
- will not require special hardware components (like ASICS)
- will not require unusual data center skills

In short, the DialChain is designed simple enought to allow each mobile phone to play the role of a validator. This simplicity shall lead to the largest spreading of validators around the world. The larger the validator base, the stronger the security of the network.

## No Validator Dominance
Validator dominance cannot occur as assignment of validators and declarations to neighborhoods occurs in a deterministic but unpredictable manner. In order for a validator to corupt the system, the validator has to controll more than half of the validators of a neighborhood and be lucky enougth to have the target token assigned to that neighborhood in the given time window.

An even if corruption occurs during the time window, counter validation at window closing will detect the flaw and discard the transaction.

## Double Spending
All token in the DialChain are non fungible in that each token has a unnique identifier. Once existent, the modification of a token must obei the rules defined in the controller block of the corresponding declarationn. As the Dial protocol uses the token id to determine the neighborhood controlling the token in the open time window, there is no way a token can be modified in parallel by two conflicting declarations.

## Programmer Adoption
The integration of the DialChain with existing business applications (like enterprise resource planning systems) is an essential goal toward the mass adoption of the DialChain. With this respect, the DialChain is built on the top of the simplest most use computer idioms like [JSON](https://datatracker.ietf.org/doc/html/rfc8259), [JWS](https://datatracker.ietf.org/doc/html/rfc7515), [DID Core](https://www.w3.org/TR/did-core/).

The DialChain will later introduce TypeScript based code automates to allow for programable declarations.

# Core Principles
A declaration is a formal or explicit and self-contained statement or announcement. A declaration is used to create and modify tokens. For this purpose, each declaration exposes a controller property that defines modification rules of the referenced token.

The purpose of the DialChain is to validate, legitimate and finalize declarations. This is done by applying following rules:
- Anyone can submit a declaration to create a token. The declaration must present a unique identifier not yet in used in the DialChain. We use cryptographic public keys for this purpose.
- Only the controller of a token can modify that token. Modification is done by submitting a declaration bearing the target token identifier and a valid assertion of the controller of that target token.
- In a DialChain neighborhood upon reception of a declaration publication request, each validator of the neighborhood:
  - proceeds with the formal validation of the declaration, then
  - proceeds with the verification of control rules (legitimation), then
  - proceeds with the signature of the declaration, then
  - proceeds with the distribution of the declaration to all other validators in the n.

After closing a time window __tw__, means during the course of the time window __tw+1__, validators of time window __tw__ coordinate to produce the hash of each neighborhood and then the hash of the closed time window __tw__. Finality is achived when 51% of neighborhoods present the same natwork protocol, containing all neighborhood protocols. Each neighborhood protocol containing a 51% vote of the neighborhood protocol.

