# Specs

## DialChain
This is a set of files documenting declarations. These files are grouped and chained together into blocks.

## DIAL Network
The DIAL Network is a group of participants that all aggree on the same state of the DialChain. 

## Participant
A [participant](./Participant.md) is an entity that has a representation in the DialChain. A computer in the network, an app on the user's mobile phone can be seen as participants if they are given a unique identifier.

A participant asserts by the mean of generating digital signatures of some declarations.

## Organization
An organization is a participant composed out of other participants. The assertion of an organization is generally a member vote. Introducinng the notion of an organization is essential to the bridge the path to real word businesses into the DialChain.

## Validator Organization
A [validator](Validator.md) is a organization that can publish entries to the log. DIAL requires each validator to have atleast 3 physically separated validator nodes. This way, the assertion of a validator allways contains two signatures.

# DiD Method DIAL
The DialChain borrows the schema design of [DiD Core](https://www.w3.org/TR/did-core/) to define its organizational structure.

# Proof
A proof is the vehicle we use to document the signature of a declaration. A proof has the following structure:
- It is a JWS detached signature
- The signature payload is the canonicalized content of the __"declarations"__ block (see bellow).
- The JWS protected header field will be the base64 encoded, canonicalize content of the __"proof"__ block without the __"signatureValue"__ element. 

# Declaration
A declaration is the principal element of the DialChain. Following sections introduce the generic schema of the DialChain:

## Declaration with Attached Signature
The producer of a declaration will generally attach a signature to that declaration. As the proof is not part of the signed payload, many signers can parallely provide signatures to be embedded into that declaration file. This means we can use a tool to produce a declaration, send it to legitimate signers. Each signer can return the signature, and I will merge all signatures into the multisigned declaration file.
```json
{
    "id": "mZjliODYxNGMtNjJmYS00OTdiLWI4OTUtZWQ5NWM1NzkzYzk0",
    "type": "Declaration",
    "declaration": [
        {
            "type": "Participant",
            "id": "mMGY3ZmZkZmMtM2E5MS00MjM1LTg0MjQtZjBlYzNjODVhMDA5",
            "created": "2021-06-16T20:39:15.429685Z",
            "controller": [
                "mMGY3ZmZkZmMtM2E5MS00MjM1LTg0MjQtZjBlYzNjODVhMDA5"
            ],
            "account": [
                {
                    "network": "org.bitcoin.production",
                    "address": "bc1qdnlhfq2jhll0ntsa36es6uxldczeu23q4cvqv8",
                    "control": {
                        "quorum": 1,
                        "verificationMethod": [
                            "mMGY3ZmZkZmMtM2E5MS00MjM1LTg0MjQtZjBlYzNjODVhMDA5#2021-06-16T20:39:15.429685Z#key-1"
                        ]
                    }
                }
            ],
            "verificationMethod": [
                {
                    "type": "Ed25519VerificationKey2021",
                    "id": "mMGY3ZmZkZmMtM2E5MS00MjM1LTg0MjQtZjBlYzNjODVhMDA5#2021-06-16T20:39:15.429685Z#key-0",
                    "publicKeyMultibase": "z8oVsDfgnTUwr2MRsLdcP7mGmezM6z1k9Js6ZGz9rRVXr"
                },
                {
                    "type": "Secp256k1VerificationKey2021",
                    "id": "mMGY3ZmZkZmMtM2E5MS00MjM1LTg0MjQtZjBlYzNjODVhMDA5#2021-06-16T20:39:15.429685Z#key-1",
                    "publicKeyMultibase": "z3GsP69NzBnAZg4W3WM5Dc5MYkn8rgSMi68bZ7dYVwiBPKvGW2r1CSvGm2Tp6MnYdroqayz5W9YzjzBeRoHwRXrAU"
                }
            ],
            "assertionMethod": [
                {
                    "type": "Signature",
                    "id": "mMGY3ZmZkZmMtM2E5MS00MjM1LTg0MjQtZjBlYzNjODVhMDA5#2021-06-16T20:39:15.429685Z#am-0",
                    "verificationMethod": "mMGY3ZmZkZmMtM2E5MS00MjM1LTg0MjQtZjBlYzNjODVhMDA5#2021-06-16T20:39:15.429685Z#key-0"
                }
            ]
        }
    ],
    "proof": [
        {
            "document": "mZjliODYxNGMtNjJmYS00OTdiLWI4OTUtZWQ5NWM1NzkzYzk0",
            "issuer": "mMGY3ZmZkZmMtM2E5MS00MjM1LTg0MjQtZjBlYzNjODVhMDA5",
            "created": "2021-06-16T20:39:15.429685Z",
            "proofPurpose": "PoP",
            "type": "JcsBase64Ed25519Signature2021",
            "verificationMethod": "mMGY3ZmZkZmMtM2E5MS00MjM1LTg0MjQtZjBlYzNjODVhMDA5#2021-06-16T20:39:15.429685Z#key-0",
            "signatureValue": "F3ouXdRHl5xVDbuimXu1zNG3NUbzs5AIXWb9W1dZ8rz_eRY_9yfoANUEJ_nH_0-0CmaPxHYrNMHSafBWv4i5CA",
            "nonce": "4c03739d-2840-4d2d-b7ff-920cb2f72d0a"
        },
        {
            "document": "mZjliODYxNGMtNjJmYS00OTdiLWI4OTUtZWQ5NWM1NzkzYzk0",
            "issuer": "mMGY3ZmZkZmMtM2E5MS00MjM1LTg0MjQtZjBlYzNjODVhMDA5",
            "created": "2021-06-16T20:39:15.429685Z",
            "proofPurpose": "PoP",
            "type": "JcsBase64Secp256k1Signature2021",
            "verificationMethod": "mMGY3ZmZkZmMtM2E5MS00MjM1LTg0MjQtZjBlYzNjODVhMDA5#2021-06-16T20:39:15.429685Z#key-1",
            "signatureValue": "Zsux1wa3-d1U8EGoo6RYXUAhLAdUyrtS82hj-5WmEKdxZNuvgSVxL4otNkYQJ4vr9DJWSRLuiJFpZEipwhJVHQ",
            "nonce": "4935aafa-395b-4362-9a3e-4c20a995ad2f"
        }
    ]
}
```

# Publication
A publication is the act of a validator signing the file and sharing with to order validators. A published file looks like:

```json
{
    "id": "mMDYzN2VjMzktMjhhOC00MjU5LWFkYmEtNGMwNTkzYTAyYmI1",
    "type": "Publication",
    "document": {
        "id": "mODI4ZTFkMjAtY2NkMC00YjBjLWFjNjUtMDVjMzRkNTg4NGJm",
        "type": "Declaration",
        "declaration": [ "content of the organization declaration, including voting rules."],
        "proof": ["assertions (signatures) of all members of the organization."]
    },
    "twindow": {
        "start": "2021-06-20T00:00:00Z",
        "end": "2021-06-21T00:00:00Z",
        "missing": "a_closinng & a_hash are not available in the genesis records, as these are the first records."
    },
    "proof": [
        {
            "document": "mMDYzN2VjMzktMjhhOC00MjU5LWFkYmEtNGMwNTkzYTAyYmI1",
            "issuer": "mY2VlZjZjOTItYzM5Yi00MzBlLTljMGMtMjI0MjZiMTY0Yzdl",
            "created": "2021-06-20T00:04:36.462561Z",
            "type": "JcsBase64Ed25519Signature2021",
            "assertionMethod": [
                "mNGI5YjBmNTgtODBmMy00NmQwLTk5YmMtNTUwNWI0MTJiZWJh#2021-06-20T00:04:31.742503Z#am-0",
                "mY2VlZjZjOTItYzM5Yi00MzBlLTljMGMtMjI0MjZiMTY0Yzdl#2021-06-20T00:04:31.723188Z#am-0",
                "mY2VlZjZjOTItYzM5Yi00MzBlLTljMGMtMjI0MjZiMTY0Yzdl#2021-06-20T00:04:31.723188Z#key-0"
            ],
            "signatureValue": "QPtPQVqQmFJLaImsXe1QOZfStmcvP6NZ2N7cbIU35jSX2ShbFKcTu6vMnFeIZmv9r9JdOsacwQMzQwwq3WEeDg",
            "nonce": "68dc7243-655c-4521-bdfb-6c6b83718981"
        },
        {
            "document": "mMDYzN2VjMzktMjhhOC00MjU5LWFkYmEtNGMwNTkzYTAyYmI1",
            "issuer": "mNDA5MTVkNzMtZDU3Mi00YzgwLWI3OWEtMDFjZDI4NGNlNGU0",
            "created": "2021-06-20T00:04:36.462561Z",
            "type": "JcsBase64Ed25519Signature2021",
            "assertionMethod": [
                "mNGI5YjBmNTgtODBmMy00NmQwLTk5YmMtNTUwNWI0MTJiZWJh#2021-06-20T00:04:31.742503Z#am-0",
                "mNDA5MTVkNzMtZDU3Mi00YzgwLWI3OWEtMDFjZDI4NGNlNGU0#2021-06-20T00:04:31.731667Z#am-0",
                "mNDA5MTVkNzMtZDU3Mi00YzgwLWI3OWEtMDFjZDI4NGNlNGU0#2021-06-20T00:04:31.731667Z#key-0"
            ],
            "signatureValue": "mBv7BNpY9-ZD1thqglMmTK_oRu1MjXZ6GGxDe-T8UFto7Uki4soMoaFVIoeVEG3QcoCrjzltjot2B5J4OoVeBQ",
            "nonce": "0ac6719e-fa3f-4a9d-bf9b-f4a069b7e612"
        }
    ]
}
```

The publication entries are allways attached. The signature data is everything else in the file except the __top level "proof"__ entry itself. Single proofs entries can be produced paralelly.
