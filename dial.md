# DIAL White Paper
The DIAL stands for __Distributed Immutable Assertion Log__.

# Abstract
The Dial is a distributed log with the main purpose of turning each inserted __declaration__ into an __immutable assertion__. The Dial can be seen as a log holding state of __tokens__. Tokens can be used to represent anything addressable. A token is (1) created or modified by the token __controller__, (2) verified, certified and published by many __publishers__.

The Dial defines time slices called __(time windows - tw)__. Each time window starts at the __UTC Hour__ and ends before the next __UTC Hour__. A day has 24 time windows __(tw-0, ..., tw-23)__. At the end of a time window, all publishers share the same state of the Dial. All declarations published during a time window are part of that time window's protocol. 

# Shallow Dive

## Time Window - Declaration - Token
A time window identifier can be represented by a string starting with TW an the formated date time YYYYMMDDHH. The following picture displays 3 time windows in which the same token is modified using declarations. 

![DIAL](./img/../specs/img/dial-decl-token-tw.png?raw=true&width=5)

The first declaration (Declaration-0) creates the token. Subsequent declarations modify the token. Like displayed in TW2022031015, a token can be modified more than once in a single time window.

The entity responsible for the publication of a declaration into the Dial is called a publisher. Before insertion, the publisher verifies that the submited declaration is consistent with the state of the token as documented so far.

## Neighborhood
In order to allow for parallel publications, Dial publishers are partitioned into ephemeral neighborhoods. The __Ephemeral Neighborhoods Protocol (ENP)__ secures a deterministic but unpredictable association between each token and a group of publishers (neighborhood) responsible for the publication of changes on that token during the hosting time window. A neighborhood exists only for the life time of the hosting time window. The __layout__ of a time window is the complete set of all neighborhoods hosted by that time window, as presented in the following image (simplified to 2 dimensions for visualization).

![ENP](./img/../specs/img/dial-ENP2.png?raw=true&width=5)

### Distance Vector Mapping
As displayed in the picture above, both publishers and tokens are assigned to neighborhoods by computing their respective __distance__ to the time window __anchor__. The time window anchor is the merkel root of the preceeding time window.

### Token's Hosting Neighborhood
A token is said to be __hosted__ by a neigborhood if the ENP assigns that token to that neighborhood in the hosting time window. The neighborhood hosting a token is called __THost__.

### Time Window's Hosting Neighborhood(TWHost)
The time window itself can be considered a token with the reserved identifier TWYYYYMMDDHH. The distance between the hash of this identifier and the anchor can alow us to locate the neighborhood responsible for hosting the time window. This neigborhood is called the __TWHost__ and is responsible for the publication of the time window protocol.

### Neighborhood's Hosting Neigborhood (NHost)
In the same logic as the time window, each neighborhood has a unique identifier carrying the id NYYYYMMDDHH-I where YYYYMMDDHH is the sufix of the hosting timewindow, and I ist the position of the neighborhood relative to the time window anchor.

The distance between the hash of this identifier and the anchor can alow us to locate the neighborhood responsible for hosting thaat neighborhood. This neigborhood is called the __NHost__ and is responsible for the publication of the neighborhood's protocol.

# Publication Protocols
## Publication Certificate
A declaration is considered published when a controller can present enougth publication certificates __(PCert)__. In order to obtain PCerts, a controller must (1) send the declaration for verification to all __n__ publishers of the THost. Upon receiving __(n/2)+1 verification certificates (VCert)__, the controller must bundle the VCerts and send them to all __k__ publishers of the NHost for insersion into he neighborhood protocol. Each publisher of the NHost returns a __Publication Certificate (PCert)__ to the controller. The declaration is considered published when the controller is in possession of __(k/2)+1__ PCerts.


## Sharing Certificates
All publishers of a neighborhood are required to share each produced certificate (VCert, PCert) with each other not later than in the __minute__ following the production of those certificates. This is essential as the earliest knowledge of each certificate will reduce the certification of conflicting declarations and help reduce noice and spam in the network.

In order to enforce sharing of produced certificates, redemtion of coin associated with work done, can only happen, if publisher shows __proof of deposition__ of produced certificates (in the inbox of other publishers).

## Neighborhood Protocol (NP)
A NP can be built out of all complete PCerts. Whereby a PCert is considered complete if produced by more than half of the publishers of the NHost.

### Incremental Computation of Merkel Tree
The NPs merkel tree is built out of the ordered list of all tokens of the neighborhood. Entries are ordered by (1) the timestamp of the tokens first publication and (2) the lexicographical token identifier. This strict order allows for the incremental computation of the merkel tree, as there is no need to rearrange the merkel tree when a declaration for the creation or modification is sent to the neighborhood.

### Intermediary Neighborhood Protocol (INP)
The INP is computed during the 57th minute of the time window and contains all PCerts from the first to the 56th minute. The INP must be sent to the TWHost before the end of the 57th minute.

## Time Window Protocol (TWP)
The TWP is the merkel tree of all corresponding NPs merkel root (a.k.a NH).

### Intermediaary Time Window Protocol (ITWP)
The ITWP is computed in the 58th minute of the time window and distributed in the 59th minute of the time window. It is used to determine the intermediatry time window hash __(ITWH)__, which is the merkel root of the ITWP.

The ITWH is available from the 59th minute of the current time window and is used as the anchor of the subsequent time window.

### Restriction on New Token
The Dial does not allow the production of new tokens in the last three minutes of a time window. As the cutoff for the computation of the new anchor is the 56th minute.

### Final Neighborhood Protocol (NP)
The final neighborhood protocol is computed in the first minute of the subsequent time window by publishers of NHost. The change date is the last second of the old time window. NP are sent to the old TWHost for documentation, as the change is hapening in the old time window.

### Final Time Window Protocol (TWP)
The final time window protocol is computed in the third minute of the subsequent time window by the TWHost (of the old time window) and documented as such.

This TWP is then markedwith the timestamp of the first second of the new time window and sent to the relevant THost of the new time window  for documentation (The saame way any token get published).

## Verifying the State of a Token

### Locatting Protocols
There is no requirement of having a single location where to store protocols. Each publisher is responsible for passing the protocol to relevant publishers of the subsequent time window.

Holding the protocol is an economic activity, as publishers are paid to release protocols. Because protocols are signed by publishers, protocol holders can also release full or partial trees to requestors against payment.

As NP and TNPs are tokens with well defined identifiers, it is always easy to compute the address of the neighborhood hosting them.
- NPs are only existent in their time window of origine.
- TWP are available:
  - as closing protocol in their neighbohood of origin
  - as openning protocol in the subsequent neigborhood

Therefore, keeping publishers of two consecutive time windows active is enougth to have access to all relevant protocols.

### Locating Neighborhoods
Knowing the anchor aand the number of publisher per neighborhood, a simple formula can be used to compute the neigborhood's boundaries.

### Accessing Partial Merkel Trees
The folowing picture illustrate both the neigghborhood's and the time window protocols.

![ENP](./img/../specs/img/dial-protocols.png?raw=true&width=5)

### Validating a Token
In order to validate a token:
- locate the current time window __(TW2022031016)__
- locate the previous time window __(TW2022031015)__
- read the previous anchor __(A2022031015)__
- use the token identifier and the anchor to compute the neighborhood __d(A2022031015, tokenId)=N2022031015-76__
- read the neighborhood partial merkel tree __pmt0=pmt(N2022031015-76, tokenId)__
- read the previous time window's partial merkel tree for the neighborhood __pmt1=pmt(W2022031015, N2022031015-76)__
- Verify that both partial merkel trees re clena given the token state
  - verify that the neighborhood hash is correct __NH2022031015-76==pmtHash(pmt0, tokenState)__
  - verify that the time window hash is correct __TWH2022031015==pmtHash(pmt1, NH2022031015-76)__

# Token and Declaration
A declaration is a document used to create or modify a token. For this purpose, each declaration exposes a controller property that defines modification rules of the underlyinng token.

## Structure of a Declaration
A declation is made out of a header and a token payload.

### Declaration Header
The declatation header only contains information relevant for the publication of that declaration:
- the token identifier (ID, final, unique)
- the controler identifier (CTL)
- the expiration date (EXP)
- the token paylod content identifier (CID). The payload of a token is not exposed to the Dial.
  
### Token Payload
The token payload is the information describing the token. It is generally specific to the application using the token. In some use cases (like managing monetary values, token payload might be well known vaalues, set by the application layer to represent type and/or value of coins).

## Creating a Token
A token is created by providing a declaration with a new public key hash. The declaration is signed with the corresponding private key. In order to be modifiable, a token must be created with a controller property.

The publisher of a new declaration must only verify that the declaration is correctly signed with the private key of the public key used to build the token identifier.

## Modifying a Token
In order to change the token (properties CTL, EXP, CID), the current controller must sign and submit a declaration for publication.

## Publishing a Declaration
The purpose of the Dial is to finalize declarations by publishing them in the Dial. Publishing is done by applying following rules:
- Anyone can submit a declaration to create a token. Creator must sign the initial declaration with the private key matching the declaration identifier.
- Once created, only the latest controller of a token can sumit a modification on the token by signing the modifying declaration with the private key matching the identifier of the controller property (CTL) of the token.

In order to publish a declaration,
- The controller of the underlying token submits the declaration to all publishers of the neighborhood for that token (THost).
- A THost publisher upon reception of a publication request,
  - proceeds with the formal validation of the contained declaration (mandatory information like ID), then
  - matches the declaration against the current state of the token (controller identifier),
  - proceeds with the verification of control rules (signature of the current controller), then
  - produces a verification certificate (VCert) and returns it to the requesting participant. 
- The controller upon receiving more than half of the responses (VCerts), submits the declaration for publication to all publishers hosting the token's neighborhood (NHost)
- An NHost publisher upon reception of the publication request,
  - verifies the legitimacy of all included VCerts including the majority rule
  - enforces the verification of remaining publishers of the THost if missing
  - produces a publication certificate (PCert) and returns it to the requesting participant

The declaraation is considered published when the controller (requesting participant) holds more than half of the PCerts.

# Ephemeral Neightborhood Protocol (ENP)
ENP secures a deterministic association between each token (existing or new) and a group of publishers responsible for that token during the given time window. The deterministic association of tokens to neighborhoods is essential for the serialization of movement of tokens acros time windows and preventconflicting state of tokens.

## Assigning Publishers to Neighborhood
Publishers are entities responsible for the security of the network. A publisher can join and leave the Dial at will. The commitment to participate in the publication process of a time window is nevertheless binding. A publisher must explicitly announce it's intention to participate for time window __tw__ with a declaration he publishes in time window __tw-2__. This mean after tw-2 is sealed during __tw-1__, all publishers for __tw__ are known. The list of publishers of tw is held

The __neighborhood__ building process is a simple, but deterministic algorithm that can be performed by any device. In order to make the neightborhood distribution of tw non predicatable, the partitioning algorithm consumes the last __ITWH__ ot tw-1, even though publishers are known at the end of tw-2.

## Availability of Publishers and Protocols

### Publisher Availability Commitment
The credit for hosting a token is only awarded to a publisher after active transmission of the token to each publisher of the next hosting neighborhood.

A publisher of time window __tw__ is comited to be available during time windows __tw+1__ to (1) actively push each hosted token to the next hosting neighborhood and (2) supply any requestor with protocols __tw__ (NP, TWP, ITWH, ...).

### Protoccol Availability Commitment
The protocol of a neighborhood contains the list of all tokens assigned to that neighborhood, independent on whether the token was modified in that neighborhood or not. A a neighborhood has a life time of 1 hour, publishers of a neighborhood have the time to incrementally collect and compile the last state of all token assigned to that neighborhood.

Based on this assumption, the Dial only need the protocol of the last time windows to be fully functional. No publisher is required to hold more than the information it needs for the validation publication of hosted tokens during the given time window.

## Joining the Network
Each publisher is known to the network and is represented by a token. The publisher performance declaration must be renewed for every time window. The publisher performance declaration contains the publisher's service addresses.

A publisher will generally need three time windows to start performing:
- In __tw-3__ the publisher submits its declaration of existence. This will be validated and published with this time window.
- During __tw-2__ the new publisher announces its intent to publish for __tw__ by submitting a modification to the network, announcing it's intent to publish. This intent is part of the protocols of tw-2.
- During __tw-1__, __tw__ publishers observe the network, collecting the addresses of all other publishers of tw from the corresponding NHost of tw-1.
- After the ITWH of tw-1 is published (anchor of tw), each publisher of tw-1 and tw computes the __layout of tw__ (neighborhood distribution). 
- In the first minutes of tw, tw-1 publishers actively rediem their coins pushing tokens and protocols to corresponding THost and NHosts of tw.
- In __tw__ THost and NHost publisher take over their duty.

## Leaving the Network
In order to leave, a publisher just needs to stop announcing itself for future time windows. As the declaration of readiness for publication in a time window muss occur actively, an innactive publisher will never be a problem for the network.

# Locating Network Information

## Time Window Anchor (TWA => A-YYYYMMDDHH)
The TWA of time window tw ins the intermediary time window hash (ITWH) of tw-1. It is the snapshot of the state of the 56th minute of tw-1. Therefore ITWH-2022031115==A-2022031116. This information is generally available to all participant of the network aand shall be circulated as metainformation among network participants.

## Closest Neigborhood (N-YYYYMMDDHH-0)
The neighborhood closest to the anchor carries the identifier N-YYYYMMDDHH-0. This neighborhood host information on the layout of the time window. The service address of all publishers of this neighborhood is known by default and shall be circulated as meta information using a gossip protocol in the network.

Each publisher of this neighborhood offers following services:
- Provide identifier of last neighborhood. e.g N-YYYYMMDDHH-2543 if this time window has 2543 neighborhoods.
- Provide the neighborhood identifier given a distance to the anchor.
- Provide the list of neighborhood publishers and the neighborhood boundaries given a neighborhood identifier.

These three services are generally sufficient to allow a new participant to hook into the Dial publication process.

## Neighborhood aas Host of Protocols
The logic of the Dial is generic in that Dial native component like neighborhoods and time windows are also considered token (with reserved identifiers). In order to locate an information, in the dial network, a participaant needs:
- the anchor (A-x)
- the closest neighborhood (n-x-0)
- the token identifier (tid)

The participant can the compute the distance between the token identifier and the anchor d(A-x, tid). This distance can be used to request hosting neighborhood information from n-x-0. Every other information on the token can then be retrieved from token hosting neighborhood (THost).

THost carries a specific name for (1) a neighborhood (NHost) and for (2) a time window (TWHost). The different naming is introduced to distinguish these reserved tokens from other tokens of the Dial Different naming therefore does not change the logic of how tod etermine the neighborhood hosting a token.

# The Dial Economy
Due to it open and permissionless character, the Dial defines a value generation system to address spam and sustainability.

## Value Generation
Every single service performed by a Dial service provider (e.g. publisher) in the Dial is paid for by the requestor of that service. The price of some fundamental services (like the publication service) is set by the network. The price of other services is left to the discretion of the service provider. A __service intent request__ allows a requestor to collect prices and other execution conditions from different service providers.

## Spam Rsistance
Spam is the main thread to open and permissionless architectures. The Dial is built on top of a fundamental spam resistance system that makes sure the revenue generated from the publication of a single declaration is sufficient to cover present and future performance required to validate, maintain and retire that declaration. 

This is also a reason why each token carries an expiration date. After the expiration date, the token identifier is not known to the Dial and does not appear in the protocol.

In order to protect publishers (or service providers in general), the Dial requires each service request to be accompanied with a payment. Even the price inquiry service (a.k.a service intent request) is a payable service. Recall that the service intent request also returns a binding offer to the requesting party.

The price paid by a party to publish a declaration has a minimum cap, a file size factor, a validation effort factor and time to live factor. This price is generally substantial enough to have a significant impact on the wealth of the party generating spammy declarations.

These three factors (a) payment for intent request, (b) payment for publication and (c) the publisher registration constraint constitute together an effective spam resistance mechanism.

## Sustainability
Because of the built in expiration date for each token, the dial is designed to not keep bothersome histories. A Dial token is fogoten with the expiration of the token, if the token is not extended by the current controller. As stated above, each Dial token is covered with enougth reserves to finance the security of the token till expiration.

The Dial also does not have a treasury. Each token caries it's maintenance budget in the form of attached coins. This maintenance budget is consumed as the token is passed from one time window to another till the token is removed from the log at expiration.

# Monetary Policy
## Fundamental Principle
Each coin in the Dial originates from a combination between an external __Proof of Work__ and the __performace__ or a __canonical service__.

### External Proof of Work (PoW)
The external PoW is designed to enforce a relation between the value extracted from of a service consumed and the effort performed to legitimate the service request. The more balanced the relationship between the effort performed (input) and the value extracted (output), the lesser probable will a participant try to spam the system.

### Mining Coins out of PoW
The Dial allows a participant to perform some computation intensive work and use the resulting proof (PoW) to pay for the execution of a service. The service execution process transforms the provided PoW into a coin. This resulting coin is subsequently used in the Dial network as a mean of payment.

### Reducing Opportunistic Behavior
With respect the open and permissionless character of the Dial, coin production must be designed such as to have the total coin supply reflect the volume of activity performed in the Dial network. With this in mind, the Dial wants to prevent participant (1)  from performing work just with the purpose of increasing the coin supply, (2) from extracting additional value out of the coin production process (e.g. by producing work for services directed to service providers known in advance).

In order to prevent opportunistic behavior, the Dial limits PoW to coin convertion to services which by their nature do not allow participants to behave oppotunistic. Currently identified services are:
- The publication service.
- The coin bundling service.

## Publication Service Model
In order to have a declaration published, the submiting participant muss provide one payment for each publisher of both the THost and the NHost. I for example the THost has 11 publishers and the NHost has 11 publishers, the participant must provide 22 payment vouchers addressed to those publishers.

If we call __main token (resp. main declaration)__ the token being created or modified and __payment token (payment declaration)__ the token being used for payment, a publication operation will involve n + 1 tokens (1 main token and n payment tokens), where n is the number of publishers of THost + NHost, as we send a payment to each publisher of those two neighborhoods.

In order to rediem the payment, a publisher must fullfil all it's obligations and submit the coin/PoW with the proof of service performed for publication to the Dial.

### Publication Workflow
In order to publish a declaration,
- the requesting participant uses the token identifier to determines the neighborhood hosting the token (THost).
- the requesting participant uses the neighborhood identifier to deteremine the neighborhood hosting the THost (NHost)
- For each publisher of the THost, the publisher provides a payment token issued to the publisher. This payment token can be either a PoW or an existing coin. In both cases, the identifier of the payment token must be chosen such as to be hosted in the same THost as the main token.
- For each publisher of the NHost, the publisher provides a payment token issued to the publisher. This payment token can be either a PoW or an existing coin. In both cases, the identifier of the payment token must be chosen such as to be hosted in the same NHost as THost. 
- The controller of the underlying token submits the declaration to all publishers of the neighborhood for that token (THost) including the THost payment token.
- A THost publisher upon reception of a publication request,
  - proceeds with the formal validation of the contained declaration (mandatory information like ID), then
  - matches the declaration against the current state of the token (controller identifier),
  - proceeds with the verification of control rules (signature of the current controller), then
  - produces a verification certificate (VCert) and returns it to the requesting participant. 
- The controller upon receiving more than half of the responses (VCerts), submits the declaration for publication to all publishers hosting the token's neighborhood (NHost), including NHost payment tokens.
- An NHost publisher upon reception of the publication request,
  - verifies the legitimacy of all included VCerts including the majority rule,
  - enforces the verification of remaining publishers of the THost if missing,
  - produces a publication certificate (PCert) and returns it to the requesting participant.

The declaration is considered published when the controller (requesting participant) holds more than half of the PCerts.

### Publication of the Rediemed Coin
In order to rediem a coin earned publishing, each publisher must:
- transfer the VCert (resp. PCert) to all relevant publishers of the THost of the subsequent time window, within a minute after closing of the time window. The proof of transfer is a transfer certificate (TCert) produced by each publisher of the THost.
- bundle the TCerts (at least half +1) with the rediemed coin and submit them for publication to the coins relevant THost and NHost.
- The received VCerts are the proof of legitimacy of the coin and caan allow the publisher to spend the coin.

These coin based operaations do not require payment.

## Payment for Publication
There are two type of payments for the publication of a declaration sent to the Dial:
- The sending participant can attach coins to the declaration, in which case the publisher will rediem the coin attached to the publication request.
- The sending participant can attach proofs of work to that declaration, in which case each publisher will mine a new coin associated with a PoW attached to the publication request.

### Coin for Payment
Using a coin for the payment of a publication service is tricky in that, the coin has to carry an identifier hosted __in the same neigborhood__ as the main declaration's underlying token. This means the publisher produces two publications at the same time:
- the conditional publication advertizing the payment
- the publication certifying the main declaration

In order to pay with a coin,
- the requesting participant has to have a coin
- the coin has to carry an identifier that falls in the same neighborhood

### Proof of Work based Payment
In the case were the requesting participant does not have a matching coin, the requesting participanat can perform some work and use that __proof of work (PoW)__ to pay for the publication of the declaration.

The PoW performed for the payment of the publication has following properties:
- PoW must carry all details of the declaration to be published
- PoW must carry all details of the target neighborhood (timestamp)
- PoW must carry a conditional controller block with the public key of the addressed publisher
- PoW must provide an identifier hosted in the target neighborhood

The PoW document will be added a generated nonced to produce a hash that satisfies a defined difficulty (number of leading zeros).

The process of redieming the PoW attached to a publication request turns that PoW into a coin that can be spent by the publisher. The redemtion process is complete when publishers of the subsequent time window certify reception of the published record and coin are published in the subsequent time window.

## Bundling Coins (mon)
In matter of file size, a 50 mon has the same size like a 1 mon. Therefore transacting with a 50 single mon coins is 50 times more expenssive than transacting with a single 50 coin. As the publication of declaration files in the network are payable, it might be impractical to be using too many coins for large amount transactions. 

A bundeling declaration allows a participant to bundle many single coins into single bigger coin. E.g.: bundeling 50 single 1 mon into 1 single 50 mon. A bundeling declaration can therefore only be performed on coins falling in the same neighborhood. The identifier of the bundled coin must also be hosted in the same neighborhood.

# Network Services
One goal of the Dial is to achieve the broadest possible decentralization. This can only be achieved by keeping the Dial simple, such as to allow for common devices like mobile phones or IOT devices to play the publisher role and therefore participate to the Dial economy.

Dial network service providers deploy simple communication infrastructure components, that will allow network limited devices to act as first class citizen in the Dial network.

Dial network services are simple enougth to allow for consumer grade home based computers with static ip addresses to be deployed and operated as Dial network services. The operation of a Dial network component shall allow the owner to cover all incured costs. The service shall be simple enougth not to require special computer skills for the operation of network nodes.

## Relay Service
A relay service allows parties to exchange point to point messages with each other. Each message sent to a relay is accopanied with a payment token. The request for reading that message is also accompanied with a token.

If two different messages are sent to the same relay address, the second message overrides the first message.

A relay is open, permissionless and offers 3 methods:
- POST(url, data, exp, payment): allowing the caller to deposit a message for pickup with the relay.
- GET(url, payment): allowing the caller to collect a message
- DEL(url): allowing the removal of a message no longer needed.

The payment amount is dependent on the size of the message and expiration of the message. The Dial defines standard paacket sizes and prices for the relay service.

## Gateway Service
A gateway service allows a Dial participant to expose a permanent endpoint at which it can receive messages. Therefore, a single gateway address holds a queue of messages. The deposition and the collection of a messaage from a gateway endpoint is payable. A gatewaay support following operations:
- POST(url, data, exp, payment): allowing the caller to deposit a message for pickup to the gateway endpoint with the address url.
- GET(url, payment, PoP): allowing the caller to collect and delete the next message in the queue
The get request to a gateway address provides a proof of possession of the endpoint url.

## Broadcast Service
A broadcast service allows a Dial participant to expose a url where authenticated information can be pushed for the rest of network participants. A broadcast endpoint generally holds one file that is updated by the controller of that broadcast address. The deposition and the collection of a messaage from a broadcast endpoint is payable. A broadcast supports following operations:
- POST(url, data, pop, payment-1): allowing a participant to update the file held at the endpoint og a broadcast address.
- GET(url, payment-2): allowing the caller to collect the file
- DEL(url, pop): allowing the removal of a message no longer needed
The broadcast url contains public key hash. Posting or deleting the file at that url requires the proof of possession of the corresponding private key. Each file posted at that location is also signed with the corresponding private key


## Service Registration
Network service providers must register their services with the Dial by submitting corresponding performance declarations to the Dial. Following the same rationales as explained for publishers, a network service provider must register the performance declaration for __tw__ in __tw-2__. A performance declaration is binding. In the same logic of publishers, coin earned in a time window can only be rediemed in the subsequent time window, after presentation of the proof of performance.

# Performance Considerations
The Dial is designed to allow for efficient participation of memory and space limited devices.

## Space Constraints
The Dial is not designed to maintain archives. Neither the dial is designed to have a single participant maintain all information. Each participant of the (including publishers and other service providers) keep only the files the have an interest in keeping.

### Files Maintained by a Controller
A controller is a participant that controls a token. This means the participant holds the private key needed to initiate a change on the token.

All information needed to proove legitimate control of that token (PCerts) must be held by that controling participant.

The protocol held by publishers only contains the hash of the state of the token.

### Files Maintained by a Publishers of THost
The THost is the neighborhood hosting a token (in time window tw). At the begining of tw, publishers of the precendent time window (tw-1) redeems their due by transafering the last state of each token they hosted (in tw-1) to all publishers of the THost in tw. The transafer is aknowledged with a transfer certificate (TCert). The bundled list of TCerts of each token are used by the publisher of tw-1 to redeem the coin associated with hosting the token in tw.

The transfer of the state of a token is associated with part of the protocol (partial merkel tree) needed to validate the authenticity of that token state. 

### Files Maintained by a Publishers of NHost
The NHost is the neigborhood hosting the protocol of a THost. The NHost is responsible for:
- preparing the INP and NP at the end of the time window, aand transfering that NP to the TWHost of the time window.
- Transfering those protocols to publishers of the correponding neighborhood of the subsequent time window for documentation agains a TCert.
- Serving those protocols or partial version thereof against payment to requesting participants during tw.
- Using the TCerts in tw to redeem the work performed in tw-1.

### Files Maintained by Publishers of the TWHost
The TWHost is the neighborhood that:
- receptions NPs 
- use INP and NPs to produce ITWP and TWP at the end of the time window. 
- Transfers the ITWP and TWP to relevant neighborhood of subsequent for documentation against TCert.
- Use the TCerts in tw to redeem the work performed in tw-1.

### General on Space Constraints
As described above, no single node is required to hold the entire state of the Dial. The more token, are available in the Dial, the more coin are generated by publication activities, the more publishers will join the network, reducing the load to be carried by single publishers.

## Scalability
The Dial will scale with the number of tokens maintained by the network. The quantity of tokens maintained by the network will make economically interesting for publishers to join or leave the network.

The number of publishers release for the service of a time window is also dependent on the quantity of token avaailable for maintenance. The Dial will define a proportion between token and publisher that will help limit the number of publishers admitted to service a time window.

## Efficiency
The Dial is designed as an ideal nano payment infrastructure for web3 network services. The Dial is designed to allow for permissionless but verry efficient interaction among network actors.
- A network node maintaining a full dial log can validate payment locally and provide services to caller before forwarding payment token to the Dial.
- A more valuable service can require the caller to get the payment published before adding the payment token to the service call.

In both scenarios, the Dial allows for verry fast execution of annonymous and permissionless service operations.

# Security Considerations
## Annonymity
The Dial is designed to allow for 100% permissionles contribution. The only credential needed for the participation is the control over certain private keys. There is no need to keep an identity over the life time of a service life cycle (3 time windows.).
## Off Chain Capabilities
The Dial publication pattern allows for off chain transfer of token. A token might migrate toward many controllers before getting published to the Dial, as long as those transacting participant trust each oder for not double spending. The chain of signature will be sufficient for the dial, as long as the first signature in the chain is the one controling the last state of the token in the dial.

# Core Characteristics

## Instant Finality
Instant Finality is provided as the ENP defines a small enougth set of publishers (11 in THost and 11 in NHost) to take care of each token during the open time window. A participant being presented 6 PCerts can be assured that the state change of the token will be part of the time window protocol and therefore assume finality.

Double spending can only occur with the complicity of the majority of publishers in the THost and NHost, meaning about 6 + 6, 12 publishers. 

A single party must have enougth participants to achieve a situation where it controls the majority of publishers of a THost and NHost.

## Organic Scalability
Organic Scalability is provided as (1) the Dial is designed to allow each participant (e.g mobile phone) to perform the duty of a publisher, (2) growing number of end users leads to a growing number of publishers, (3) growing number of publishers leads to a growinng number of neighborhoods.

## Throughput
The Dial does not know the concept of a block size. The Diaal scales with the number of registered publishers. As there is a maximum number of token processable by a neighborhood, the Dial expect more publishers to join as the number of token maintained grows and some publishers to leave as the publication insentive drops due decreasing number of tokens.

## DETerministic Ordering of EXecution (DETOX)
DETOX is essential for the adoption of blockchain by other industries. As the Dial does nto have blocks, front running a declaraation will require the complicity of all publishers of THost.

## Spam Resistance
Spam Resistance is provided despite the open and permissionless character of the Dial. All service operation are payable. Payment ist performed either using existing acquired coins or proof of work done to generate aa coin. In both cases the price is set such aas to make it unatttractive for a participant to generate sapmy declarations.

## Constrained Tokens
The Dial provide the network with the possibility of constraining the exchange of some tokens. (1) the __authenticated withness protocol (AuthWith)__ requires the (new) controller of a token to provide an off chain proof of identification, while staying anonymous on chain, (2) __time lock contracts__ will delay the time to change control of the enclosing token, (3) __key locked contracts__ will allow the designated participant to control the enclosing token if it presents the proof of possession of a key, (4) combination thereof might also be applied to constrain token disposition.
