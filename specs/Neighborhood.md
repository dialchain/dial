# Ephemeral Neighborhood Protocol

# Excourse on the Dial Chain
The dial chain is a distributed log with the main purpose of turning each inserted __declaration__ into an __immutable assertion__. The dial chain can be seen as a log holding __state of tokens__. Tokens can be used to represent digital assets, people, organizations or even real estates, in short everything addressable.

A __time window__ is the lapse of time in which there is a deterministic partitioning of tokens and validators into __neighborhoods__. Partitioning is achieved by calculating the distance of each validator (resp. Token) to the __time window anchor__.

This __Ephemeral Neighborhood Protocol (ENP)__ secures the unpredictable but deterministic assocciation between validators and tokens in any given time window, hereby preventing validators from extracting additional value from their priviledged role of validator.

# Neighborhood
A neighborhood is a group of validators that are delegated the guardianship of a range of tokens in a given time window. Segmenting the network into neighborhods allows to (1) implement an efficient way to prevent double spend, (2) implement a natural scalability scheme for the dial network, (3) put no limit on the quantity of neighborhoods required for a time window, thus (4) keeping the validation time for each declaration constant, despite the unlimited block size of the network.

The distance function used to map validators and tokens to neighborhoods guarantees a fair spreading of both tokens and validators across the network. The use of an unpredictable anchor for the distance computation reduces the time span in which validators can take influence on the construction of neighborhoods. This prevent validators from extracting additional values out of the network (a.k.a. MEV).

The following picture illustrates the structure of a neighborhood.

![ENP](./img/enp.png?raw=true)

The dial network expect each participant to be able to compute neighborhoods associated with a time window.

## Member of a Neighborhoods
Members of a neighborhood are validators algorithmically assigned to that neighborhood. In order to qualify as validator in time window tw, a validator has to submit a performance declaration during time window tw-2. A performance declaration exposes a __Session Public Key__. This public key is used by the validator to produce assertions for all activities associated with this neighborhood. This same public key is also used as a __Protocol Address__ to reference the validation protocol produced by the validator at the closing of the time window. The validation procol can be saved on the __ipfs network__ under an __ipns address__ made out of the hash of this public key.

## Neighborhood Protocol
The neighborhood protocol is a file to be published by each member of the neighborhood as the act of closing the time window. When the member creates the neighborhood protocol, it stores it on the __ipfs network__ under the __Protocol Address__.

The neighborhood protocol is a sub-declaration of the member. For the protocol to be valid, The member must send the protocol declaration to the tw-1 neighborhood guarding the id of the member for publication. To prove validaty of the protocol, the member must update the protocol ipfs copy with the signature of each validator of tw-1. The __Member's Neighborhood Main Protocol__ must include references to folowing files, each file referenced by their content identifiers:

__Validator Registration Protocols__: this is the certified ordered list of all performance declarations sent to this neighborhood.

__Token State Protocol__: this is the certified ordered list of the last declarations of each modified token under the guardianship of this neighborhood during the given time window.

__Fraud Report__: this is a file containing the ordered list of submited declarations that where juged fraudulent by the validator.

## Neighborhood Hash
Finality is defined at a token level. Each token that appears in 6 of 11 protocols and does not appear in any fraud protoccol is considered valid. The hash of the ordered list of all valid tokens (token-id + file ccontent identifier) contitute the final __Neighborhood Hash__ of the neighborhood. This hash can be computed by any participant with access to all 11 neighborhood protocols. The hash is generally computed by data services and store for commercial redistribution.

## Time Window Hash
The time window hash is the sha256 hash of the ordered list of all neighborhood hashes. The time window hash of tw-2 is used a __anchor__ for time window __tw__.

## Eligible Validators for a Time Window
To compute neighborhood partitions for time window tw+2, a participant has to request all validator protoccols of time window tw. These protocols can be retrieved from the data services (ipfs network). Upon reception of those protocols, the participant can:
- calculate the hash of each nenighborhood,
- calculate the hash of time window tw-2 using neighborhood hashes,
- use the time window hash __hash_tw-2__ and the neigborhood validation registrations to compute the partitions of time window tw. 

## Administrative Tasks performed during tw-1

### Publishing the Neighborhood Protocol
The time window tw-2 is closed during tw-1. Closing operations are managed by validators of time window tw-2. Each validator of tw-2 publishes its neighborhood protocol by:
- sending it to all 11 validators of time window tw-1 for publication,
- aggregating publiccation signatures
- pushing the protocol enriched with tw-1 validator signatures to the ipfs network under the validator's __Protocol Address__.

### Validating Neigborhood Protocol Declarations
One of the main tasks of validators of tw-1 is the counter revalidation of neighborhood protocols sent for publication by a validator of tw-2. In general, each declaration (except protocol declaration) contained in the submited neighborhood protocol must be validated prior to counter signing the protocol. This might sound heavy at first sight, but task can be simplified if validator of tw-1 act as an observer durinng tw-2. As tw-1 validators know their neightborhood after closing of tw-2, they can register with relevant tw-2 and have each declaration sent to them instantly. An instant validation of those declarations will allow them to hint validators of tw-2 on fraudulent declarations ahead of the generation of the time winndow protocol. By the time they receive a neighborhood protocol from a validator of tw-2, they must have validated 99% of included decalrations.

## Minimum Number of Validators per Neighborhood
The minimum number of validators per neighborhood is currently set to 11. This means we will determine the number of neighborhoods existent in time window __tw__ by dividing the total number fo validators by 11. The last group will host the overflow, thus having more than 11 members. The following pseudocode displays the computation of the number of neighborhoods and the number of validators of the residual neighborhood.

```
let v be the number of validators registered for tw;
let n be the number of neighborhood for tw;

// The number of neigborhoods is the integer division by 11
n = t ~/ 11;
// The rest of the division is given to the last group
r = t % 11;
// Therefore, neighborhoods 1 .. n-1 have 11 members and neighborhood n  has 11 + t % 11 members.
```

# Unpredictable Distribution
The distribution of validators into neighborhoods must happen in a deterministic but unpredictable way, as having persistent neighborhoods will lead to validators extracting additional value out of the network (a.k.a MEV).

### Moving Anchors
The deterministic but unpredictable character is introduced by using the time window hash of __tw-2__ as an anchor in the computation of neighborhoods of tw. This is essential as participants can not change that constellation of participating validators for tw after the tw-2 is closed.

After closing tw-2, the distance computation will take the following form:
```dart
// For the distance computation, we use 
// point-1: The sha256 of the time window tw-2 (Anchor)
// point-2 The sha256 of point-1 (Anchor) and the sha256 of the id of the validator (Member)
final distance = euclideanDistance(Sha256Hash.of(__tw-2__), Sha256Hash.of(Sha256Hash.of(__tw-2__) + Sha256Hash.of(__member_id__)));
```

## Assignement of Validators to Neighborhoods
The assignement to neighborhoods is linear. We first put all elligible validators in a list ordered by their distance to the anchor. Then we cut by group of 11 validators per neighborhood, from the first to the last. The last entry contains the rest of the division by 11.

## Assignment of Declaration to Neighborhoods
The assignement of a declaration to a neighborhood follows the same pattern as the assigment of the validator to a neighborhood. The distance to the anchor is calculated using the following algorithm.

```dart
// point-1: The sha256 of the time window tw-2 (Anchor)
// point-2 The sha256 of point-1 (Anchor)  and the sha256 of the id of the declaration's id (Token)
final distance = euclideanDistance(Sha256Hash.of(__tw-2__), Sha256Hash.of(Sha256Hash.of(__tw-2__) + Sha256Hash.of(__delaration_id__)));
```
Once the distance is known, we assign the declaration to the neighborhood containing the distance. If for example we have the follwing distribution of neighborhoods:

```
neighborhood (0)[null, 487.3776769611017[, (1)[487.3776769611017, 558.3735308912843[, (2)[558.3735308912843, null[
```

A declaration with the distance to anchor of 505.3133209612843 will be assigned to neighborhood (1).
