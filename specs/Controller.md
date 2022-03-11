# Controller
The controller of a declaration is the entity authorized to change the declaration. It is represented by the public key referenced by the controller entry of tthe decclaration.

The concept of a controller if fundamental to the dial chain, as it is used to implement all type of __transfer of control__ in the dial network. e.g. In order for a participant (payer) to make a payment to another participant (payee) in the dial chain, the payer must transfer controll of a set of dial coins to the payee.

## Representation
The controller entry is the hash of a public key. It is represented inn multihash format.
```json
{
    "type": "Declaration",
    "declaration": [
        {
            "type": "Asset",
            "id": "unnique PublicKeyHash-MultiCodec",
            "controller": "another PublicKeyHash-MultiCodec",
            "exp": "time-utc-sec",
            "class": "dial",
            "value": "10"
        }
    ]
}
```

## Transfer of Control
In the dial network, we can call the participant giving up control the __transferer__ and the entity receiving control the __transferee__. In generall, the transferee has an interest in proving finality to the transfer. As these proofs will be needed to exercise any type of control on the received token. As the validators are not required to archive proof, this shall be done by each controlling participant with the self interest of retrieving when needed.

A typical transfer occurs in following steps: 

- The transfer declaration (accompanied by the latest proof of controll of the token) is submited to relevant validators of the current time window. Submission can occcur either (1) through the transferee or (2) through the transferer.
  - In the first case the transferer submits a transfer declaration the transferee. The transferee prevalidates if he can exercise controll on the new declaration (if he is in possession of the private key). If this is the case, the transferee forwards the declaration to eligible validators. 
  - In the second case, the transferer start by sending the declaration to validators and then forward the validated declaration to the transferee (Including all validator signatures).
- In both cases, each validator retrieves neighborhood protocols (or partial merkel tree) of the preccedent time window and use it to legitimate the presented control relationship. Each validator certifies the transfer and returns the new proof to the submeeting participant. 
- Submiting participant forward newest declaration to the other participant.

Note that the dial network does not require the transferer to submit the transfer declation to validator. Nor does the dial network requires the transferee to do so. The transmission of a declaration to a validator can be done by any party, a mixin service or any other type os pearticipant in the network. What matters is that the proof will have to be accessible to the new controller at the moment he want to exercise controll on the token.

## Verifying Authenticity of a Declaration
The authenticity of a declaration can be verified by any holder, by accessing the partical merkel tree of the host neighborhood for the precedent time window, in the case of a closed time window, or by just verifying the signature of relevant participants in the current time window, assuming that the publication is going to be part of the closing merkel tree.

## Constrained Tokens
The controller block of a __Constrained Tokens__ provide the network with the possibility of constraining the exchange of that token. (1) the authenticated witness protocol requires the (new) controller of a token to provide an offchain proof of identification, while staying anonymous onchain, (2) time lock contracts will delay the time to change control of the enclosing token, (3) hash locked contracts will allow the designated participant to control the enclosing token if it presents the seed of the given hash, (4) combination thereof might also be applied to constrained token disposition.

### AuthWit

### Time Locked Contract

### Hash Locked Contract

### HTLC (Hash Time Locked Contract)