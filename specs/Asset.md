# Asset
An asset is a sort of token used to represent value. The value can be the mapping of an external asset or the representation of a native asset like the dial coin.

Despite entity token types, the creator of an asset is not allways the enti

In order to prevent misuse of identifiers, the dial network (1) requires identifier of a token to be a public key, (2) requires a new declaration to prove possession of the corresponding private key. This way, reusing a token identifier will require control on the corresponding private key.

In a json representation, the identifier is displayed encoded in a [multibase](https://github.com/multiformats/multibase) format.

## Declaration
In order to create or modify a token, we use a declaration. The declaration identifier is always the token identifier.

### Json Representation
```json
{
    "type": "Declaration",
    "declaration": [
        {
            "type": "Participant",
            "id": "zEruWfhngbEc16jmpZBHSk4Tx872CHDWXeNsDJfL8yHo6",
        }
    ]
}
```
### Binary Representation
All operations operating on a token use the sha256 of the tokens public key bytes.

## Sub-Declaration
Some tokens have a hierarchical structure. A Participant can have a validator function. For that purpose the participant must register a performance declaration for each time window of action. A performance declaration itself is a sub-declaration, derived from the declaration of a participant.

The following json displays the header part of a performance declaration.
```json
{
    "declaration": [
        {
            "type": "Perfomance",
            "id": "zEruWfhngbEc16jmpZBHSk4Tx872CHDWXeNsDJfL8yHo6#z6uYZbi4aubwxGkZ2wEXpvfp1XVN5cQ2FDGmowGyMJDXY",
            "controller": [
                "zEruWfhngbEc16jmpZBHSk4Tx872CHDWXeNsDJfL8yHo6"
            ]
        }
    ]
}
```
The first part of the identifier refers to the public key multibase of the enclosing participant. The second part of the id is the multibase representation of the public key of this performance declaration. The controller of a performance declaration is allways the enclosing participant.

## Proof of Possession
The declaration identifier is allways a public key. The producer of a declaration must prove possession of the corresponding private key. This is done by adding a proof block to the declaration. The following document displays the proof associated with a new declaration.
```json
{
    "type": "Declaration",
    "declaration": [
        {
            "type": "Participant",
            "id": "zEruWfhngbEc16jmpZBHSk4Tx872CHDWXeNsDJfL8yHo6",
            "created": "2021-06-24T21:36:03.409110Z",
            "controller": [
                "zEruWfhngbEc16jmpZBHSk4Tx872CHDWXeNsDJfL8yHo6"
            ],
            "rest...": "ignored for display ..."
        }
    ],
    "proof": [
        {
            "issuer": "zEruWfhngbEc16jmpZBHSk4Tx872CHDWXeNsDJfL8yHo6",
            "created": "2021-06-24T21:36:03.409110Z",
            "proofPurpose": "PoP",
            "type": "JcsBase64Ed25519Signature2021",
            "verificationMethod": "zEruWfhngbEc16jmpZBHSk4Tx872CHDWXeNsDJfL8yHo6#2021-06-24T21:36:03.409110Z#key-0",
            "signatureValue": "NJlKbI7fqMzkm_PWpfd4jCPdVghxaH3gYw3tH22Ht29xen6DW0anTpsb_1Cw0lid37aEiDdte1SCbvc6BQsYAg",
            "nonce": "43102c83-c20f-4e38-bfe0-b805bf54c6e2"
        }
    ]
}
```
Proof of possession is essential, as we give the responsibility of publishing this document in the __ipfs network__ to the creator of the document.

## Publishing a Declarationn to IPFS using the IPNS Address
Each declaration produced in the dial network can be advertized by the producer of the Declaration in the ipfs network. (1) the producing participant starts by storing the document in the ipfs network under the __content identifier (cid)__ of the declarationn file. (2) the cid is then used to create a publication file looking like:
```json
{
    "type": "Publication",
    "cid": [
        "B7NCdnaDQvwipw4YLV58MHb1yCkW6rTamgwCXwVNHtqijxRroN6wDa86LG1myQCthekWsf3sNLJrU1M4YNa61hQXdYBz"
    ]
}
```
(3) This second file is published on ipns under the __ipns address__ of the declaration, that is the sha256 of the public key bytes representing the id of the token, as specified by [ipns](https://docs.ipfs.io/concepts/ipns/#example-ipns-setup-with-cli). 

Publishing declarations and sub-declarations associated with a token is only meaningfull for well defined use cases. A sub-declaration is published under the public key of the sub-declaration. This is the second multibase string in the id of the sub-declaration.

The publication document as presented above is called a __non certified document__.

### Validating a Declaration
Declarations and sub-declarations related to a token are always validated in the neighborhood associated with the token identifier. The token identifier is always the first multibase string in the id field of the declaration (resp. subdeclaration).

### Publishing a Declaration IPFS
When a participant send a declaration to a validator for publication, the validator returns a proof block to the participant. It is the responsibility of the participant to add that proof block to the publication file and update the publication file in the ipfs network.

The creating participant has a legitimate innterest of updating this file, as the order transacting party will have to verify the file before trusting the transaction.

After two validation responses, the ipns referenced file will look like:

```json
{
    "type": "Publication",
    "cid": [
        "B7NCdnaDQvwipw4YLV58MHb1yCkW6rTamgwCXwVNHtqijxRroN6wDa86LG1myQCthekWsf3sNLJrU1M4YNa61hQXdYBz"
    ],
    "proof": [
        {
            "issuer": "zEruWfhngbEc16jmpZBHSk4Tx872CHDWXeNsDJfL8yHo6",
            "created": "2021-06-24T21:36:03.457066Z",
            "type": "JcsBase64Ed25519Signature2021",
            "assertionMethod": [
                "zGCPM1TZZdBTdH1LUrP1u38Y3L89wVj94Y8iBXCLEeMqZ#2021-06-24T21:36:03.422792Z#am-0",
                "zEruWfhngbEc16jmpZBHSk4Tx872CHDWXeNsDJfL8yHo6#2021-06-24T21:36:03.409110Z#am-0"
            ],
            "verificationMethod": "zEruWfhngbEc16jmpZBHSk4Tx872CHDWXeNsDJfL8yHo6#2021-06-24T21:36:03.409110Z#key-0",
            "signatureValue": "nU81rjImBqm4sAilkHJbqWDZO8Hm0P_JviHQemr7jvhmSEcU6oOZTQN_WkZzmNhwXuIpP7Y0pO5Yo5vLio_sCg",
            "nonce": "33019ed2-99a9-4feb-984b-adfcaf0b2b39"
        },
        {
            "issuer": "zAo7AYWYkFH2cPfmfq4LEzwGk7UTJYePDbqGozztnK8Kt",
            "created": "2021-06-24T21:36:03.457066Z",
            "type": "JcsBase64Ed25519Signature2021",
            "assertionMethod": [
                "zGCPM1TZZdBTdH1LUrP1u38Y3L89wVj94Y8iBXCLEeMqZ#2021-06-24T21:36:03.422792Z#am-0",
                "zAo7AYWYkFH2cPfmfq4LEzwGk7UTJYePDbqGozztnK8Kt#2021-06-24T21:36:03.415619Z#am-0"
            ],
            "verificationMethod": "zAo7AYWYkFH2cPfmfq4LEzwGk7UTJYePDbqGozztnK8Kt#2021-06-24T21:36:03.415619Z#key-0",
            "signatureValue": "USD8oFoBTtIo4Js1EPGe7OohjE1FFJU0QMFR4MiBdvNxWBd7RNlK8qWIEKFoYTw86u8RfQXf-VaBzCMXtNOfDw",
            "nonce": "41179231-bf1f-4399-827f-50b9ebaa61bf"
        }
    ]
}
```

## No Archivinng of Proofs
The dial network does not require validators to archive document they certify. The network assumes each controller of a token has an economic interest in keeping the last active version of the token declaration and the justifying publication.

The sole information to be maintained by validators for the purpose of performing their duties are neighborhood protocols.

A controller willing do dispose a token must provide the last version of the declaration and corresponsing publicationn proof to each validator of the target neighborhood.
