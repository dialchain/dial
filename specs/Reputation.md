# Reputation
The dial network has no authoritative identification mechanism. It conditions permissionless participation through __Proof of Work (PoW)__. The PoW is initially designed to keep noices (spams) out of the network.

The __reputation__ is a value earned the by a participant of the dial network for being active an behaving honest. As the dial network is open and permissionless, there is no authoritative identification required to enlist a participant. Using our __Time Degrading Proof of Work Protocol__, the network can automatically attach a value to the reputation of a participant. The reputation of a participant allows the participant to generate more value performing less work, thus turning the reputation into a non tradeable capital bound to the identity of that participant.

In order to __regulate monney emmission__, (1) he dial network limits the quantity of the proof of work to be performed by a single participant within a given amount of time (time window), (2) the dial network only accounts the proof of work effectively put into circulation by that participant to date (by the mean of paying for network security services), (3) The proof of work is always set higher for the creation of a new token, than for the modification of an existing token, so participant won't generate token identifiers based on the known target neighborhood, so they can direct revenue to known validators.

# Mining a Coin
There is two way of paying for a declaration sent to the network for validation. (1) either the sending participant attaches coins to the declaration, or it attaches a proof of work to that declaration.

In the first case, the validator will rediem the coinn attached to the declaration. In the second case, the validator will mine a new coin associated with the PoW attached to the declaration. For performance reason, there is no need to check for participant limit at the validation time, as any limit violation will ruin the reputation of the participant at the closing of the time window.

## Preventing Delegation of PoW
In order to prevent an illicite PoW market, the PoW system is designed such as to force the participant to sign the nonced input of the PoW-Hash. This process will make it more expensive for a participant to delegate millions of hash operations to a network computer as network operations will endup being more expensive than the local hash computation.

## Guarantee of Actuallity
Actuallity of the proof of work is essential to make sure reputaion is really built onn continuous usage of network services. Proof of actuality of the work done is provided by having the participant include the hash of the last known time window (tw-2) into the input string to be signed.

# Time Degradation of the Proof of Work
In order to turn the work done sofar into a reputation, the network allows a participant to use the work done sofar (accumulated reputation capital) as leverage to generate new tokens with less work. In order to generate a certificate of work done, a participant can send a subdeclaration to the network summarizing the work done sofar into a single PoW Certificate. That proof can be used in future operations to reduce the PoW to be performed on a new declaration.

## Less work for new Declarations
A PoW certificate expresses the work done in number of time windows. As the proof of work required for a single declaration is also expressed in number of Time Windows, the reputation expressed on the PoW certificate can be used to multiply the PoW generated for a single declaration.

If for example (1) a time window is one hour, (2) the PoW required to submit a declaration is 6 minutes, the participannt will have to perform 6 minute of work for the submission of a declaration. In case the participant presents 1000 time windows the participant can save a minute of work.


## Perfoming Services in the Network
In order for a participant to offer service in the network (validator, relay, ...) and thus earn money, the participant has to proove ownership of a certain reputation.

# Losing Reputation
The reputation of a participant is lost, as soon as the network can proove the participant's dishonest behavior. A dishonest behavior is given when a participant intentionaly submits conflicting declarations to the network (e.g when the participant double spend a coin). Every signed decalration is assumed an intended act of the participant, as the participant bears the responsibility of protecting it's private key.
