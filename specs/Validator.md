# Validator
A validator is a form of organization supported in the DialChain.

An organization is a participant that relies on the vote of its members (participants) for the production of declarations. Therefore, an organization assert with votes. 

The following json document displays the example of a simple declaration of organization (that can be used by a validator).
```json
{
    "type": "Declaration",
    "declaration": [
        {
            "type": "Organization",
            "id": "zGCPM1TZZdBTdH1LUrP1u38Y3L89wVj94Y8iBXCLEeMqZ",
            "created": "2021-06-24T21:36:03.422792Z",
            "controller": [
                "zGCPM1TZZdBTdH1LUrP1u38Y3L89wVj94Y8iBXCLEeMqZ"
            ],
            "account": [
                {
                    "network": "org.bitcoin.production",
                    "address": "3BvzcwdXihvGa6GAbV9RDSCTX6fXrNnorX",
                    "control": {
                        "quorum": 2,
                        "verificationMethod": [
                            "z4DiXDE9t44qkq6uGmrhwWZHsTFofqmaKvuTWq687UawA#2021-06-24T21:36:02.970369Z#key-1",
                            "zEruWfhngbEc16jmpZBHSk4Tx872CHDWXeNsDJfL8yHo6#2021-06-24T21:36:03.409110Z#key-1",
                            "zAo7AYWYkFH2cPfmfq4LEzwGk7UTJYePDbqGozztnK8Kt#2021-06-24T21:36:03.415619Z#key-1"
                        ]
                    }
                }
            ],
            "verificationMethod": [
                {
                    "type": "Ed25519VerificationKey2021",
                    "id": "zGCPM1TZZdBTdH1LUrP1u38Y3L89wVj94Y8iBXCLEeMqZ#2021-06-24T21:36:03.422792Z#key-0",
                    "publicKeyMultibase": "zGCPM1TZZdBTdH1LUrP1u38Y3L89wVj94Y8iBXCLEeMqZ"
                }
            ],
            "assertionMethod": [
                {
                    "type": "Vote",
                    "id": "zGCPM1TZZdBTdH1LUrP1u38Y3L89wVj94Y8iBXCLEeMqZ#2021-06-24T21:36:03.422792Z#am-0",
                    "quorum": 2,
                    "member": [
                        {
                            "id": "z4DiXDE9t44qkq6uGmrhwWZHsTFofqmaKvuTWq687UawA",
                            "shares": 1
                        },
                        {
                            "id": "zEruWfhngbEc16jmpZBHSk4Tx872CHDWXeNsDJfL8yHo6",
                            "shares": 1
                        },
                        {
                            "id": "zAo7AYWYkFH2cPfmfq4LEzwGk7UTJYePDbqGozztnK8Kt",
                            "shares": 1
                        }
                    ]
                }
            ],
            "service": [
                {
                    "type": "PublisherService",
                    "id": "zGCPM1TZZdBTdH1LUrP1u38Y3L89wVj94Y8iBXCLEeMqZ#2021-06-24T21:36:03.422792Z#PublisherService-0",
                    "serviceEndpoint": "https://node0.first-dial-validator.io/publisher",
                    "assertionMethod": "zGCPM1TZZdBTdH1LUrP1u38Y3L89wVj94Y8iBXCLEeMqZ#2021-06-24T21:36:03.422792Z#am-0"
                },
                {
                    "type": "PublisherService",
                    "id": "zGCPM1TZZdBTdH1LUrP1u38Y3L89wVj94Y8iBXCLEeMqZ#2021-06-24T21:36:03.422792Z#PublisherService-1",
                    "serviceEndpoint": "https://node1.first-dial-validator.io/publisher",
                    "assertionMethod": "zGCPM1TZZdBTdH1LUrP1u38Y3L89wVj94Y8iBXCLEeMqZ#2021-06-24T21:36:03.422792Z#am-0"
                },
                {
                    "type": "PublisherService",
                    "id": "zGCPM1TZZdBTdH1LUrP1u38Y3L89wVj94Y8iBXCLEeMqZ#2021-06-24T21:36:03.422792Z#PublisherService-2",
                    "serviceEndpoint": "https://node2.first-dial-validator.io/publisher",
                    "assertionMethod": "zGCPM1TZZdBTdH1LUrP1u38Y3L89wVj94Y8iBXCLEeMqZ#2021-06-24T21:36:03.422792Z#am-0"
                },
                {
                    "type": "LookupService",
                    "id": "zGCPM1TZZdBTdH1LUrP1u38Y3L89wVj94Y8iBXCLEeMqZ#2021-06-24T21:36:03.422792Z#LookupService-0",
                    "serviceEndpoint": "https://open.first-dial-validator.io/lookup",
                    "assertionMethod": "zGCPM1TZZdBTdH1LUrP1u38Y3L89wVj94Y8iBXCLEeMqZ#2021-06-24T21:36:03.422792Z#am-0"
                }
            ]
        }
    ],
    "proof": [
        {
            "issuer": "zGCPM1TZZdBTdH1LUrP1u38Y3L89wVj94Y8iBXCLEeMqZ",
            "created": "2021-06-24T21:36:03.422792Z",
            "proofPurpose": "PoP",
            "type": "JcsBase64Ed25519Signature2021",
            "verificationMethod": "zGCPM1TZZdBTdH1LUrP1u38Y3L89wVj94Y8iBXCLEeMqZ#2021-06-24T21:36:03.422792Z#key-0",
            "signatureValue": "SjYlTPmG-Q6l9qJDnfGwC8U4CnOoTFbQq2EEdWHodhSYG8qBWN86U5IhsmY1HdhhckeGQAZVKU63lQZTXqeiCg",
            "nonce": "e3aa1fe3-f617-49f0-ac0d-1336d879e1c9"
        },
        {
            "issuer": "z4DiXDE9t44qkq6uGmrhwWZHsTFofqmaKvuTWq687UawA",
            "created": "2021-06-24T21:36:03.442490Z",
            "type": "JcsBase64Ed25519Signature2021",
            "assertionMethod": [
                "zGCPM1TZZdBTdH1LUrP1u38Y3L89wVj94Y8iBXCLEeMqZ#2021-06-24T21:36:03.422792Z#am-0",
                "z4DiXDE9t44qkq6uGmrhwWZHsTFofqmaKvuTWq687UawA#2021-06-24T21:36:02.970369Z#am-0"
            ],
            "verificationMethod": "z4DiXDE9t44qkq6uGmrhwWZHsTFofqmaKvuTWq687UawA#2021-06-24T21:36:02.970369Z#key-0",
            "signatureValue": "hZVWWKDwFlYurt-yCMWUTuBDXWRvi6uRxMz0DFBjqwM8b9UblyZBJWBSeUza9KmlV6hF-1IUOmfvoeJmt2Y8Cg",
            "nonce": "4125fd41-c134-4b6a-998f-c420a46a2532"
        },
        {
            "issuer": "zEruWfhngbEc16jmpZBHSk4Tx872CHDWXeNsDJfL8yHo6",
            "created": "2021-06-24T21:36:03.450192Z",
            "type": "JcsBase64Ed25519Signature2021",
            "assertionMethod": [
                "zGCPM1TZZdBTdH1LUrP1u38Y3L89wVj94Y8iBXCLEeMqZ#2021-06-24T21:36:03.422792Z#am-0",
                "zEruWfhngbEc16jmpZBHSk4Tx872CHDWXeNsDJfL8yHo6#2021-06-24T21:36:03.409110Z#am-0"
            ],
            "verificationMethod": "zEruWfhngbEc16jmpZBHSk4Tx872CHDWXeNsDJfL8yHo6#2021-06-24T21:36:03.409110Z#key-0",
            "signatureValue": "mMSs_oHUIJZiS-Vv955DtcfNqGGhu5jtEqEitxJTnw9XARlpix10McS5Wvex-pJkKpkfCX2LfLqvARuMq5noDQ",
            "nonce": "e0998cc1-e1cf-4e17-97a5-3502756441dc"
        },
        {
            "issuer": "zAo7AYWYkFH2cPfmfq4LEzwGk7UTJYePDbqGozztnK8Kt",
            "created": "2021-06-24T21:36:03.453456Z",
            "type": "JcsBase64Ed25519Signature2021",
            "assertionMethod": [
                "zGCPM1TZZdBTdH1LUrP1u38Y3L89wVj94Y8iBXCLEeMqZ#2021-06-24T21:36:03.422792Z#am-0",
                "zAo7AYWYkFH2cPfmfq4LEzwGk7UTJYePDbqGozztnK8Kt#2021-06-24T21:36:03.415619Z#am-0"
            ],
            "verificationMethod": "zAo7AYWYkFH2cPfmfq4LEzwGk7UTJYePDbqGozztnK8Kt#2021-06-24T21:36:03.415619Z#key-0",
            "signatureValue": "-dQGZDW5rPUMyGFO7WO8BHd-PfP7wZ8_lPpnLcvl1bS8GJ24BD0cbT7P7y5ZnRT23P3JTwdKpLeg75FiVWRwDA",
            "nonce": "f5ce1bea-d1e9-45de-bb10-4a79d850f3c2"
        }
    ]
}
```
## Content Identifier
The cid of this organization declaration file is
```json
"B7NCdnaDQvwipw4YLV58MHb1yCkW6rTamgwCXwVNHtqijxRroN6wDa86LG1myQCthekWsf3sNLJrU1M4YNa61hQXdYBz"
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