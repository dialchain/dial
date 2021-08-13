# Controller
The [controller](./Controller.md) of a declaration is the entity authorized to change the declaration. it is the holder of the declaration. A controller can be a simple verification method, a participant or an organization identifier.

The concept of a controller if fundamental to the dial chain, as it is used to implement all type of __transfer of control__ in the dial network. e.g. In order for a participant (payer) to make a payment to another participant (payee) in the dial chain, the payer must transfer controll of a set of dial coins to the payee.

## Representation
Following entry display the example of a controller entry.
```json
{ 
    "type" : "Controller-type",
    "id" : "controller-id",
    "origin":"source-ipns-address",
    "address":"target-ipns-address"
}
```
### type
This is the type of the ccontroller entry. This can be a simple verification method, a particcipant identifier, or even a constrained controll entry. The type determines the nature of other fields required by the controller block.

### id
The identifier of the controller. It is generally a multibase representation of a public key, even when it references a participant.

### origin
This is the public key used to compute the ipns address of the former controller. Precedent certification of the transfer of conntrol can be found here. We also call if __certificate of origin__.

### address
This is the public key used to compute the ipns address of this controller. In the case of annonymous coins, this will match the id property of the controller. Maintaining origin and address references allow to trace the control path of a token.

## Transfer of Control
In the dial network, we can call the participant giving up control the __trnasferer__ and entity receiving control the __transferee__. In generall, the transferee has an interest in proving finality of the transfer. As these proofs will be needed to exercise any type of control on the token. As the validators are not required to archive proof, this shall be done by each controlling participant with the self interest of retrieving when needed.

A typical transfer occurs in following steps: (1) the transferer submits a transfer declaration to eligible validators. This transfer declaration accompanied by certificate of origine of the current control (latest publication changing the controller of the token). (2) each validator uses neighborhood protocols to legitimate the presented control relationship. (3) each validator certifies the transfer and returns the new proof to the transferer. (4) tranferer submit declaration and proofs to the transferee. (5) transferee publishes the proof in the ipns network under the new controller address.

Note that the dial network does not require the transferer to submit the transfer declation to validator. Nor does the dial network requires the transferee to be the one publishinng those files to the ipfs network. The transmission of a declaration of validator can be done by the transferee, a mixin service or any other type os pearticipant in the network. What matters is that the proof will have to be accessible to the new controller at the moment he want to exercise controll on the token.

The __address__ of the controller block is the public key used to advertize the publication justifying this control relationship. Wether this address is controlled by the source (old controller) of the target (new controller) of the transfer of control, or wether the address is controll by an archiving service in the network is left to the decision of the participants.

## Constrained Tokens
The controller block of a __Constrained Tokens__ provide the network with the possibility of constraining the exchange of that token. (1) the authenticated witness protocol requires the (new) controller of a token to provide an offchain proof of identification, while staying anonymous onchain, (2) time lock contracts will delay the time to change control of the enclosing token, (3) hash locked contracts will allow the designated participant to control the enclosing token if it presents the seed of the given hash, (4) combination thereof might also be applied to constrain token disposition.

### AuthWit

### Time Locked Contract

### Hash Locked Contract

### HTLC (Hash Time Locked Contract)