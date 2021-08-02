# Performance
Performance is the act of providing a service in the Dial network. Well known services are:
- Relay Service provided by __Router Nodes__
- Gateway Service provided by __Gateway Nodes__
- Data Service provided by __Data Nodes__
- Publishing Service provided by __Validator Node__

As we can notice in the naming, only Relay and Gateway services require permanent presence in the network. Those need static ip addresses so they can be permanently reachable by other network participants.

Both data and validator nodes can rely on the the service of a Gateway Nodes to provide for reachability.

Because of the permissionless nature of the DialChain, it is difficult to tell when a service provider join or leaves the network. Therefore, the Dial protocol requires service providers to pre-announce readyness for performance. We call this announcement a __Performance Declaration__. Performannce declarations are binding. E.g. in order for a service provider to perform in time window __tw__, it needs to publish its readyness in time window __tw-2__. This concept is essential for the stability of the network, as a participant consuming a service must rely on providers being available.

The following file shows the structure of a performance declaration:

```json
{
    "declaration": [
        {
            "type": "Perfomance",
            "id": "z597FwdoYuc71oKc1wvR13o8D7Sdx4u6W3sySp1pVTRXU",
            "created": "2021-07-24T03:09:26.000Z",
            "controller": [
                "z597FwdoYuc71oKc1wvR13o8D7Sdx4u6W3sySp1pVTRXU"
            ],
            "account": [
                {
                    "network": "org.bitcoin.production",
                    "address": "bc1qt64l9pxn373vv7j774p5lmsh3qwed46alcx32f",
                    "control": {
                        "quorum": 1,
                        "verificationMethod": [
                            "z597FwdoYuc71oKc1wvR13o8D7Sdx4u6W3sySp1pVTRXU#2021-07-24T03:09:26.000Z#key-Secp256k1-1"
                        ]
                    }
                }
            ],
            "verificationMethod": [
                {
                    "type": "Ed25519VerificationKey2021",
                    "id": "z597FwdoYuc71oKc1wvR13o8D7Sdx4u6W3sySp1pVTRXU#2021-07-24T03:09:26.000Z#key-Ed25519-0",
                    "publicKeyMultibase": "z6uYZbi4aubwxGkZ2wEXpvfp1XVN5cQ2FDGmowGyMJDXY"
                },
                {
                    "type": "Secp2561k1VerificationKey2021",
                    "id": "z597FwdoYuc71oKc1wvR13o8D7Sdx4u6W3sySp1pVTRXU#2021-07-24T03:09:26.000Z#key-Secp256k1-1",
                    "publicKeyMultibase": "zs5jSP1MiMb4aNxyahBzshhn8ad9DnoPrHaiVyvfVhtzR"
                }
            ],
            "keyAgreement": [
                {
                    "type": "X25519KeyAgreementKey2021",
                    "id": "z597FwdoYuc71oKc1wvR13o8D7Sdx4u6W3sySp1pVTRXU#2021-07-24T03:09:26.000Z#key-X25519-0",
                    "publicKeyMultibase": "zGsfqoxaxPgN2C1zLW3s3qB1EATfQGBFKeTJPsSZQBSGd"
                }
            ],
            "assertionMethod": [
                {
                    "type": "Signature",
                    "id": "z597FwdoYuc71oKc1wvR13o8D7Sdx4u6W3sySp1pVTRXU#2021-07-24T03:09:26.000Z#am--0",
                    "verificationMethod": "z597FwdoYuc71oKc1wvR13o8D7Sdx4u6W3sySp1pVTRXU#2021-07-24T03:09:26.000Z#key-Ed25519-0"
                }
            ],
            "service": [
                {
                    "type": "PublisherService",
                    "id": "z597FwdoYuc71oKc1wvR13o8D7Sdx4u6W3sySp1pVTRXU#2021-07-24T03:09:26.000Z#PublisherService-0",
                    "serviceEndpoint": "https://node0.first-dial.io/z597FwdoYuc71oKc1wvR13o8D7Sdx4u6W3sySp1pVTRXU/publisher"
                },
                {
                    "type": "PublisherService",
                    "id": "z597FwdoYuc71oKc1wvR13o8D7Sdx4u6W3sySp1pVTRXU#2021-07-24T03:09:26.000Z#PublisherService-1",
                    "serviceEndpoint": "https://node23.all-cloud.net/z597FwdoYuc71oKc1wvR13o8D7Sdx4u6W3sySp1pVTRXU/publisher"
                },
                {
                    "type": "PublisherService",
                    "id": "z597FwdoYuc71oKc1wvR13o8D7Sdx4u6W3sySp1pVTRXU#2021-07-24T03:09:26.000Z#PublisherService-2",
                    "serviceEndpoint": "https://www1.empire.us/z597FwdoYuc71oKc1wvR13o8D7Sdx4u6W3sySp1pVTRXU/publisher"
                }
            ]
        }
    ],
    "type": "Declaration",
    "proof": [
        {
            "issuer": "z597FwdoYuc71oKc1wvR13o8D7Sdx4u6W3sySp1pVTRXU",
            "created": "2021-07-24T03:09:26.000Z",
            "proofPurpose": "PoP",
            "type": "JcsBase64Ed25519Signature2021",
            "assertionMethod": [
                "z597FwdoYuc71oKc1wvR13o8D7Sdx4u6W3sySp1pVTRXU#2021-07-24T03:09:26.000Z#am--0"
            ],
            "verificationMethod": "z597FwdoYuc71oKc1wvR13o8D7Sdx4u6W3sySp1pVTRXU#2021-07-24T03:09:26.000Z#key-Ed25519-0",
            "signatureValue": "472J4Aez8h_l1jK8mIMSX6J5ShBaxZeoTK2zb3_2BqsL9ysuFxnC9ZZ043VNPfuokMiYtRdajTgQmQkjACn9BA",
            "nonce": "8df586b8-6ae1-4db3-8f23-c7ae3abc8c77"
        },
        {
            "issuer": "z597FwdoYuc71oKc1wvR13o8D7Sdx4u6W3sySp1pVTRXU",
            "created": "2021-07-24T03:09:26.000Z",
            "proofPurpose": "PoP",
            "type": "JcsBase64Secp256k1Signature2021",
            "verificationMethod": "z597FwdoYuc71oKc1wvR13o8D7Sdx4u6W3sySp1pVTRXU#2021-07-24T03:09:26.000Z#key-Secp256k1-1",
            "signatureValue": "MEUCIQDE_LI9GW_keTbK9vhwzFjcrB0fDZoasPOo-rtVPoZWhgIgaCwuRICUQtHf26-DBYUqDgRdwv0b5_Rl7wbJeGYmv9Q",
            "nonce": "fda28d8c-1497-4757-9e2b-a2f237c5c16f"
        },
        {
            "issuer": "z597FwdoYuc71oKc1wvR13o8D7Sdx4u6W3sySp1pVTRXU",
            "created": "2021-07-24T03:09:26.000Z",
            "proofPurpose": "Assertion",
            "type": "JcsBase64Ed25519Signature2021",
            "assertionMethod": [
                "z597FwdoYuc71oKc1wvR13o8D7Sdx4u6W3sySp1pVTRXU#2021-07-24T03:09:25.000Z#am--0"
            ],
            "verificationMethod": "z597FwdoYuc71oKc1wvR13o8D7Sdx4u6W3sySp1pVTRXU#2021-07-24T03:09:25.000Z#key-Ed25519-0",
            "signatureValue": "uekZFHunbuONGISAhkHWo2Dp0Ncjgdq_yWQ6WNt8FrB1b0VuKxQOPu375asqhGflyY9BD79d82V3MIHhxetXDw",
            "nonce": "bccc2977-203e-44a9-95b3-b873610babe8"
        }
    ]
}
```

## Identifier
The declaration.id field references the participant issuing this declaration. Therefore, there is no need to have a controller rule in a performance declaration. The controller is automatically the controller of the participant with the same identifier.

## Service Records
The performance declaration also exposes service records, associated endpoints and corresponding authentication credentials (assertion method). A single service record has the following architecture:
```json
{
    "type": "PublisherService",
    "id": "z597FwdoYuc71oKc1wvR13o8D7Sdx4u6W3sySp1pVTRXU#2021-07-24T03:09:26.000Z#PublisherService-2",
    "serviceEndpoint": "https://www1.empire.us/z597FwdoYuc71oKc1wvR13o8D7Sdx4u6W3sySp1pVTRXU/publisher"
}
```

### type
Indicate the type of service as decribed in the Dial type registry.

### serviceEndpoint
This is the network endpoint receiving service calls on behalf of the participant. The reason for registering many service endpoints is to increase availability. Those endpoint my be operated by gateway services independent of the registering service provider.

## VerificationMethods and KeyAgreement
A service record is only valid for a time window. It exposes assertion and keyAgreement mechanisms solely associated with this record. Those two verification methods will be forcefully regenerated for each new performance declaration, thus forcing key rotation.

## Proof
In this performance declaration, there are 2 PoP proofs justifying newly generated public keys and one assertion proof of the cotoller of the participant declaration, as it is also the controller of this performance declaration.