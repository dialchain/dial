# Reputation
The __reputation__ is a value earned the by a participant of the dial network for being active an behaving honest. 

The Dial publication process consist in :
- (1) verifying the proof of execution (PoE) of the controller script attached to the token,
- (2) inserting the token into the Dial log and maintaining the state of the token in the log throughout the expiration of the token.

The payment provided by the submitting participant is used to cover both activities. A well defined amount of the payment is used to cover the cost of verifying the PoE of the controller script of the token. The rest of the payment is added to the work of the token and used to maintain the token in the Dial toward it's expiration.

Every unit of work cosumed by the Dial network can be added to the reputation of the controlling participant. A cummulating operation occurs everytime aa modification operation is submitted with an accompanying reputation token.

## Usage of a Reputation
### Identifier and Neighborhood
A reputation is a token with a random identifier. Like the proof of work aand any other form of payment, the reputation caan only be used in the host neighborhood. This means in order to leverage aa reputation, the controlling participant must attach the reputation to aa modification request that faalls in the same neighborhood.

### Controller Property
Like any other token, a reputation has a controller property that documents the script guarding that reputation. This makes a reputation tradeable like any other token.

### Aggregation
Like coins, reputations can be aggregated. This means two reputations of each _1000 wu_, that both fall in the same neighborhood caan be bundeld in a declaration to produce a reputation of _2000 wu_. Agggregationn can only take place among reputations falling in the same neighborhood.

### Reputation Credit
As the Dial maintains a token without the intervention of the controller, every work unit spent to move the token from a time window to the next one is accumulated into the _rep_ field of the token and caan be awarded to the controller with the next modificaation operation, if the controller provided aa reputation token.

### Flow Controll
A reputation object can not be leveraged more than twice in a single time window. Nevertheless, it can be used a accumulator in that time window as many times as possible.


## Privileges of the Reputation
### Less work for new Declarations (Reputtaationn Ratio)
If the Dial sets the reputation ratio for a proof of work to be 1 per 10,000, a participant will be able to leverage a reputation of _10,000 wu_  to represent a PoW of _1 wu_ in a time window.

For a sound monrtary policy
- From time window 0 to TW 999, the Dial will set reputation ratio to 1 per 1,000
- From TW 1000 to TW 9999, the Dial will set reputation ratio to 1 per 10,000
- From TW 10,000, the Dial will set a reputaation ration of 1 per 100,000

### Perfoming Services in the Network
In order for the Dial to function aas designed, some Dial services need to provide a certain degree of reliability:
- A commited publisher must be available from th 56th minute of the preccedent time window to the 4th minute of the subsequennt time window. This aavailaability in essential for the receptioning of token going into the custudy of the publisher in the target time window and for the transfer of token to publishers of the subsequent time window.
- A commited relay service must be available for the time frame of commitment, as participant rely on that availability to perform peer to peer messaaging operations.

As the failure to perform commited services will penalize the network, Dial service providers are required to guaranty their commitment with an amount of work unit held into a reputation object. A verifiable violation of the provider commitment will lead to the lost of deposited reputation. Recall that a reputation deposited for the security of a commitment can not be traded or leveraged during the commitment period (Sort of bound capital).

TODO: define the reputation amount needed for each service type (relay, publishing)

# Reputation as Warant for Honest Behavior
A reputation can also be used as warant for honest behavior. For exaample for reason of speed or annonymity, some transaction can be performed offchain and submitted in a batch to the Dial. For counterparty services performed reputaations can be used to secure promisse of payment. The failure of payment might then lead to couterparty loosing deposited reputations.