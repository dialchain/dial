# Publication
A publication is the act of a verifying a declaration and inserting that declaration into the Dial.

## Publicaion Process
### Controller Activities
Any participant can submit a declaration for the creation of a new token. A controller of an existing token is a participant that can prove the execution of the controller script of that token. The publication process proceeds as follow:
- the requesting participant uses the token identifier to determines the neighborhood hosting the token (THost).
- the requesting participant uses the neighborhood identifier to deteremine the neighborhood hosting the THost (NHost)
- For each publisher of the THost, the publisher provides a payment declaration transfering control over a payment token to the target publisher. This payment token can be either a PoW or an existing coin. In both cases, the identifier of the payment token must be chosen such as to be hosted in the same THost as the main token. This is important to allow THost publishers to verify legitimacy of the paayment token without additional effort.
- For each publisher of the NHost, the publisher provides a payment token issued to the publisher. This payment token can be either a PoW or an existing coin. In the same rationale like for publishers of the THost, the identifier of the payment token must be chosen such as for those token to be hosted in the same neighborhood as THost. 
- The requesting participant produces a declaration
- The requesting participant signs the declaration:
  - If this is a new declaration, the participant signs the declaration using a private key that matches the hash of the public key used to identify the token.
  - If this is a modification, the participant provides the proof of execution of the script referencedin the controller block of the token.
- the requesting participant submits the bundled declaration to all publishers of the THost. A bundled declaration contains:
  - the maain decclaration (creating or modifying a token)
  - all payment declarations transfering payment token to publishers
  - for each modifying declaraation the controller scrypt of the referenced token. As only the hash of this controller scrypt is documented in the Dial.

### Activities of THost Publishers
Each publisher of the THost upon reception of a publication request,
- proceeds with the formal validation of the contained declaration (mandatory information like ID), then
- matches the declaration against the current state of the token (controller identifier),
- proceeds with the verification of control rules (proof of execution of the current controller scrypt), then
- produces a verification certificate (VCert) and forward it to all publishers of the NHost

### Activities of NHost Publishers
Each NHost publisher upon reception of more than half of the VCerts,
- verifies the legitimacy of all VCerts including the majority rule,
- enforces the verification of remaining publishers of the THost if missing,
- produces a publication certificate (PCert) and returns it to the requesting participant.

The declaration is considered published when the controller (requesting participant) holds more than half of the PCerts.

## Payment for Publication
### Publication of the Redeemed Coin
In order to redeem a coin earned publishing, each publisher must:
- transfer the VCert (resp. PCert) to all relevant publishers of the THost of the subsequent time window, within a minute after closing of the time window. The proof of transfer is a transfer certificate (TCert) produced by each publisher of the THost.
- bundle the TCerts (at least half +1) with the rediemed coin and submit them for publication to the coins relevant THost and NHost.
- The received PCerts are the proof of legitimacy of the coin and caan allow the publisher to spend the coin.

The process of publishing an earned payment is called a called a coin based operation. These coin based operations do not require proper payment.

### Types of Payment
There are two type of payments for the publication of a declaration sent to the Dial:
- the sending participant can attach coins to the declaration, in which case the publisher will redeem the coin attached to the publication request.
- The sending participant can attach proofs of work to that declaration, in which case each publisher will mine a new coin associated with a PoW attached to the publication request.

### Coin based Payment
Using a coin for the payment of a publication service is tricky in that, the coin has to carry an identifier hosted __in the same neigborhood__ as the main declaration's underlying token. This means the publisher produces two publications at the same time:
- the conditional publication advertizing the payment
- the publication certifying the main declaration

In order to pay with a coin,
- the requesting participant has to have a coin
- the coin has to carry an identifier that falls in the same neighborhood as the main payment

This will motivate participant in holding a lot of coins so they can transact without having to generate new of PoW tokens.

### Proof of Work based Payment
In the case were the requesting participant does not have a matching coin, the requesting participant can perform some work and use that __proof of work (PoW)__ to pay for the publication of the declaration.

The PoW performed for the payment of the publication has following properties:
- PoW must carry all details of the declaration to be published
- PoW must carry all details of the target neighborhood (timestamp)
- PoW must carry a conditional controller block with the public key of the addressed publisher
- PoW must provide an identifier hosted in the target neighborhood

The PoW document will be added a generated nonced to produce a hash that satisfies a defined difficulty (number of leading zeros).

The process of redieming the PoW attached to a publication request turns that PoW into a coin that can be spent by the publisher. The redemtion process is complete when publishers of the subsequent time window certify reception of the published record and coins are published in the subsequent time window.

### Reputation
The constraint of haaving the coin identifier match the neighborhood of the main token reduces the chance of using mined coin to pay for publication. IT encourages the generation of new PoW for the publication of declarations.

Using it reputation, a participant can invest less work in generating the PoW needed to publish declaraations. This increases the importance of reputations in the monetary policy of the Diaal and discourages misbehaviors.
