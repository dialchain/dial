# DIAL White Paper
# Motivation
Web3 is struggling with finding the correct architecture. Fully mature and apparently decentratized applications appear to be giving way to censorship, because end user access to peer to peer networks are routed through API servers that are under the control of centralized organizations.

As we figure out that end user devices are not designed to be full citizen of peer to peer networks, API layers are establishing themselves as foundation for good user experience in Web3.

This paper describes a network that creates an economy for the deployment of scalable, open, permissionless and nano payment capable API networks. The latest will in turn open room for the deployment of trully decentralized and censorship resistant web3 applications.

# Abstract
The Dial __(Distributed Immutable Assertion Log)__ is a distributed log with the main purpose of turning each inserted __declaration__ into an __immutable assertion__. The Dial can be seen as a log holding state of __tokens__. Tokens can be used to represent anything addressable. A token is (1) created or modified by the token __controller__, (2) verified, certified and published by many __publishers__.

The Dial defines time slices called __time windows__. Each time window starts at the __UTC Hour__ and ends before the next __UTC Hour__. At the end of a time window, a __protocol__ is produced to make sure all participants share the same state of the Dial.

The Dial scales by __partitioning__ tokens and publishers into neighborhoods. The __Ephemeral Neighborhoods Protocol (ENP)__ secures a deterministic but unpredictable association between each token and a group of publishers (neighborhood) responsible for the verification and publication of changes on that token in the given time window.

The Dial has no authoritative identification mechanism. The Dial conditions permissionless participation with a __cummulative Proof of Work (cPoW)__. The __reputation__ of a participant is the aggregation of the PoW performed sofar by that participant. The reputation of a participant (sort of capital) exposes the participant to priviledges (e.g. eligibility to provide or consume some services). __Spam controll__ is provided by making sure verifiable misbehavior of a particpant leads to the lost of that participant's reputaion.

The Dial does not care about the __nature or the content of a token__. The main purpose of the Dial is to document the last authorization state of each token, such as to prevent illicite modification. Therefore, data found in Dial protocols are mainly identifiers, expiration dates, content and authorization hashes. In this same perspective, the Dial does not require a publisher to maintain a protocol history. 

The Dial does not require a publisher to __store  all protocols__. All data relevant to the Dial are partitioned among neighborhoods of the current time window. Whereby all publishers of a neighborhood hold the same data. After closing a time window, publishers of the closed time window transfer each protocol they controll or produce to relevant publishers in the new time window (as part of their coin redemtion process). This partitioning is possible because each protocol in the Dial is also considered a token and hence, has an identifier that can be used to determine the protocol's neighborhood.

The Dial does not require a publisher to __stay alive__ beyond the time commited to service a time window. After passing produced proocols to relevant publishers of the new time window, current publisher can go out of service. Violating promissed availability will nevertheless lead to a publisher losing it's reputation.

The Dial __monetary policy__ allows the mining of coins out of participant's PoWs and the reuse of those coins for the payment of goods and services among Dial participants.

The Dial __sustainability policy__ requires each token to be associated with a payment substential enougth to maintain the token toward it's expiration. The total value held by the Dial will be the motivating factor for publishers to join and service future time windows.

The following picture depicts the life cycle of a declaration, form the request for publication to the transfer of control to the subsequent time window. Dashed lines describe operations performed at the closing of a time window. Solid lines cover the process from the submission of a declaration to the reception of the publication certificate by the current controller.

![DIAL-WORKFLOW](./img/../specs/img/dial-workflow.png?raw=true&width=5)

Transfering control on a token occurs by the means of the current controller publishing a new declaration. In order to publish a declaration, (1) the current controller submits the declaration to one or more publishers of the token neighborhood (THost). (2) Addressed publishers verify the declaration and share the declaration with all other publishers of that neighborhood. (3) Each publisher of that neighborhood produces a verification certificat (VCert) and (4) sends the VCert to all publishers of the protocol neighborhood (NHost). (5) Upon receiving more than half of VCerts, each publisher of the protocol neighborhood creates a PCert and returns it to the submitting controller. The declaration is considered published when the submitting controller is in possession of more than half of PCerts.

# Key Entities

## Time Window - Declaration - Token
A time window identifier can be represented by a string starting with TW an the formated date time YYYYMMDDHH. The following picture displays 3 time windows in which the same token is modified using declarations. 

![DIAL](./img/../specs/img/dial-decl-token-tw.png?raw=true&width=5)

The first declaration (Declaration-0) creates the token. Subsequent declarations modify the token. Like displayed in TW2022031015, a token can be modified more than once in a single time window.

## Publisher
The entity responsible for the publication of a declaration into the Dial is called a __publisher__. Before insertion into the Dial, the publishers of the __neighborhood__ responsible for this token verify that the submited declaration is consistent with the state of the token as documented so far, and publishers of the neighborhood responsible for that neighborhood insert the declaration into the protocol of the first neighborhood.

In order to act as a publisher in the time window TW+1, a publisher must register for performance in time window TW.

## Neighborhood
In order to allow for parallel publications, Dial publishers are partitioned into ephemeral neighborhoods. The __Ephemeral Neighborhoods Protocol (ENP)__ secures a deterministic but unpredictable association between each token and a group of publishers (neighborhood) responsible for the verification and publication of changes on that token in a time window. A neighborhood exists only for the life time of a time window. The __layout__ of a time window is the ordered list of all neighborhoods of that time window, as presented in the following image (simplified to 2 dimensions for visualization).

![ENP](./img/../specs/img/dial-ENP2.png?raw=true&width=5)

### Distance Vector Mapping
As displayed in the picture above, both publishers and tokens are assigned to neighborhoods by computing their respective __distance__ to the time window __anchor__. The time window anchor is the merkel root of the intermediary protocol of the preceeding time window.

### Neighborhood hosting a Token (THost)
A token is said to be __hosted__ by a neigborhood if the ENP assigns that token to that neighborhood in the given time window. The neighborhood hosting a token is called __THost (for token host)__.

### Neighborhood hosting a Time Window(TWHost)
A time window itself is considered a token with the reserved identifier TWYYYYMMDDHH. The distance between the hash of this identifier and the anchor alows to locate the neighborhood responsible for that time window. This neigborhood is called the __TWHost (time window host)__ and is responsible for the publication of information on that time window e.g list of registered publishers, the time window protocol.

### Neighborhood hosting a Neigborhood (NHost)
Each neighborhood is also a token with the reserved unique identifier NYYYYMMDDHH-I where YYYYMMDDHH is the timestamp of the hosting time window, and I ist the position of the neighborhood relative to the time window anchor.

The distance between the hash of this identifier and the anchor can alow us to locate the neighborhood responsible for hosting that neighborhood. This neigborhood is called the __NHost (neighborhood host)__ and is responsible for aggregation of the work done by publishers of a neighborhood and the publication of the neighborhood's protocol.

## Certificates
Certificates are proofs. They are not directly stored in the Dial, but can be part of the hash documenting the authorization state of a token.

### Verification Certificate (VCert)
A __verification certificate (VCert)__ is produced by each publisher of the THost as a proof that the submitted declaration is consistent witth the state of the token as documented sofar.

### Publication Certificate (PCert)
A ___publication certificate (PCert)__ is a proof that the referenced token state is present in the Dial. A declaration is considered published when a controller can present __(k/2)+1 PCerts__, where k is the number of publishers of the given time window.

### Sharing Certificates (SCert)
All publishers of a neighborhood are required to share each produced certificate (VCert, PCert) with each other not later than in the __minute__ following the production of those certificates. This is essential as the earliest knowledge of each certificate will reduce the certification of conflicting declarations and help reduce noice and spam in the network.

In order to enforce sharing of produced certificates, redemtion of coin associated with work done can only happen, if publisher present __Sharing Certificates (SCerts)__. These are recceipts produced by other publishers after recception of certificates produced by their neighborhood peers.

## Protocols
A protocol is a merkel tree holding the state of some entities. The Dial knows neighborhood protocols and time window protocols.

### Incremental Computation of Merkel Roots
We can allow for incremental computation of a merkel roots if design the ordering criteria to apend new leaf nodes at the end of the list of leaf nodes. All protocols in the Dial are designed such as to allow for the incremental  computation of merkel roots and therefore reduce the time needed to secure the state of the Dial between time windows.

### Neighborhood Protocol (NP)
The NP is the merkel tree of the last state of all tokens hosted by the target neighborhood. The neighborhood protocol is produced by publishers of the NHost.

In order to allow for incremental computation of the neighborhood protocols, leaf nodes are ordered by (1) the timestamp ot the token first publication and (2) the lexicographical order of the token identifier. This way, new token are appended at the end of the list and do not trigger a rebalance of the protocol tree.

### Intermediary Neighborhood Protocol (INP)
The INP is computed during the 57th minute of the time window and contains (1) the state of all unchanged tokens and (2) the state of all changed tokens from the first to the 56th minute. The INP must be sent to the TWHost before the end of the 57th minute.

Publishers of time window TW+1 must register for performancce in TW, before the ITWH is computed. This list of publishers of TW+1 is available to a neigborhood of TWHost at the time it computed the ITWH. Together with the INP, the list of all publishers registered for performance with the target neighborhood is also transfered to the TWHost.

### Time Window Protocol (TWP)
The TWP is the merkel tree of all neighborhood protocols hosted by the time window. 

As the list of neigborhoods of a time window is knwon in advance, as well as their order, the merkel root of the TWP can be upgraded evertime a publication certificate upgrades the NP.

### Intermediary Time Window Protocol (ITWP)
The ITWP is computed in the 58th minute of the time window and distributed in the 59th minute of the time window. It is used to determine the intermediatry time window hash __(ITWH)__, which is the merkel root of the ITWP.

The ITWH is available from the 59th minute of the current time window and is used as the anchor of the subsequent time window.

After the ITWH of TW if computed, publishers of TWHost can pull the list of publishers of TW+1 and use it to compute the layout of TW+1.

### Final Neighborhood Protocol (NP)
The final neighborhood protocol is computed in the first minute of the subsequent time window by publishers of NHost. The change date is the last second of the old time window. NP are sent to the old TWHost for documentation, as the change is hapening in the old time window.

### Final Time Window Protocol (TWP)
The final time window protocol is computed in the third minute of the subsequent time window by the TWHost (of the old time window) and documented as such.

This TWP is then marked with the timestamp of the first second of the new time window and sent to the relevant THost of the new time window  for documentation (The same way any token get published).

The folowing picture illustrate both the neigghborhood and the time window protocols.

![Protocols](./img/../specs/img/dial-protocols.png?raw=true&width=5)

### Transfer and Location of Protocols
Protocols are held by publishers which produce and pass them to relevant publishers of the subsequent time window.

Each time window protocol produced in TW is transfered by each publisher of the NHost of TW to the corresponding publisher of the NHost of TW+1 as part of the opening protocol of TW+1. The identifier of the neighborhood in TW is used to compute the new neighborhood in TW+1.

Each publisher of the NHost receiving a NNP of TWmust verify the protocol, sign it and submit if the corresponding publishers of the TWHost in TW+1 as part of the opening protocol.

TWHost of the old time window protocol received the protocol over two different channels: (1) from the TWHost of the old time window and (2) from the publishers of NHost of old neighborhood inn the new time window. This allow them to make sure the protocol is sufficiently consistent for the Dial moving forward.

Holding a protocol is also an economic activity, as publishers are paid to release those protocols.

As protocols have identifiers and are therefore tokens, it is always easy to compute the address of the neighborhood hosting a protocol.
- NPs are existent:
  - as closing protocol in their neighbohood of origin
  - as openning protocol in the subsequent neigborhood
- TWP are available:
  - as closing protocol in their neighbohood of origin
  - as openning protocol in the subsequent neigborhood

Therefore, the most actual protocols are always available either in the current time window (in form of oppening protocols), or in the former time windows in form of closing protocols.

### Authorization State of a Token
Event though protocols are used to secure the state of tokens, contenta and authorization state of a token is held by the token controller. Only the hashes of content and authorization state of the token is used in the computation of protocols.

In the proccess oof submiting a declaration to modify a token, the token controller must provide an authorization state, whose hash matches the one included in the current protocol.

In order to validate the sate of a token at the end of a given time window, two partial merkel trees (PMT) are required:
- The PMT of the neighborhood protocol hosting the token in the given time window
- The PMT of the protocol of the given time window.

This two doccuments might be in the possession of different publishers. Because each of these documents is a token, the doccument identifier and the anchor of the current time window can be used to compute the neighborhood where to retrieve the documents.

# The Dial Economy
Due to it open and permissionless character, the Dial defines a value generation system to address spam and sustainability.

## Value Generation
Every single service performed by a Dial service provider (e.g. publisher) in the Dial is paid for by the requestor of that service. The price of some fundamental services (like the publication service) is set by the network. The price of other services is left to the discretion of the service provider. A __service intent request__ allows a requestor to collect prices and other execution conditions from different service providers.

## Spam Rsistance
Spam is the main thread to open and permissionless architectures. The Dial is built on top of a fundamental spam resistance system that makes sure the revenue generated from the publication of a single token is sufficient to cover present and future performance required to validate, maintain and retire that token. 

This is also a reason why each token carries an expiration date. After the expiration date, the token identifier is not known to the Dial and does not appear in the protocol.

In order to protect publishers (or service providers in general), the Dial requires each service request to be accompanied with a payment. Even the price inquiry service (a.k.a service intent request) is a payable service. Recall that the service intent request also returns a binding offer to the requesting party.

The price paid by a party to publish a declaration has a minimum cap, a file size factor, a validation effort factor and time to live factor. This price is generally substantial enough to have a significant impact on the wealth of the party generating spammy declarations.

These three factors (a) payment for intent request, (b) payment for publication and (c) the publisher registration constraint constitute together an effective spam resistance mechanism.

## Sustainability
Because of the built in expiration date for each token, the dial is designed to not keep bothersome histories. A Dial token is fogoten with the expiration of the token, if the token is not extended by the current controller. As stated above, each Dial token is covered with enougth reserves to finance the security of the token till expiration.

The Dial also does not have a treasury. Each token caries it's maintenance budget in the form of attached coins. This maintenance budget is consumed as the token is passed from one time window to another till the token is removed from the log at expiration.

# Monetary Policy
## Fundamental Principle
Each coin in the Dial originates from a combination between an external __Proof of Work__ and the __performance__ of a __canonical service__.

### External Proof of Work (PoW)
The external PoW is designed to enforce a relation between the value extracted from of a service consumed and the effort performed to legitimate the service request. The more balanced the relationship between the effort performed (input) and the value extracted (output), the lesser probable will a participant try to spam the system.

### Mining Coins out of PoW
The Dial allows a participant to perform some computation intensive work and use the resulting proof (PoW) to pay for the execution of a service. The service execution process transforms the provided PoW into a coin. This resulting coin is subsequently used in the Dial network as a mean of payment.

### Reducing Opportunistic Behavior
With respect the open and permissionless character of the Dial, coin production must be designed such as to have the total coin supply reflect the volume of activity performed in the Dial network. With this in mind, the Dial wants to prevent participant (1)  from performing work just with the purpose of increasing the coin supply, (2) from extracting additional value out of the coin production process (e.g. by producing work for service requests directed to service providers known in advance).

In order to prevent opportunistic behavior, the Dial limits the conversion of PoW to coin to services which by their nature do not allow participants to behave oppotunistic. Currently identified services are:
- The publication service.
- The coin bundling service.
