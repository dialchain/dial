# Validator
An organization is a participant that relies on the vote of its members (participants) for the production of declarations. Therefore, an organization assert with votes. 
The following json document displays the example of a simple declaration of organization (that can be used by a validator).
```json
{
    "declaration": [
        {
            "type": "Organization",
            "id": "z6Sdi3MYqAr1d3UvSKUAqyrZcy4u676rRnqUg7kitioAe",
            "created": "2021-07-24T03:25:47.000Z",
            "controller": [
                "z6Sdi3MYqAr1d3UvSKUAqyrZcy4u676rRnqUg7kitioAe"
            ],
            "account": [
                {
                    "network": "org.bitcoin.production",
                    "address": "bc1qmmcjrsewshtcltf3967hrt5z84ewe8hkpg5hlxukurj2nfzrkf8s8d8adh",
                    "control": {
                        "quorum": 2,
                        "verificationMethod": [
                            "zHyijTZH7kHWPZKbgPcKfuQBYJLAXRtWQWyjMgAxnzaVH#2021-07-24T03:25:47.000Z#key-Secp256k1-1",
                            "z8kd8g7fLQvnPzikZXgdjGe3vHDzzuV3izEq4kshuEPnq#2021-07-24T03:25:47.000Z#key-Secp256k1-1",
                            "zHpMz1GAQt4HS89Ss8BZSSzwtPqL7PT1CLov6ScDHTYpD#2021-07-24T03:25:47.000Z#key-Secp256k1-1"
                        ]
                    }
                }
            ],
            "verificationMethod": [
                {
                    "type": "Ed25519VerificationKey2021",
                    "id": "z6Sdi3MYqAr1d3UvSKUAqyrZcy4u676rRnqUg7kitioAe#2021-07-24T03:25:47.000Z#key-Ed25519-0",
                    "publicKeyMultibase": "z6Sdi3MYqAr1d3UvSKUAqyrZcy4u676rRnqUg7kitioAe"
                }
            ],
            "assertionMethod": [
                {
                    "type": "Vote",
                    "id": "z6Sdi3MYqAr1d3UvSKUAqyrZcy4u676rRnqUg7kitioAe#2021-07-24T03:25:47.000Z#am-0",
                    "quorum": 2,
                    "member": [
                        {
                            "id": "zHyijTZH7kHWPZKbgPcKfuQBYJLAXRtWQWyjMgAxnzaVH",
                            "shares": 1
                        },
                        {
                            "id": "z8kd8g7fLQvnPzikZXgdjGe3vHDzzuV3izEq4kshuEPnq",
                            "shares": 1
                        },
                        {
                            "id": "zHpMz1GAQt4HS89Ss8BZSSzwtPqL7PT1CLov6ScDHTYpD",
                            "shares": 1
                        }
                    ]
                }
            ]
        }
    ],
    "type": "Declaration",
    "proof": [
        {
            "issuer": "z6Sdi3MYqAr1d3UvSKUAqyrZcy4u676rRnqUg7kitioAe",
            "created": "2021-07-24T03:25:47.000Z",
            "proofPurpose": "PoP",
            "type": "JcsBase64Ed25519Signature2021",
            "verificationMethod": "z6Sdi3MYqAr1d3UvSKUAqyrZcy4u676rRnqUg7kitioAe#2021-07-24T03:25:47.000Z#key-Ed25519-0",
            "signatureValue": "cHNbILr92sRmGc3TYstseO0ohx8qlPgSkhtX20w1xV-OXYT3pkQnE9-IcB3wfJo7bBh4pzPn9ejgT1QdPNwfCg",
            "nonce": "3253edc8-7568-4ac3-90b1-75c431a01b4e"
        },
        {
            "issuer": "zHyijTZH7kHWPZKbgPcKfuQBYJLAXRtWQWyjMgAxnzaVH",
            "created": "2021-07-24T03:25:47.000Z",
            "proofPurpose": "PoP",
            "type": "JcsBase64Ed25519Signature2021",
            "assertionMethod": [
                "z6Sdi3MYqAr1d3UvSKUAqyrZcy4u676rRnqUg7kitioAe#2021-07-24T03:25:47.000Z#am-0",
                "zHyijTZH7kHWPZKbgPcKfuQBYJLAXRtWQWyjMgAxnzaVH#2021-07-24T03:25:47.000Z#am--0"
            ],
            "verificationMethod": "zHyijTZH7kHWPZKbgPcKfuQBYJLAXRtWQWyjMgAxnzaVH#2021-07-24T03:25:47.000Z#key-Ed25519-0",
            "signatureValue": "w_R_JuFQH9WZGBjjhPB-S_brLxWXW49bqJc6l84W86AvH_1_5XVrQEiXOQ1oaln9vpQ9u9W-3LieHHWg7fBXAA",
            "nonce": "1113ed7e-26b7-435f-87f4-abc0a8203c2e"
        },
        {
            "issuer": "z8kd8g7fLQvnPzikZXgdjGe3vHDzzuV3izEq4kshuEPnq",
            "created": "2021-07-24T03:25:47.000Z",
            "proofPurpose": "PoP",
            "type": "JcsBase64Ed25519Signature2021",
            "assertionMethod": [
                "z6Sdi3MYqAr1d3UvSKUAqyrZcy4u676rRnqUg7kitioAe#2021-07-24T03:25:47.000Z#am-0",
                "z8kd8g7fLQvnPzikZXgdjGe3vHDzzuV3izEq4kshuEPnq#2021-07-24T03:25:47.000Z#am--0"
            ],
            "verificationMethod": "z8kd8g7fLQvnPzikZXgdjGe3vHDzzuV3izEq4kshuEPnq#2021-07-24T03:25:47.000Z#key-Ed25519-0",
            "signatureValue": "8yXT17vgicfbJKnkshvSv4GWkXggMI0qBeHuBUQn08VhPYp8X9ZgpA8s-L9D7ZYoSkb0we5U9UZHhpE4cXSsDA",
            "nonce": "16e71d6b-a5b3-43ec-988b-221e286b4997"
        },
        {
            "issuer": "zHpMz1GAQt4HS89Ss8BZSSzwtPqL7PT1CLov6ScDHTYpD",
            "created": "2021-07-24T03:25:47.000Z",
            "proofPurpose": "PoP",
            "type": "JcsBase64Ed25519Signature2021",
            "assertionMethod": [
                "z6Sdi3MYqAr1d3UvSKUAqyrZcy4u676rRnqUg7kitioAe#2021-07-24T03:25:47.000Z#am-0",
                "zHpMz1GAQt4HS89Ss8BZSSzwtPqL7PT1CLov6ScDHTYpD#2021-07-24T03:25:47.000Z#am--0"
            ],
            "verificationMethod": "zHpMz1GAQt4HS89Ss8BZSSzwtPqL7PT1CLov6ScDHTYpD#2021-07-24T03:25:47.000Z#key-Ed25519-0",
            "signatureValue": "Yr7C-AqlARZmNDykh7HuXtw_u2uTYatxoKY9JK0bEUQ04mrUhK3ZWq-JWuQswz4SsUlAeGqeJtuAfL5jqrPsBQ",
            "nonce": "cd6b3133-d589-4a55-9131-a690bcec85d4"
        }
    ]
}
```
## Content Identifier
The cid of this organization declaration file is
```json
...
```
## General Items
The structure of this document is very similar to the one defined in [Participant](./Participant.md). Therefore similar elements will not be explained here.

## [declaration][i][type]
The type of this declaration. In this case "Organization"

## [declaration][i][id]
The unique identifier of this declaration. If this is an organization declaration, [id] will be the unique identifier of the organization. This shall be unique as the DialChain does not allow for duplicate declarations. A new declaratation with the same [id] is considered a modification of the existing declaration. 

The id is always a public key in base58. The producer of this declaration must include the corresponding verification method in the declaration file and a proof (signature) with the purpose "PoP", proving access to the corresponding private key.

The key used produce the id of this declaration shall not be the one used by a member for proper assertions.

### Validation Rule DIAL00100
Each declaration has a unique identifier. The submission of a new declaration carrying this same [id] is understood  by the network as a modification request. Validator will make sure modificator proves control of the document as defined by the controller block of the latest version of this declaration.

If the producer of a declaration file can not prove possession of the corresponding private key, the declaration will be deemed invalide.

The key used for an organization identifier shall not be the same as a key used by a member. The corresponding private key can be destroyed after the production of the PoP proof as, further modification of the declaration will be controlled by the assertionMethod block.

## [declaration][i][account][address]
Despite the case of the single participant, this organization bitcoin address is a multisig acount, that requires 2  of 3 signatures to spend.

## [declaration][i][account][control]
References the verification methods to be used by members to spend from this account. Corresponding members public keys are located in the declaration files that can be found derefencing the verification method ids.

## [declaration][i][type]
This is a reference to the data structure used in the assertionMethod subelement. In this case a Vote.

## [declaration][i][assertionMethod][id]
This is the identifiier of this assertion method. A declaration can contain many assertion methods.

## [declaration][i][assertionMethod][member]
Member entries reference other participants (simple or organization) that can vote to the extend of shares they hold.

## [declaration][i][assertionMethod][member][shares]
States the number of shares assigned to this member.

### Validation Rule DIAL00101
Shares value must be a natural number higher than zero.

## [declaration][i][assertionMethod][quorum]
The quorum defines the number of shares needed for a valid assertion.

### Validation Rule DIAL00102
The quorum must be a natural number higher zero and less or equals the total of shares listed in the member subelement.

## [declaration][i][service]
A service record describes a service provided by an organization. In the case above, the validator exposes three PublisherServices and one LookupService.

## [proof]
As the example above displays, the declaration of an organization must provide: 
- a valid assertion of the identifier. 
- a valid assertion of each member.