# Token
A token is the unit of existence in the dial network. There is nothing else in the dial network but tokens.

## Token Properties

### Controller Identifier
The controller of a token is the party authorized to modify the token. It is the address referencing a public key that can be used to verify the next modification on this token.

### Token Identifier
The identifier of a token is the hash of the public key generated for the purpose of identifying this token. The underlying keypair is used to legitimate the token declaration (proof) at creation.

### Expiration
Each token has an expiration date. The expiration date of a token can be extended by the mean of the current controller submiting a change declaration of the token. The expiration date of a token is essential, as the network has to keep the history of the protocols for the purpose of validating changes on unexpired token.s The longer the expiration time of he token, the more expesive is the validation of he token, as the network will have to keep all protokols affecting this token, till the token expires.

## Token Declaration
In order to create or modify a token, we use a declaration. The declaration identifier is always the token identifier.

### Json Representation
Note that (1) we will use Json to describe the structure of document in prose, (2) We will use [CBOR](https://datatracker.ietf.org/doc/html/rfc8152) as the underlying serialization format, (3) we will use [multicodec](https://github.com/multiformats/multicodec) to prefix all binary representations of keys, hashes and content identifiers.
```json
{
    "type": "Declaration",
    "declaration": [
        {
            "type": "Participant",
            "id": "unnique PublicKeyHash-MultiCodec",
            "controller": "another PublicKeyHash-MultiCodec",
            "exp": "time-utc-sec"
        }
    ],
    "proof": ["proof produced with private of id"]
}
```

## Proof of Possession

The declaration identifier is allways a public key. The producer of a declaration must prove possession of the corresponding private key. This is done by adding a proof block to the declaration. The following document displays the proof associated with a new declaration.
```json
{
    "type": "Declaration",
    "declaration": [
        {
            "type": "Participant",
            "id": "zEruWfhngbEc16jmpZBHSk4Tx872CHDWXeNsDJfL8yHo6",
            "exp": "2021-06-24T21:36:03Z",
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
Proof of possession is essential, as we give the responsibility of publishing the initial document to the creator of the document.

## Token Controll

### Token Validation
A declaration associated with a token can be validated by any entity in possession of the relevant recent partial history of the network. Validation is simple enougth to allow each participant of the network to validate a declaration in milliseconds. Nevertheless, a valide token is far from being sufficient for a transaction as the controller of the token can issue two conflicting declarations at the same time.

### Publishing a Declaration
Publishing a declaration in the network allows the prevetion of the issuance of conflicting declarations on the same token.

When a participant sends a declaration to a publisher for insersion into the network log, the publisher returns a proof block to the participant. It is the responsibility of the participant to store and advertize the issued proof as certificate of ccontroll of the underlying token. 

Publisher aare only required to hold the declaration of a very limited aamount of time. The time needed to pass over publication responsibilities to other validators.

A declaration with two publication certificated, looks like.

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
The dial network does not require publishers to archive document they certify. The network assumes each controller of a token has an economic interest in keeping the last active version of the token declaration and the justifying publication.

The sole information to be maintained by publishers for the purpose of performing their duties are neighborhood protocols.

A controller willing to exercise controll on a token must provide the last declaration tranfering control to that participant.
