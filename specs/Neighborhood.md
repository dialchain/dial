# Ephemeral Neighborhood Protocol

# Excourse on DialChain
The DialChain is a distributed log with the main purpose of turning each inserted __declaration__ into an __immutable assertion__. The DialChain can be seen as a log holding __state of tokens__. Tokens can be used to represent a digital coin, a person, an organization or even a physical building, in short everything addressable and therefore non fungible.

A __time window__ is the laps of time in which all validators agree on the __state__ of every single __token__ maintained by the DialChain. Therefore when a time window is closed, we assume every token has a cosistent state across the network (all participants). To guaranty all participants see the same state, a time window closes with a __Twindow Hash__. This is the merkel tree of all declarations published during the target time window. A twindow is therefore known as aggreed upon when __51%__ of eligible validator publish that hash in the subsequent time window.

For the moment, the length of a time window is set to one __Earth Hour__. This means a declaration published to the DialChain might need up to 2 hours to achieve finality. In order to provide for more instant finality, the DialChain's __Ephemeral Neighborhood Protocol (ENP)__ secures a deterministic association between each token and a group of validators (neighborhood) responsible for that token in a given time window. The ENP makes sur:
- Eligible validators are assigned neigborhoods prior to the start of the time window.
- Each declaration submitet for publication is also assigned to a single neighborhood during that time window.

We assume all validator in a neighborhood will have the same state of assigned token, and achieve the same result for the validation of each declaration. If the neighborhood cannot achieve a __51%__ agreement over the state of a token, the next closest neighborhood is invited to co-validate that token. The process is repeated till a 51% consensus is achieved throughout the network for any given token.

# Neighborhood
A neighborhood is a group of validators that are toghether responsible for the validation of a group of tokens in a given time window. The intention of segmenting the network into neighborhod is:
- Provide for an efficient way to prevent double spend.
- Provide for a natural scalability of the network. As the quantity of neighborhoods is not limited. The distance function used to map validator and token to neighborhoods guaranties a fair spreading of both token and validators across the network.
- Provide a way of preventing MEV by making the association of token to neighborhoods unpredictable.

The following picture illustrate the structure of a the ephemeral neighborhood protocol.
![ENP](./img/enp.png?raw=true)

## Eligible Validators for a Time Window
The list of validators eligible to validate declarations in time window __tw__ is known in advance during time window __tw-1__, as each validator of __tw__ must publish its performance declaration during __tw-2__.

## Closing Time Window TW-2
The time window tw-2 is closed during tw-1. It is closed in some cordinated operation between the validators of tw-2. After the sha256 of __tw-2__ is computed and published by more than 51% of the validators of tw-2, each network participant can consider the time window tw-2 closed.

Upon receiving notification for the closing of tw-2, validators of tw can start preparinng the work by:
- retrievinng the list of all validators registered for tw
- constructing the neighborhoods for tw
- retrieving and caching state of tokens associated with that relevant neighborhood.
- monitorinng changes on those declarations during time window tw-1

## Retrivinng the Validator List for TW
After tw-2 is closed during tw-1, analyzing the chain files will 
- provide the list of all validators registered for tw (during tw-2).
- provide the sha256 of the time winndow tw-2 known as hash256_tw_m2

## Minimum Number of Validators per Neighborhood
The minimum number of validators per neighborhood is currently set to 11. This means we will determine the number of groups existent in time window __tw__ by dividing the total number fo validators by 11. The last group will host the overflow, thus having more than 11 members. The following pseudocode displays the computation of the number of validators per neighborhood.

```
let v be the number of validators registered for tw;
let n be the number of neighborhood for tw;

// The number of neigborhoods is the integer division by 11
n = t ~/ 11;
// The rest of the division is given to the last group
r = t % 11;
// Therefore, neighborhoods 1 .. n-1 have 11 members and neighborhood n  has 11 + t % 11 members.
```

## Ephemeral Distribution
The distribution of validators into neighborhood must happen in a deterministic but unpredictable way, as having persistent group will lead to validator extracting value out of the network (a.k.a MEV).

### Unpredictability (Moving Anchors)
The deterministic but unpredictable character is introduced by usinng the sha256 of tw-2 as an anchor in the computation. This is essential as participants can not change that constellation of participating validators for tw after the tw-2 is closed.

After closing tw-2, the distance computation will take the following form:
```dart
// For the distance computation, we use 
// point-1: The sha256 of the time window tw-2 (Anchor)
// point-2 The sha256 of point-1 (Anchor) and the sha256 of the id of the validator (Member)
final distance = euclideanDistance(Sha256Hash.of(__tw-2__), Sha256Hash.of(Sha256Hash.of(__tw-2__) + Sha256Hash.of(__member_id__)));
```

## Assignement of Validators to Neighborhoods
The assignement to neighborhoods is linear. We first put all elligible validators in a list ordered by their distance to the anchor. Then the cut by group of 11 validators per neighborhood, from the first to the last. The last entry contains the rest of the division by 11.

## Assignment of Declaration to Neighborhoods
The assignement of a declaration to a neighborhood follows the same pattern as the assigment of the validator to a neighborhood. The distance to the anchor is calculated using the following algorithm.
```dart
// point-1: The sha256 of the time window tw-2 (Anchor)
// point-2 The sha256 of point-1 (Anchor)  and the sha256 of the id of the declaration's id (Token)
final distance = euclideanDistance(Sha256Hash.of(__tw-2__), Sha256Hash.of(Sha256Hash.of(__tw-2__) + Sha256Hash.of(__delaration_id__)));
```
Once the distance is known, we assign the declarationn to the neighborhood containing the distance. If for example we have the follwing distribution of neighborhoods:
```
neighborhood (0)[null, 487.3776769611017[, (1)[487.3776769611017, 558.3735308912843[, (2)[558.3735308912843, null[
```
A declaration with the distance to anchor of 505.3133209612843 will be assigned to neighborhood (1).

# Preparing Performance for TW
In the Dial network, preparingn for performance includes following steps:
- Announce performance declaration see [Performance Declaration](./Performance.md) in tw-2
- Monitor tw-1 to be notified on completion of tw-2.
- If necessary, compute your neighborhood for tw-2
- Collect and cache Token assigned to your neighborhood for tw
- Wait for tw and start lsitening to service requests.