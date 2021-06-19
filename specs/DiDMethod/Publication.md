# Publication
A publication is the act of a validator adding a file to a DialChain. For this purpose, a validator  must expose a publisher service.

## Structure of a Publication
The following file shows the template of a publication:
```json
{
    "id": "mZGMyMzljMmItZWM2Yy00MjJjLWI2YTQtNjM0MTk5YzdhMzFm",
    "type": "Publication",
    "document": {
        "id": "mYzRiZGIzMTItNmUxOC00ZDE1LThjNmYtMDgxYWE4YTY5Yzk1",
        "type": "Declaration",
        "declaration": [],
        "proof": []
    },
    "twindow": {
        "start": "2021-06-09T00:00:00Z",
        "end": "2021-06-10T00:00:00Z",
        "a_closing": "2021-06-08T00:00:00Z",
        "a_hash": "S3DUV3H7G5MY3T3D75JQMWXAAAC4UHL4UBS2OJA2JLCCY6NRN4SVDP5HTZ7E54UXKIUMAFIIA6FQBUYEDTHUAFTNCD7WZN5T3DJZCSI",
    },
    "proof": [
        {
            "issuer": "mZjQwN2ZiMGMtMGQxMi00ZjQ3LWEwZDQtZmIwYzM0ODg4NzNm"
        },
        {
            "issuer": "mZmRlNzEwMDgtZjQxMC00OTMwLTkyMWEtY2ZmMTdkN2RjMGIx"
        }
    ]
}
```
### "type": "Publication"
Indicates that this document is a publication.

### "document"
This is the document being published.

### "document"."proof"
Issuer of the document have their signature in the embedded "proof" block.

### "twindow"
This indicates the twindow in which this document is published.

#### "twindow"."a_hash"
This is the hash of the anntecedant block. This is an attestation that the validator aggrees with the state of the antecedant block.

### "proof"
This block documents the signature of nodes of this validator. In the simplest case, 2 of 3 nodes have to sign each declaration for it to be considered valid by the network.

## Sample Publications
The following file shows the sample publication for one of the nodes.
```json
{
    "id": "mZGMyMzljMmItZWM2Yy00MjJjLWI2YTQtNjM0MTk5YzdhMzFm",
    "type": "Publication",
    "document": {
        "id": "mYzRiZGIzMTItNmUxOC00ZDE1LThjNmYtMDgxYWE4YTY5Yzk1",
        "type": "Declaration",
        "declaration": [
            {
                "type": "Participant",
                "id": "mN2I3NTM2MTItMDhlNi00OWU5LWFkMTItMWJlMjRmYWI5Mjlj",
                "created": "2021-06-09T03:42:26.317366Z",
                "controller": [
                    "mN2I3NTM2MTItMDhlNi00OWU5LWFkMTItMWJlMjRmYWI5Mjlj"
                ],
                "verificationMethod": [
                    {
                        "type": "Ed25519VerificationKey2021",
                        "id": "mN2I3NTM2MTItMDhlNi00OWU5LWFkMTItMWJlMjRmYWI5Mjlj#2021-06-09T03:42:26.317366Z#key-0",
                        "publicKeyMultibase": "zEHwiDynVvinC6jjzH5RR4MwgxYPq4xiRagfksAyUPyjv"
                    }
                ],
                "assertionMethod": [
                    {
                        "type": "Signature",
                        "id": "mN2I3NTM2MTItMDhlNi00OWU5LWFkMTItMWJlMjRmYWI5Mjlj#2021-06-09T03:42:26.317366Z#am-0",
                        "verificationMethod": "mN2I3NTM2MTItMDhlNi00OWU5LWFkMTItMWJlMjRmYWI5Mjlj#2021-06-09T03:42:26.317366Z#key-0"
                    }
                ]
            }
        ],
        "proof": [
            {
                "document": "mYzRiZGIzMTItNmUxOC00ZDE1LThjNmYtMDgxYWE4YTY5Yzk1",
                "issuer": "mN2I3NTM2MTItMDhlNi00OWU5LWFkMTItMWJlMjRmYWI5Mjlj",
                "created": "2021-06-09T03:42:26.317366Z",
                "type": "JcsBase64Ed25519Signature2021",
                "assertionMethod": [
                    "mN2I3NTM2MTItMDhlNi00OWU5LWFkMTItMWJlMjRmYWI5Mjlj#2021-06-09T03:42:26.317366Z#am-0"
                ],
                "signatureValue": "o_Nna_q_skVE7-5r3mj8HMAvPBSo1LIiJxbbjT0AWWLJnOWGThWxLLU7-t5_fH0yiv0pd1OyfwjLLU3sUAfeBQ",
                "nonce": "38aab536-9433-47c9-ba17-259bb40a2cad"
            }
        ]
    },
    "twindow": {
        "start": "2021-06-09T00:00:00Z",
        "end": "2021-06-10T00:00:00Z"
    },
    "proof": [
        {
            "document": "mZGMyMzljMmItZWM2Yy00MjJjLWI2YTQtNjM0MTk5YzdhMzFm",
            "issuer": "mZjQwN2ZiMGMtMGQxMi00ZjQ3LWEwZDQtZmIwYzM0ODg4NzNm",
            "created": "2021-06-09T03:42:26.777072Z",
            "type": "JcsBase64Ed25519Signature2021",
            "assertionMethod": [
                "mZWYyYzE1MjItMjU2NS00MzAwLWExNGQtMGYwODNlMzMyMzk1#2021-06-09T03:42:26.705853Z#am-0",
                "mZjQwN2ZiMGMtMGQxMi00ZjQ3LWEwZDQtZmIwYzM0ODg4NzNm#2021-06-09T03:42:26.697626Z#am-0"
            ],
            "signatureValue": "VXbCZedoiIsDirPLaKnRcZb89eO_rZ9J8T7fHEym4bsqLVr8JMyBFy60YGBlDsaHIHaqRPn0Al2AZ_Iv-CFUCg",
            "nonce": "78fc6596-dbbe-4649-8d5a-a062d0561da1"
        },
        {
            "document": "mZGMyMzljMmItZWM2Yy00MjJjLWI2YTQtNjM0MTk5YzdhMzFm",
            "issuer": "mZmRlNzEwMDgtZjQxMC00OTMwLTkyMWEtY2ZmMTdkN2RjMGIx",
            "created": "2021-06-09T03:42:26.777072Z",
            "type": "JcsBase64Ed25519Signature2021",
            "assertionMethod": [
                "mZWYyYzE1MjItMjU2NS00MzAwLWExNGQtMGYwODNlMzMyMzk1#2021-06-09T03:42:26.705853Z#am-0",
                "mZmRlNzEwMDgtZjQxMC00OTMwLTkyMWEtY2ZmMTdkN2RjMGIx#2021-06-09T03:42:26.701615Z#am-0"
            ],
            "signatureValue": "dEl1pl0GNjGS1SZm7JoEP16sv5cLkBXoMC5zbckj5xnEk51qHvltiCoS2HrEwS9jchvJx4jD5qBYPQ8Q_cr5BQ",
            "nonce": "b8eef027-5540-413e-85bc-48617620a3f7"
        }
    ]
}
```

The next file shows the sample publication for the validator organization.
```json
{
    "id": "mNWVkYzJmYTAtNDcxNy00Y2MyLWJkY2MtZTAwMTJhNDYyZDc0",
    "type": "Publication",
    "document": {
        "id": "mMTM0MGRkNTItNzVlMy00YjY3LWFmMDEtZjE0MzhjZDY1YzMy",
        "type": "Declaration",
        "declaration": [
            {
                "type": "Organization",
                "id": "mZWYyYzE1MjItMjU2NS00MzAwLWExNGQtMGYwODNlMzMyMzk1",
                "created": "2021-06-09T03:42:26.705853Z",
                "controller": [
                    "mZWYyYzE1MjItMjU2NS00MzAwLWExNGQtMGYwODNlMzMyMzk1"
                ],
                "assertionMethod": [
                    {
                        "type": "Vote",
                        "id": "mZWYyYzE1MjItMjU2NS00MzAwLWExNGQtMGYwODNlMzMyMzk1#2021-06-09T03:42:26.705853Z#am-0",
                        "quorum": 2,
                        "member": [
                            {
                                "id": "mN2I3NTM2MTItMDhlNi00OWU5LWFkMTItMWJlMjRmYWI5Mjlj",
                                "shares": 1
                            },
                            {
                                "id": "mZjQwN2ZiMGMtMGQxMi00ZjQ3LWEwZDQtZmIwYzM0ODg4NzNm",
                                "shares": 1
                            },
                            {
                                "id": "mZmRlNzEwMDgtZjQxMC00OTMwLTkyMWEtY2ZmMTdkN2RjMGIx",
                                "shares": 1
                            }
                        ]
                    }
                ],
                "service": [
                    {
                        "type": "PublisherService",
                        "id": "mZWYyYzE1MjItMjU2NS00MzAwLWExNGQtMGYwODNlMzMyMzk1#2021-06-09T03:42:26.705853Z#PublisherService-0",
                        "serviceEndpoint": "https://node0.first-dial-validator.io/publisher",
                        "assertionMethod": "mZWYyYzE1MjItMjU2NS00MzAwLWExNGQtMGYwODNlMzMyMzk1#2021-06-09T03:42:26.705853Z#am-0"
                    },
                    {
                        "type": "PublisherService",
                        "id": "mZWYyYzE1MjItMjU2NS00MzAwLWExNGQtMGYwODNlMzMyMzk1#2021-06-09T03:42:26.705853Z#PublisherService-1",
                        "serviceEndpoint": "https://node1.first-dial-validator.io/publisher",
                        "assertionMethod": "mZWYyYzE1MjItMjU2NS00MzAwLWExNGQtMGYwODNlMzMyMzk1#2021-06-09T03:42:26.705853Z#am-0"
                    },
                    {
                        "type": "PublisherService",
                        "id": "mZWYyYzE1MjItMjU2NS00MzAwLWExNGQtMGYwODNlMzMyMzk1#2021-06-09T03:42:26.705853Z#PublisherService-2",
                        "serviceEndpoint": "https://node2.first-dial-validator.io/publisher",
                        "assertionMethod": "mZWYyYzE1MjItMjU2NS00MzAwLWExNGQtMGYwODNlMzMyMzk1#2021-06-09T03:42:26.705853Z#am-0"
                    },
                    {
                        "type": "LookupService",
                        "id": "mZWYyYzE1MjItMjU2NS00MzAwLWExNGQtMGYwODNlMzMyMzk1#2021-06-09T03:42:26.705853Z#LookupService-0",
                        "serviceEndpoint": "https://open.first-dial-validator.io/lookup",
                        "assertionMethod": "mZWYyYzE1MjItMjU2NS00MzAwLWExNGQtMGYwODNlMzMyMzk1#2021-06-09T03:42:26.705853Z#am-0"
                    }
                ]
            }
        ],
        "proof": [
            {
                "document": "mMTM0MGRkNTItNzVlMy00YjY3LWFmMDEtZjE0MzhjZDY1YzMy",
                "issuer": "mN2I3NTM2MTItMDhlNi00OWU5LWFkMTItMWJlMjRmYWI5Mjlj",
                "created": "2021-06-09T03:42:26.754921Z",
                "type": "JcsBase64Ed25519Signature2021",
                "assertionMethod": [
                    "mZWYyYzE1MjItMjU2NS00MzAwLWExNGQtMGYwODNlMzMyMzk1#2021-06-09T03:42:26.705853Z#am-0",
                    "mN2I3NTM2MTItMDhlNi00OWU5LWFkMTItMWJlMjRmYWI5Mjlj#2021-06-09T03:42:26.317366Z#am-0"
                ],
                "signatureValue": "H5vF6u7jMeBm0QS5KPDjZt_hb-Gdh5X4oWMS-rV3BzzsIReBb_1Tr0Z8HyubiZ5xQV34t7Y7VuiK44uysjH7Bg",
                "nonce": "dfea6186-b710-46a5-8451-64185c9af1d8"
            },
            {
                "document": "mMTM0MGRkNTItNzVlMy00YjY3LWFmMDEtZjE0MzhjZDY1YzMy",
                "issuer": "mZjQwN2ZiMGMtMGQxMi00ZjQ3LWEwZDQtZmIwYzM0ODg4NzNm",
                "created": "2021-06-09T03:42:26.767556Z",
                "type": "JcsBase64Ed25519Signature2021",
                "assertionMethod": [
                    "mZWYyYzE1MjItMjU2NS00MzAwLWExNGQtMGYwODNlMzMyMzk1#2021-06-09T03:42:26.705853Z#am-0",
                    "mZjQwN2ZiMGMtMGQxMi00ZjQ3LWEwZDQtZmIwYzM0ODg4NzNm#2021-06-09T03:42:26.697626Z#am-0"
                ],
                "signatureValue": "jngrOrEwZSCx-lHKUfhwHipjnNal6vk2Wv0_fDmhGNRfxuBStERuutiS_vsXe24sdhVdxATsfJtxQt5ggSucBA",
                "nonce": "94f8f4c0-cf44-4b31-9245-ee50f3a2e693"
            },
            {
                "document": "mMTM0MGRkNTItNzVlMy00YjY3LWFmMDEtZjE0MzhjZDY1YzMy",
                "issuer": "mZmRlNzEwMDgtZjQxMC00OTMwLTkyMWEtY2ZmMTdkN2RjMGIx",
                "created": "2021-06-09T03:42:26.773016Z",
                "type": "JcsBase64Ed25519Signature2021",
                "assertionMethod": [
                    "mZWYyYzE1MjItMjU2NS00MzAwLWExNGQtMGYwODNlMzMyMzk1#2021-06-09T03:42:26.705853Z#am-0",
                    "mZmRlNzEwMDgtZjQxMC00OTMwLTkyMWEtY2ZmMTdkN2RjMGIx#2021-06-09T03:42:26.701615Z#am-0"
                ],
                "signatureValue": "VvUwUBUM9pl9vT_sLP6Gosnb4g4rWGvG3vrm8ON_5jzeSwI3H12pndaWqUXakjl1ITLt8C1WQUFwxBOFc0JJDQ",
                "nonce": "f1b0ede0-4015-4fad-9b1b-407d0e300010"
            }
        ]
    },
    "twindow": {
        "start": "2021-06-09T00:00:00Z",
        "end": "2021-06-10T00:00:00Z"
    },
    "proof": [
        {
            "document": "mNWVkYzJmYTAtNDcxNy00Y2MyLWJkY2MtZTAwMTJhNDYyZDc0",
            "issuer": "mZjQwN2ZiMGMtMGQxMi00ZjQ3LWEwZDQtZmIwYzM0ODg4NzNm",
            "created": "2021-06-09T03:42:26.777072Z",
            "type": "JcsBase64Ed25519Signature2021",
            "assertionMethod": [
                "mZWYyYzE1MjItMjU2NS00MzAwLWExNGQtMGYwODNlMzMyMzk1#2021-06-09T03:42:26.705853Z#am-0",
                "mZjQwN2ZiMGMtMGQxMi00ZjQ3LWEwZDQtZmIwYzM0ODg4NzNm#2021-06-09T03:42:26.697626Z#am-0"
            ],
            "signatureValue": "RON0Sp3QbC_cRZj2Rob1aSPSA4Nl4sJbORL6diPLBLwbHj9x95sqltoINu5N71RWEHUnNAY4MarN537QVhmMDw",
            "nonce": "595a47ab-8f5a-4e0f-a54e-33cf5def17cd"
        },
        {
            "document": "mNWVkYzJmYTAtNDcxNy00Y2MyLWJkY2MtZTAwMTJhNDYyZDc0",
            "issuer": "mZmRlNzEwMDgtZjQxMC00OTMwLTkyMWEtY2ZmMTdkN2RjMGIx",
            "created": "2021-06-09T03:42:26.777072Z",
            "type": "JcsBase64Ed25519Signature2021",
            "assertionMethod": [
                "mZWYyYzE1MjItMjU2NS00MzAwLWExNGQtMGYwODNlMzMyMzk1#2021-06-09T03:42:26.705853Z#am-0",
                "mZmRlNzEwMDgtZjQxMC00OTMwLTkyMWEtY2ZmMTdkN2RjMGIx#2021-06-09T03:42:26.701615Z#am-0"
            ],
            "signatureValue": "OoRxRp75lIMO_hztkHZv66N2ze6s4_kCEwEtCnq_pbxU9Imoe_3GjhUe1EIUj8x8Ngd4Ad4uNYfBAhRJ5K0BAQ",
            "nonce": "af21f291-3f54-4e42-b800-7d21732c2efa"
        }
    ]
}
```
# Genesis Publications
At the bootstraping of the DialChain, each validator will publish their own genesis record to the chain. Genesis records consist of consists of:

- The declaration record of all 3 nodes
- The declaration record of the validator
- The declaration of the DIAL treasury

These files will be exposed on a bootstrap server, exposed in the project source repository.

Genesis files will not have antecedant hashes.

## Dial Treasury