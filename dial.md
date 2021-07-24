# DialChain White Paper

# Abstract
The DialChain is a distributed log with the main purpose of turning each inserted __declaration__ into an __immutable assertion__. The DialChain can be seen as a log holding state of __tokens__. Tokens can be used to represent a digital coin, a person, an organization or even a physical building, in short everything addressable and therefore non fungible (__NFT__).

The DialChain is unique in its kind of offering an __unlimited block size__ and a __deterministic ordering and execution protocol (DETOX)__. Unlimited block size capability is achieved by accepting all valid declarations submited during a period of time (a.k.a epoch or time window). 

Instead of having a single validator building limited size blocks (PoW, PoS), DialChain's __Ephemeral Neighborhood Protocol (ENP)__ secures a deterministic association between each token and a group of validators (neighborhood) responsible for that token during the open time window. If the neigborhood can not achieve a __51%__ agreement over the state of a token, the next closest neigborhood is invited to covalidate that token. The process is repeated till a 51% consensus is achieved for any given declaration.

After closing a time window, each nneiborhood produces and distribute an execution protocol. This is the merkel tree hash of all transactions validated by the neighborhood during that time window. With the protocol of each neigborhood, each validator can compute the time window hash that is the merkel tree hash of all neigborhood protocols and the hash of the precedent time window.

# Core Principles
A declaration is a formal or explicit and self contained statement or announcement. A declaration is used to create and modify tokens. For this purpose, each declaration exposes a controller property that defines modification rules of the referenced token.

The purpose of the DialChain is to validate, legitimate and finalize declarations. This is done by applying following rules:
- Anyone can submit a declaration to create a token. The declaration must present a unique identifier not yet in used in the DialChain. We use cryptographic public keys for this purpose.
- Only the controller of a token can modify that token. Modification is done by submitting a declaration bearing the target token identifier and a valid assertion of the controller of that target token.
- A DialChain validator upon reception of a declaration publication request,
  - proceeds with the formal validation of the declaration, then
  - proceeds with the verification of control rules (legitimation), then
  - signs the declaration and drops it in the neiborhood responsible for that token in the current time window.
- In that neighborhood, all validators will:
  - procced with the verification of controll rules (legitimation), then
  - proceed each with the signature of the declaration, then
  - proceed with the distribution of the declaration to all other validators to achieve finality.

After closing a time window __tw__, means during the course of the time window __tw+1__, validators of time window __tw__ will coordinate to produce the hash of the closed time window __tw__. The signature of this hash bei each involved validator is the proof of finality of all declarations submitted in that time window. Consensus is reached when __51%__ of validators of __tw__ sign the hash.

__Finality__ turns each declaration into an immutable assertion. Finality is achieved by ensuring that each published declaration is propagated to all validators within a defined time frame called __Time Window (Block)__. All declarations of a closed time window are final and non-conflicting with each other. The cryptographic hash of a time window is included in the computation of the hash of the next time window.

The DialChain uses an __earth hour__ to contain a block, meaning that one would have to wait for the end of the hour to achieve finality. 

Our __Ephemeral Neighborhoud Protocol (ENP)__ secures a deterministic association between each token and a group of validators (neighbourhood) responsible for that token during the open time window. This deterministic association of tokens to neighborhoods is essential to prevent conflicting modifications on the same token (double spending). A neighborhood is a small enougth group of validators to synchronize concurent modifications on a single token. Consensus is achieved inside the neighborhood with a __51%__ rule.

# Validator
Validators are entities responsible for the security of the network. Validators can join and leave the DialChain at will. Nevertheless, commitment to participate in the validation of a time window are binding. A validator must explicitly announce it's intention to validate for time window __tw__ with a declaration published in time window __tw-2__. Therefore, while __tw-2__ is being sealed during __tw-1__ all validators for __tw__ are known. The __neighborhood__ building process for __tw__ can also take place, as building process is contolled by a deterministic algorithm.

## Joining the Network
Each validator is known to the network and is represented by a token whose declaration also contains the validator's service addresses. In order to join as a validator, it is sufficient to submit guaranty funds to the DialDao and send a __Validator Declaration__ to one or many existing validators.

A validator will generally need 3 time windows to get active.
- In __tw-3__ the validator can submit it's declaration of existance. This will be validated and published with this time window.
- During __tw-2__ the new validator announces it's intent to validate for __tw__, bei again submitting a declaration to the network (through an acctive validator).
- During __tw-1__, after the hash of __tw-2__ is published, the neighborhood building process for __tw__ takes place. tw validators start preparing the field. Loading known identifiers that might be processed in that neighbourhood during tw. Collecting ip addresses of peer validators in the same neighborhood.
- During __tw__ the validator is actively sent validation requests for token assigned to it's neighborhood.

## Leaving the Network
In order to leave, a validator just need to stop announcing itself for future time windows. As the declaration of readiness for the validation in a time window muss occur actively, an innactive validator will never be a problem for the network.

## Withdrawal of Guarantee Funds
After __24 tw__ of innactivity, a validator can submit a request to withdraw his validator deposit from the Dial treasury.

# The Dial Economy
Due to it open and permissionless character, the DialChain will need some sort of value generation system to address spam and sustainability.

## Value Generation
Every single service performed by a service provider (e.g. validator) in the Dial network is paid for by the requestor of that service. The price of each service is left to the discretion of the service provider. A __service intent request__ allows a requestor to collect prices and other execution conditions from different service providers.

## Spam Resistance
Spam is the main thread to open and permissionless architectures. The DialChain is built on top of a fundamental spam resistance system that makes sure the revenue generated from the publication of a single declaration is sufficient to cover present and future performance required to validate, maintain and retire that declaration.

In order to protect validators (or service provider in general), the DialChain requires each service request to be accompanied with a payment. Even the price inquiry service (a.k.a service intent request) is a payable service. Recall that the service intent request also returns a binding offer to the requesting party.

The price paid by a party to publish a declaration has a minimum cap, a file size factor and a validation effort factor. This price is generally substantial enough to have a significant impact on the wealth of the party generating spammy declarations.

These three factors (a) payment for intent request, (b) payment for publication and (c) the validator registration constraint constitute together an effective spam resistance mechanism.

## Sustainability Incentive
Traditional blockchain networks do not reflect on the future cost of current operations. Most blockchain networks are built on the speculation that the appreciation of the underlying crypto currency will motivate miners (validators) to stay in business. This is a risky approach as:

- This __currency appreciation based theory__ does not give miners the necessary accounting tools to legally build provisions for the future maintenance of those files.
- Letting a miner build a position in the miner's balance sheet does not prevent the miner from quitting when yield gets unattractive (due to increase of competition in the networks and among networks).
- Further, the massive growth of the blockchain size (block history) might make the entrance of new validators economically unattractive.

As the DialChain does not plan with future appreciation of the DIAL, reserves needed to maintain a declaration during the lifetime of that declaration is collected from the issuing party with the publication of that declaration. The collected revenue is held in the Dial treasury and distributed to validators for each tw of relevance of the concerned record.

## Value Added Tax (VAT)
In order to provide for sustainability, the Dial network must make sure every present operation is priced with future costs it incurs. For example:

- Each file inserted in the DialChain log will have to be maintained for a substantial amount of time (we presume 50 earth years).
- Each monetary value held by the Dial network will maintain a sound relationship to the corresponding external asset. For example, the BTC account held by the DialDAO will continouosly incure costs in the Etherum network.

The cost of maintaining those assets (log entries, currencies) is paid by the originating parties at the moment of publication of the declaration into the DialChain log. The Dial treasury will retain this amount from the revenue of the service provider (in the form of a VAT). This retained revenue will be spent by the Dial treasury during the lifetime of that token to pay for the maintenance of that token. For each block of maintenance of an asset, the corresponding maintenance fee will be distributed to the service providers of the network based on predefined distribution keys; sample key is the proportion of revenue generated during the block (e.g. earth hour).

# Monetary Policy
The Dial native economy does not create money. The Dial economy relies on the capabilities of existing crypto networks like BTC and ETH to work. 

## DialDAO
The DialDAO is the external treasury of the Dial network operated on the Etherum network. The DialDAO is simple and has no governance. Deposit and withdrawal rules are defined an never change.

## Liquid External Currencies
Money emission occurs as counter value to deposited external currencies into the DialDAO. External currencies deposited into the DialChain are mapped aggainst their Dial internal __L-XXX__ counterparts (L-BTC, L-ETH, L-MATIC, ...).

## Operation Currency
The DialChain will needs a currency to proceed with operations. At the beginning, the DialChain will be using L-BTC as the core operational currency. Service will then be paid in L-Satoshis.

## Native Currency
Dial will latter emit a native currency call DIAL whose value will be the mirror of external reserves held by the DialDAO. Therefore DIALs will be automatically produced and burned with the act of the DialDAO earning and spending external currencies.

# Liquidity Service
The liquidity service of the DialChain is a service provided by the Dial treasury that allows the mapping of external monetary values into the Dial network. Those values are generally denominated L-XXX, where XXX is the denomination known in the world outside of Dial. E.g.: L-BTC, L-ETH. Beside fees collected by the Dial treasury for the maintenance of those underlying records, the value of an L-BTC (Liquid Bitcoin) is a one-to-one mapping of the value of a Bitcoin.

In order to expose an external monetary asset to the Dial network, the asset has to be transfered to the Dial treasury.

## Depositing of Liquid-Assets
If we take the BTC as an example, a participant will simply emit L-BTC by depositing corresponding BTC amount into the Dial treasury. The purpose code of that transaction will be a public key identical to the declaration to be submitted by that same participant to the Dial network. Once the declaration is processed in the Dial network, the corresponding token is under the controll of the entity holding the matching private key. In other words, the deposited asset exists in the Dial network as a token.

## Breaking Down Liquid Assets
In the DialChain, an L-BTC Coin can be broken down into 10 Million 10-Satoshis Coins. This will happen in a transaction in which the controller of the L-BTC token generates 10.000.001 declarations, the first one to kill the L-BTC (erasing the controller block) and the subsequent 10Mio declarations to activate each 10 statoshis coin generated. Once this declarations are published, the holder of those satoshis can start spending them in the network, e.g. using them to pay for services.

If the breaking down of an L-BTC into 10 Mio satoshis exceeds the maximum file size, the controller of the L-BTC can consider taking an intermediary step. For example first breaking down the L-BTC into 1 coin of 90.000.000 satoshis and 1.000.000 coins of 10 satoshis. In this case the declaration file will contain only 1.000.002 files instead of 10.000.001 files.

Recall that each coin generated has a proper identifier (proper NFT). This will generally be the initial controlling public key. From there on, those coins can be moved arround by just submitting declarations that modify the controller block to bear the new public key controlling the coin.

The work of the validators of the break down declaration will consist in verifying that the conversion between 1 L-BTC and 10 Millions L-Satoshis is sound.

## Bundling Coins
As the publication of declaration files in the network are payable, it might be impractical to be using too many coins for large amount transactions. Using 500.000.000 declarations (spending each 1 satoshi) in a transaction that want to transfer 5 L-BTC might not work because of the file size. In some cases, the party holding too many small coins can bundle them by sending corresponding bundeling declarations to the network.

A bundelling declaration might not be easy to validate, as each token in the declaration file might have to be validated in a different neighbourhood.

## Withdrawal of Liquid-Assets
To withdraw from the DialDAO, the controller of a token jsut need to publish a modification of the token including the indication of an externnal payment account (e.g. bitcoin address) and the new controller as the target address of the DialDAO . For each closed tw, after the tw hash is generated, the DialDAO will run through the tw files and transfer all whithdrawn token to corresponding external addresses.

# Routers
One goals of the DialChain is to achieve the broadest possible decentralization. This can only be achieved by keeping the DialChain simple, such as to allow for common devices like mobile phones or IOT devices to play the validator role and therefore participate to the Dial economy.

Routers are Dial service providers that deploy simple communication infrastructure, that will allow network limited devices to act as first class citizen in the Dial network.

## Sensorship Resitence
Routers services will be simple enougth to allow for consumer grade home based computers with static ip addresses to be deployed and operated as routers. The operation of a router shall allow the owner to cover the cost of material and utility needed to operate the router. The service shall be simple enougth not to require special computer skill for the operation of router nodes.

## Simple Relay
Some routers will act as simple relay, allowing parties to exchange point to point messages with each other. Each message will off cource be associated with the corresponding payment. Payment collection and message delivery can be bundled into attomic transactions (atomic swap).

## Gateway
Some routers will play the role fo gateway for end user devices willing to participate to the validation protocoll. The gateway payment model will be negotiated between the gateway node and the end user device.

## Registration
Router can register their services with the network by submitting corresponding service declaration to the networt.

# File Services
These are the next enabling service for use in the Dial network. In order to keep validators simple, they are not required to maintain the whole state of the DialChain locally. The DialChain leverages the IPFS network to hold and maintain the history of the network. Files are generally referenced by their content identifiers, making them verifiable upon download.

## Registration
The DialChain will allow IPFS data nodes to register with the network as storage providers, providing their service and payment addrsses. The pricing policy for this service is left to the operator of the ipfs node.
