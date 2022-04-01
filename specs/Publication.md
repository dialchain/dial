# Publication
## Publicaion Process
### Verification Workflow
The following picture displays the life cycle of a declaration modifying a token, from the request for publication to the transfer of control to the subsequent time window. Solid lines cover the process from the submission of a declaration to the reception of the publication certificate by the submitting participant. Dashed lines describe operations performed at the closing of a time window.

![DIAL-WORKFLOW](../img/../specs/img/dial-workflow.png?raw=true&width=5)

Creating or modifying a token occurs by the mean of the current controller submitting a new declaration. To publish a declaration, (1) the current controller submits the declaration to one or more publishers of the token neighborhood (THost). (2) Addressed publishers verify the declaration and share the declaration with all other publishers of that neighborhood. (3) Each publisher of that neighborhood produces a certificate (PCert), (4) shares this certificate with other controllers of the same neighborhood and (5) returns the certificate to the submitting controller. The declaration is considered published when the submitting controller is in possession of at least one PCerts and zero rejection certificate. Publishing does not reflect successfull modification, as rejection certificates will also be published.

The picture above shows that each token is randomly validated by at least two neighborhoods. The neighborhood hosting the token in the current time window (THost) and the neighborhood hosting the token in the subsequent time window.

With the unpredictable distribution of publishers to neighborhoods and the possibility for a single publisher to uncover wrong doing, a group of malicious publishers must cover a substantial part of the network to successfully induce the illegitimate modification of a single token, as the group has to corrupt all publishers of two randomly built neighborhoods in subsequent time windows to achieve capability of corrupting a single token.

The highest assurance is provided, when control is transfered to publishers of the subsequent time window, as a second validation of each declaration takes place there.

### Closing a Time Window
As displaayed in the picture above, following activities are performed at the end of the time window.

- (6) Each publisher of the token neighborhood creates a neighborhood protocol and (7) sends that protocol to the time window host.
- (8) Each publisher of the time window host produces a time window protoccol, (9) shaare the TWP with all publishers of the time window and (10) shares it with the time window host a computed in the subsequent time window (TW+1)
- (10) Each publisher traansfers it's neighboorhood protocol (NP) to all publishers of the neighborhood host in TW+1
- (10) Each publisher tansfers each token under custody to all publishers of the neighborhood hosting the token in TW+1
- (11) Each publisher of TW+1 verifies the token again and publishes the token with the neighborhood host in TW+1
- (12) Each publisher of the neighborhood host inn TW+1 rebuilds the protocol and compare with the received protocol. Then transfers the protocol the the time window host in TW+1.

Each publisher of the time window host of TW+1 can reproduce the protocol from neighborhood protocols and compare it with the one delivered by publishers of the time window host in TW.


A publication is the act of a verifying a declaration and inserting that declaration into the Dial.

## Payment for Publication
### Publication of the Redeemed Coin
In order to redeem a coin earned publishing, each publisher must:
- transfer the VCert (resp. PCert) to all relevant publishers of the THost of the subsequent time window, within a minute after closing of the time window. The proof of transfer is a transfer certificate (TCert) produced by each publisher of the THost.
- bundle the TCerts (at least half +1) with the rediemed coin and submit them for publication to the coins relevant THost and NHost.
- The received PCerts are the proof of legitimacy of the coin and can allow the publisher to spend the coin.

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

This will motivate participant in holding a lot of coins so they can transact without having to generate new PoW tokens.

### Proof of Work based Payment
In the case were the requesting participant does not have a matching coin, the requesting participant can perform some work and use that __proof of work (PoW)__ to pay for the publication of the declaration.

The PoW performed for the payment of the publication has following properties:
- PoW must carry all details of the declaration to be published
- PoW must carry all details of the target neighborhood (timestamp)
- PoW must carry a conditional controller block with the public key of the addressed publisher
- PoW must provide an identifier hosted in the target neighborhood

The PoW document will be added a generated nonced to produce a hash that satisfies a defined difficulty (number of leading zeros).

The process of redieming the PoW attached to a publication request turns that PoW into a coin that can be spent by the publisher. The redemtion process is complete when publishers of the subsequent time window certify reception of the published record and coins are published in the subsequent time window.

