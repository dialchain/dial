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
The producer of a declaration will generally attach a signature to that declaration. As the proof is not part of the signed payload, many signers can parallely provide signatures to be embedded into that declaration file. This means, I can use a tool to produce a declaration, send it to legitimate signers. Each signer can return the signature, and I will merge all signatures into the multisigned declaration file.
```json
{
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
}
```
## Detached Signature
If the declaration file is published to the log before all signers provide their assertions, additional signatures can be collected afterward.
```json
{
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
}
```
Detached signatures are used in many use cases:
- when it is legally necessary to document the time of signature of each signing member. The time of signature might have legal implications on the outcome a business case.
- when a business process separates a reservation of fund from the release fund. e.g.: the accountant generating and signing a series of pay slips at the end of the month, hereby making the reserved fund unspendable. With a given number of signatures of treasurers, the fund will finally be released.
- in token governed DAO, each token holder will cast a vote by providing a signature of the given declaration in a separate document.

## "declaration"."id"
The unique identifier of this declaration file. A declaration file can appear multiple times in the DialChain, as the same declaration can be parallelly published by many validators.

## "declaration"."entries"."type"
The declaration type indicates the structure and format of data held by this declaration. 

## "declaration"."entries"."type":"ref"
If the type is a reference, the cid points to another declaration file existing in the DialChain. This will generally be the case for template declarations.

## "declaration"."entries"."cid"
The cid version 1 identifier of the canonicalized content of another declaration (Not the declaration file).

# Publication
A publication is the act of a validator signing the file and sharing with to order validators. A published file looks like:

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

The publication entries are allways attached. The signature data is everything else in the file except the __top level "proof"__ entry itself. Single proofs entries can be produced paralelly.

## "proof"."assertionMethod"
In the default configuration, a publication will be signed by two of three members of the validator organization, reducing the risk of verification mistakes and the risk of spam publications due to the lost a validator node's private key.

- The first entry in the list of assertionMethods references the signature rule defined in the idenntity declaration of the validator organization.
- The second entry references the assertionMethod defined in the identity declaration of the validator node (member).

In the following expression:
```json
{
    "assertionMethod": [
        "mZWYyYzE1MjItMjU2NS00MzAwLWExNGQtMGYwODNlMzMyMzk1#2021-06-09T03:42:26.705853Z#am-0",
        "mZmRlNzEwMDgtZjQxMC00OTMwLTkyMWEtY2ZmMTdkN2RjMGIx#2021-06-09T03:42:26.701615Z#am-0"
    ]
}
```

- __mZWYyYzE1MjItMjU2NS00MzAwLWExNGQtMGYwODNlMzMyMzk1#2021-06-09T03:42:26.705853Z#am-0__ is the asertionMethod as defined in the organization declaration file.
- __mZmRlNzEwMDgtZjQxMC00OTMwLTkyMWEtY2ZmMTdkN2RjMGIx#2021-06-09T03:42:26.701615Z#am-0__ is the assertionMethod as defined in the node declaration file.

### Validation Rule DECL0001
The last element in the list of assertionMethod must allways be the assertion method of a simple participant.

### Validation Rule DECL0002
The list of assertionMethod must form a directed delegation chain (means can not be circcular).
  
### Validation Rule DECL0003
Event though there is no limit on the dept of the assertion chain, the deeper the delegation chain, the most complicated is the validation. Therefore the more expensive will be the insertion into the chain.