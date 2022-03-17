# Ephemeral Neighborhood Protocol

## Excourse on the Dial Chain
ENP secures a deterministic association between each token (existing or new) and a group of publishers responsible for that token during the given time window. The deterministic association of tokens to neighborhoods is essential for the serialization of movement of tokens acros time windows and to prevent conflicting state of tokens.

## Neighborhood
A neighborhood is a group of validators that are delegated the guardianship of a range of tokens in a given time window. Segmenting the network into neighborhods allows to (1) implement an efficient way to prevent double spend, (2) implement a natural scalability scheme for the dial network, (3) put no limit on the quantity of neighborhoods required for a time window, thus (4) keeping the validation time for each declaration constant, despite the unlimited number of token that caan be managed at once.

The distance function used to map publishers and tokens to neighborhoods guarantees a fair spreading of both tokens and validators across the network. The use of an unpredictable anchor for the distance computation reduces the time span in which validators can take influence on the construction of neighborhoods. This prevent validators from extracting additional values out of the network (a.k.a. MEV).

The following picture illustrates the structure of a neighborhood.

![ENP](./img/dial-ENP2.png?raw=true)

The dial network expect each participant to be able to compute neighborhoods associated with a time window, given the list of publishers and the anchor.

## Publisher
Publishers are entities responsible for the security of the network. A publisher can join and leave the Dial at will. The commitment to participate in the publication process of a time window is nevertheless binding. A publisher must explicitly announce it's intention to participate for time window __tw__ with a performance declaration he publishes in time window __tw-1__, but before the computation of the intermediary neighborhood protocols of tw-1.

The __neighborhood__ building process is a simple, but deterministic algorithm that can be performed by any device.

## Session Public Key
The performance declaration submited by a participant to service a time window, exposes a __Session Public Key__. This public key is used by the participant to produce assertions for all activities associated with this time window.

## Neighborhood Protocol
The NP is the merkel tree of the last state of all tokens hosted by the referenced neighborhood. The neighborhood protocol is produced by publishers of the neighborhood hosting neighborhood (NHost).


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