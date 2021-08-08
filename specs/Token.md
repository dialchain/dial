# Token
A token is the unit of existance in the dial network. Each token has an identifier. This identifier is unique in the dial network. The identifier of a token is allways a public key. In a json representation, the identifier is displayed encoded in a [multibase](https://github.com/multiformats/multibase) format.

## Declaration
In order to create or modify a token, we use a declaration. The declaration id is allways the token id.
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
To verify the uniquness of a token, we use the sha256 bynary representation of the public key.

## Sub-Declaration
Some tokens have a hierarchical structure. A Participant can have a validator function. For that purpose the participant must register a performance declaration for each time window of action. A performance declaration itself is a proper declaration, derived from the declaration of a participant.

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
The first part of the identifier refers to the public key multibase of the enclosing participant. The second part of the id is the multibase representation of the public key of this performance declaration.

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

## IPNS Address
Each declaration produced in the dial network can be advertized by the producer of the token in ipfs network. The __ipns address__ of the token is the sha256 of the public key bytes, as specified by [ipns](https://docs.ipfs.io/concepts/ipns/#example-ipns-setup-with-cli). 

Publishing declarations and sub-declarations associated with a token is only meaningfull for well defined use cases.

A sub-declaration is published under the public key of the sub-declaration. This is the second multibase string in the id of the sub-declaration.

## Validating a Declaration
Declarations and sub-declarations related to a token are always validated in the neighborhood associated with the token identifier. The token identifier is always the first multibase string in the id field of the declaration (resp. subdeclaration).

## Publishing a Declaration IPFS
When a participant send a declaration to a validator for publication, the validator returns a proof block to the participant. It is the responsibility of the participant to add that proof block to the declaration file and publish the declaration to the ipfs network.

## Archivinng Proofs
Each validator producing a proof also has the responsibility of archiving that proof. For the purpose of archiving the proof, the validator can rely on the data services operated in the dial network. Data services will archive these proofs an return them to participants against payment.

A proof has the following structure

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

The file with multiple proof entries is the aggregated publication produced by the participant upon reception of the proof sent by each validators. Each validator proof looks identical, but only with one proof entry. Thar archiving of the document and the validator proof is in the responsibility of validator. The publication of the aggregated publication to the ipfs network can only be done by the controling participant, as this is done under the public key identifying the token.

Data services also have the intelligence to aggregate proofs provided to them for storage.