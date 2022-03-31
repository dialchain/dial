# DIAL White Paper
# Motivation
Web3 is struggling with finding the correct architecture. Fully mature and apparently decentralized applications appear to be giving way to censorship, because end user access to peer-to-peer networks are routed through API servers that are under the control of centralized organizations.

As we figure out that end user devices are not designed to be full citizen of peer to peer networks, API layers are establishing themselves as foundation for good user experience in Web3.

This paper describes a network that creates an economy for the deployment of scalable, open, permissionless and nano payment capable API networks. The latest opens room for the deployment of truly _decentralized_ and _censorship resistant_ web3 applications.

# Abstract
The Dial _(Distributed Immutable Assertion Log)_ is a distributed log holding state of tokens. A _token_ can be created or modified using a _declaration_ that contains a _proof of execution_ of the token controller script. Each token is (1) created or modified by the token _controller_, (2) verified and certified by many _validators_.

Each verification act is documented in a _certificate_ whose hash is part of the Dial _protocol_. Certificates are held by controllers and Dial protocols are held by validators. The overall state of the Dial at any given _moment_ is therefore distributed among controllers and validators.

To allow for the parallel proccessing of tokens, the Dial scales by _partitioning_ validators of into groups called _neighborhoods_. A simple and deterministic algorithm allows the location of the group of validators responsible for any given token.

As the Dial is open and permissionless, validators might join and leave at will. This opennes justifies the requirement not to keep the last state of a token with a single group of validators for an unlimited amount of time. The _transfer of responsibility_ to other validators is implemented by defining time slices called _time windows_. Each time window starts at the _UTC Hour_ and ends before the next _UTC Hour_. At the end of a time window, the last state of each token is passed by the current validators of this token to new validators the token. At the begining of each time window, all validators cordinate to produce an opening protocol documenting the last state of all tokens.

Neighborhoods are reshuffled at the beginning of each time window. Inside the time window, each token is assigned to exactely one neighborhood. This way, changes on a single token inside a time window are all verified by the same set of validators, thus preventing the certification of conflicting changes. 

The Dial _sustainability policy_ requires each token to be associated with payments substantial enough to maintain the token toward its expiration. Part of the total value held by the Dial is released to validators as each time window closes, making this the motivating factor for validators to join and service future time windows.

# Principles

## Proof of Work (PoW)
The open and permissionless nature of a network leaves room for opportunistic behavior and/or spam. For that reason, the Dial relies on the proof of work as an effective way of conditioning permissionless participation.

Each request to the Dial is required to provide a payment, either in form of coins or in from of the proof of performance of a difficult computational task (so called proof of work). The amount of the  required payment is set by the Dial such as to prevent spam.

As the Dial __monetary policy__ allows the conversion of PoW into coins, both coins and PoW are seen as equivalent means of payment in the Dial.

## Reputation Token
A reputation token is a cumulated reward for participation and honest behavior. Whenever a participant pays for the execution of a service, the value of the payment is added to a reputation token (if provided by that participant).

A reputation token, as an aggregation of the PoW performed so far, can be seen as some sort of capital that can be used by it's controller:
- as a collateral to guaranty honest behavior and promissed availability of a validator,
- as a support for the reduction of the PoW required for a given request,
- as a collateral to mitigate counter party risk in a contract.

Event though a reputation token can be traded:
- the Dial does not convert reputation tokens into coins,
- the Dial does not aggregate reputatioon tokens.

When used as support or collateral, verifiable misbehaviour of the controlling participant will lead to the lost that reputation.

## Sustainability
Each token in the Dial carries a monetary value measured in number of work units _wu_ (resp. reputation unit _ru_). Moving a token from one time window to another consumes one _work unit_ (resp. one _ru_). As each token pays for it's own maintenance, a token with a work unit value of zero will be considered _expired_ an not further maintained by Dial validators.

This auto sufficience property of each token:
- is essential for the simplicity of the Dial, as there is no cross token interaction,
- allows the Dial to reduce the log to active tokens only,
- relieves the Dial from the necessity of maintaining a common treasury.

## Participant Opportunistic Behavior
A participant controlling a token is assumed to have sole control on corresponding key credentials. Submitting conflicting declarations to the Dial can occur by the mean of the participant sending different versions of that declaration to validators. Even though this attempt will never succeed due to coordination rules implemented by neighborhoods, the submitting participant will lose the payment associated with the declaration. If this payment is a PoW sponsored by a reputation, the submitting participant will also loose that reputation.

## validator Opportunistic Behavior
Despite participants, which are given less room for opportunistic behavior, validators are given the priviledge to:
- convert proof of work into coins,
- aggregate payments into reputations,
- verify and certify creation and modifications of tokens,
- verify and certify token operations (aggregation, split).

### Collateralizing the validator Service
As the Dial is open and permissionless, it does not expect any integrity from validators. The publishing service is collateralized with a substantial enougth reputation that will be lost if verifiable misbehavior of a validator is uncovered. The collateral of a publishing session is held during the entire subsequent session, thus giving all participants the time to discover and expose misbehavior of the closed session.

Even though the Dial does not keep the change history, participants can archive past certificates and protocols for the purpose of:
- providing them to other participants against payment,
- uncovering weaknesses and loopholes in the Dial coordination workflow,
- uncovering validators misbehaviors.

If a misbehavior is exposed in the given retention time of the collateral, the acting participant will be rewarded with part of the collateral (reputation) attached to the transaction, the rest will be lost (burned).

### Publication and Rejection Certificate
A _publication certificate_ is returned by a validator to the submitting participant as a commitment for inclusion of the creation or modification request into the Dial. A _rejection certificate_ tells a participant, that a creation or modification request is either not valid, or conflicting.

As declaration are always signed and acompanied with payment (resp. PoW),
- A declaration with invalid payment (PoW) is not proccessed,
- An invalid declaration with valid payment is processed, as validator will collect the payment for the verification and documentaion of the invalid request.

A participant can consider a token published if none of the custodying validators returns a rejection certificate.

### Hijacking a Neighborhood
A group of related validators could cordinate their effort in neighborhoods they controll to perform illegitimate modifications on tokens. Recall a neighborhood can only be controlled if all validators of the neighborhood are controlled, as a single controller issuing a rejection certificate will uncover the intended illegitimate modification. 

To prevent controll of neighborhood by validators, the Dial's _Ephemeral Neighborhoods Protocol (ENP)_ secures a deterministic but unpredictable association between each token and the neighborhood responsible for the validation of changes on that token in the given time window.

### Publication Workflow
The following picture displays the life cycle of a declaration modifying a token, from the request for publication to the transfer of control to the subsequent time window. Solid lines cover the process from the submission of a declaration to the reception of the publication certificate by the submitting participant. Dashed lines describe operations performed at the closing of a time window.

![DIAL-WORKFLOW](./img/../specs/img/dial-workflow.png?raw=true&width=5)

Creating or modifying a token occurs by the mean of the current controller submitting a new declaration. To publish a declaration, (1) the current controller submits the declaration to one or more validators of the token neighborhood, (2) addressed validators verify the declaration, produce each a certificate (PCert), share this certificate with other validators of the same neighborhood and return the certificate to the submitting controller. The declaration is considered published when the submitting controller is in possession of at least one PCerts and zero rejection certificates. Publishing does not reflect successfull modification, as rejection certificates will also be published.

The picture above shows that each token is randomly validated by at least two neighborhoods. The neighborhood hosting the token in the current time window and the neighborhood hosting the token in the subsequent time window.

With the unpredictable distribution of validators to neighborhoods and the possibility for a single validator to uncover wrong doing, a group of malicious validators must cover a substantial part of the network to successfully induce the illegitimate modification of a single token, as the group has to corrupt all validators of two randomly built neighborhoods in subsequent time windows to achieve capability of corrupting a single token.

The highest assurance is provided when control is transfered to validators of the subsequent time window, as a second validation of each declaration takes place there.

### Transfer Control to the Next Time Window
As displayed in the picture above, following activities are performed at the end of the time window.

- (4) Each validator of the token neighborhood creates a neighborhood protocol.
- (5) validators compute the time window protocol (TWP) pairing up in a cordinated way to exchange hashes and aggregate nodes that will lead to the merkel root of the time window.
- (6) The time window protocol is distributed to all validators of the time window.
- (7) Each validator tansfers each token under custody to all validators of the neighborhood hosting the token in TW+1, including corresponding protocols and certificates.

After receiving all tokens from TW, validators of TW+1 cordinate to produce opening neighborhood and opening time window protocols. If there is any discrepancy between validator on the state of an opening protocol, Dial defined majority rules will be used to decide on which version of the  protocol to keep.

# Time Window
The following image displays a simplified layout of a time window.

![ENP](./img/../specs/img/dial-ENP2.png?raw=true&width=5)

The Dial is always inside a time winndow. The time window is the primary element of synnchronizationn in the Dial network. It is represented with the keywork TW and the timestamp of the first second of the UTC Hour _TWYYYYMMDDHH_ e.g. _TW2022032415_. Each Participant can compute this identifier without any additional information.

## Time Window Anchor
The _anchor_ is the most critical information of the Dial. The anchor of a time window is a _hash_ of the state of the Dial at the end of the 56th minute of the precedent time window.

The _anchor_ is used to:
- partition validators of the time winndow into neighborhoods
- determine the neighborhood hosting a token

The _anchor_ is :
- computed in a coordinated effort among neighborhoods (distributed merkel tree)
- verified by and known to all validators.

If there is any dispute durring the computation of the anchor, majority rules set by the Dial will be used to decide on which value to keep.

## Neighborhood
A neighborhood is a set of validators commonly responsible for the guardianship of a set of tokens inside the given time window. 

The list of validators registered for performance in the next time window is propagated together with the construction of the neighborhood protocol. The same way the neighborhood hashes are incrementaly aggregated up the tree to compute the time window hash, the list of validators registered with the subtree inncluding it's hash is propagated up the merkel tree.

The layout of neighborhoods in a time window can then be computed by any given participant holding the time window hash and the list of registered validators.

As displayed in the picture above, both validators and tokens are assigned to neighborhoods by computing their respective _distances_ to the anchor.

Each neighborhood has the same number of validators. In this case 11 validators. The remaining group of validators less than 11 does not serve for the given time window.

## Token and Declaration
A declaration can be submittet by a participant to create or modify a token.

## validator
The entity responsible for the publication of a declaration into the Dial is called a _validator_. Before insertion into the Dial, validators of the neighborhood responsible for this token verify that the submitted declaration is consistent with the state of the token as documented so far.

To act as a validator in the time window _TW+1_, a validator must register for performance in time window TW before the 56th minnute of the current time window _TW_.

# Certificates
A certificate is a validator signed doccument, that can be presented by the particcipant to support a claim.

## Publication Certificate (PCert)
A publication certificate is a proof that the resulting state of the referenced token is consistent with the state of the token as documented so far. A PCert is produced by a validator and returned to the controller of the token for documentation. A PCert is also transfered by the producing validator to the hosting validators of the subsequent time window (as soon as this last one is known).

## Transfer Certificates (TCert)
A transfer certificate is a proof, that a validator has passed the held protoccols and certificates to the relevant validator of the subsequent time window.

To enforce transfer of produced certificates, redemption of coin associated with work done in a time window only happens if validator presents corresponding TCerts.

# Protocols
A protocol is a merkel tree documenting modification on one or multiple tokens. 

## Principles
### Incremental Computation of Merkel Root
Both neigghborhood and time window protocols are computed at the opening and/or closing of a time window and computation must be very efficient to allow for seamless availability of the Dial.

Because protocol are all merkel trees, they can be computed incrementally if the Dial designs the ordering criteria of each protocol to prevent rebalancing of the merkel tree upon modification or insertion of new elements.

### Protoccol as Synchronization Vehicle
Beside the purpose of documenting changes on tokens, nodes of intermediary protocols are constantly circulated among validators to synchronize the state of changes among each other.

### Multi Phase Synchronization Scheme
In many situations, knowledge on the work performed by a validator might be used by another validator to extract illicite value out of the Dial. This would be the case if a group of validators where entrusted with the task to produce the time window protocol. They might forge some tokens, with the purpose of achieving an intended value of the time window hash, thus influencing the layout of the subsequent time window.

The Multi Phase Synchronization Scheme can be applied by a group of validators to implement a sound synchronization.
- In the first phase, each validator sends the merkel root of his state to all other validators of the group.
- In following phases, validators synchronize each order state down the tree till diverging leafs are available to all validators.

### Protocol Discovery
Protocol identifiers are generally made out of the underlying entity identifier and the timestamp of the protocol. Beside token, all other entities like time windows, neighborhoods have conventional identifiers, that can be computed by each particpant.

## Typeof Protocols
The Dial knows three types of protocols:
- the token protocol,
- the neighborhood protocol, and 
- the time window protocol.

### Token Protocol (TP)
A token protocol is a merkel tree documenting all certificates produced to secure the state of a token. The token protocol is held by validators as part of the neighborhood protocol. Leaf nodes of the token protocol are hashes of publication certificates. 

Publication certificates are:
- held by publishhers as they will be transfered to validators of the subsequent token neighborhood,
- held by the controller of the token, as they will be presented to validators with the next declaration to modify that token.

By verifying the inclusion of the controller provided certificate in the merkel tree of the token,the validator can trust and consume information contained in the submitted modification request.

### Neighborhood Protocol (NP)
A neighborhood protocol at a given moment is the merkel tree of the last state of all tokens hosted by the target neighborhood at the given moment. It is produced in a common effort by all validators of the target neighborhood.

To allow for incremental computation of neighborhood protocols, leaf nodes are ordered by (1) the timestamp of the token first publication and (2) the lexicographical order of the token identifier. This way, new tokens are appended at the end of the list and do not trigger a rebalance of the protocol tree.

Each leaf node contains three values:
- the token identifier (for new token prefixed with the token insertion date),
- the hash of the token state
- the hash of the validator issued certificate

The token protocol can be computed for any given minute. During the minnute, each validator:
- maintains a tree of self produced certificates (cert tree)
- maintains a tree with the known last state of each token of the neighborhood (token tree).

At the end of the target minute, each validator shares the merkel root of it's cert tree with all other validators. After all validators are in possession of all cert trees, they can synchronize their certificates with each order a no new certificate can be produced upon knowing certificates produced by other validators.

### Time Window Protocol (TWP)
A time window protocol is the merkel tree of all neighborhood protocols hosted by that time window. 

As the list of neighborhoods of a time window is known in advance, the merkel tree of a time window is built in a parallel and distributed maner. The cordination algorithm determines which validators collaborates and shares data with other to achieve the fastest route to a time window protocol.

## Anchor
### Computing the new Anchor
Intermediary Neighborhood Protocols (INP) are computed during the 57th minute of the time window and contain (1) the state of all unchanged tokens and (2) the state of all changed tokens from the first to the 56th minute. The INP must be available before the end of the 57th minute.

Aspiring validators of time window TW+1 must register for performance in TW, before the INP is computed. This list of registered validators for TW+1 is circulated with the INP during the coordinated construction of the intermediary time window protocol in the 58th minute. The identifier of an INP follows the pattern: _INP-YYYYMMDDHH-I_ where _YYYYMMDDHH-I_ is the suffix of the neighborhood. 

The Intermediary Time Window Protocol (ITWP) is computed and distributed in the 58th minute of the time window. The identifier of an ITWP follows the pattern: _ITWP-YYYYMMDDHH_ where _YYYYMMDDHH_ is the suffix of the time window. 

The ITWP is used to determine the intermediary time window hash __(ITWH)__, which is the merkel root of the ITWP. The ITWH is available from the 59th minute of the current time window and is used as the anchor of the subsequent time window.

After the ITWH of TW is computed, each validator of TW is in possession of the ITWH and the list of validators of TW+1 and can use both information to compute the layout of TW+1.

In the first minute of TW+1, validators of TW start transfer all tokens to relevant validators in TW+1.

Upon receiving all tokens, validators of each neighborhood of TW+1 each verify each token and compute the neighborhood opening time window protocols. The identifier of a opening neighborhood protocol follows the pattern: _ONP-YYYYMMDDHH-I_ where _YYYYMMDDHH-I_ is the suffix of the neighborhood.

In a cordinated effort, validators of time window TW compute the opening time window protocol (OTWP). As soon as this is available, each token of TW is sent (toghether with CNP) by the holding validator to validators of the custodian neighborhood in TW+1. The identifier of an OTWP follows the pattern: _OTWP-YYYYMMDDHH_ where _YYYYMMDDHH_ is the suffix of the time window.

The following picture illustrate both a time window protocol and attached neighborhood protocols.

![Protocols](./img/../specs/img/dial-protocols.png?raw=true&width=5)

### Verifying a Token
To validate a token at the end of a given time window, two partial merkel trees (PMT) are required:
- The PMT of the opening neighborhood protocol hostig the token in the subsequent time window
- The PMT of the opening time window protocol.

Knowing the identifier of each of these documents, a participant can locate where to download the documents in the current time window.

# Monetary Policy
Each coin in the Dial originates from a combination between a __Proof of Work__ and the __performance__ of a __canonical service__.

## Proof of Work (PoW)
The PoW is designed to enforce a relation between the value extracted from of a service consumed and the effort performed to legitimate the service request. A balanced relationship between the effort performed (input) and the value extracted (output) will discourage a participant from spamming the Dial.

## Mining Coins out of PoW
The Dial allows a participant to perform some computation intensive work and use the resulting proof (PoW) to pay for the execution of a Dial service. The service execution process transforms the provided PoW into a Dial coin. This resulting coin is subsequently used in the Dial network as a mean of payment.

## Reputation
The reputation of a participant is the cumulated amount of PoW performed by that participant so far. As described above, the reputation exposes the participant to privileges:
- the registration as a service provider requires a participant to provide a ccertain reputation it controlls.
- the amount of PoW required to submit a publication request is an inverse factor of the reputation of the submitting participant. The bigger the reputation of a participant, the lesser is the PoW required from the participant for the submission of a publication request.
- the reputation of a participant can also be attached to some operations as a guaranty of not double spending. Speeding up the off chain transaction of token and increasing the annonymity of the overall echo system.
- Reputations are integral part of the monetary policy as reputation are tradable value object.

## Supply Cap
The Dial monetary policy does not set a supply cap, but designs the proof of work (PoW) such as to have the Dial supply reflect the volume of activity performed in the Dial network:
- the PoW required for a service is set such as to have the work done consume resources equivalent to the monetary value to be paid for the same service. As devices get powerfull, PoW will be addjusted to service it original purpose. 
- the PoW performed includes details on the service request and on the target time window. This means a PoW generaated for a service request can not be reused for another service request, thus preventing the development of a secondary PoW market.