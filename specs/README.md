# Specs
The dial network is a permissionless network made out of tokens. Everything in the dial network (participants, assets, protocols) is represented with a token.

# Token
A [token](./Token.md) is a unit of existance in the dial network. Each token has an identifier. The following schema is the most simplified type of a token:
```json
{
    "type": "Declaration",
    "declaration": [
        {
            "type": "token-type",
            "id": "token-id",
        }
    ]
}
```
The id of an active token is unique among all active tokenn in the network. The id of an expired token can be reused.

# Entities
An entity is a unit of interaction. An entity can therefore produce assertions.

## Verification Method
The simplest form of an entity is a verification method. This is a public key, enhanced with the indication of key algorithm associated with the key. Bellow is the example of a standalone verification method:
```json
{
    "type": "Ed25519VerificationKey2021",
    "publicKeyMultibase": "z4DiXDE9t44qkq6uGmrhwWZHsTFofqmaKvuTWq687UawA"
}
```

## Participant
A [participant](./Participant.md) is an entity that has a representation in the dial network. A computer in the network, an app on the user's mobile phone can be seen as participants if they are given a unique identifier. A participant asserts by the mean of generating digital signatures of some declarations. A participant decalaration is used to list verification and assertion methods exposed by the participant.

## Validator
A [validator](./Validator.md) is an active participant that takes the duty of validating declarations sent by other participants to the network.

## Organization
An [organization](./Organization.md) is a participant composed out of other participants which act as members. The assertion of an organization is generally a member's vote. Introducing the notion of an organization is essential to bridge the path to real word business cases.

# DiD Method DIAL
The dial chain borrows the schema design of [DiD Core](https://www.w3.org/TR/did-core/) to define organizational structures.

# Proof
A proof is the vehicle we use to document the signature of a declaration. A proof has the following structure:
- It is a JWS detached signature
- The signature payload is a file content without the proof subelement.
- The JWS protected header field will be the base64 encoded, canonicalized content of the __"proof"__ block without the __"signatureValue"__ element. 

To produce a signature, (1) drop the proof subelement, (2) canonicalize the remaining json file, and (3) compute the base64 urlencoded string for the "payload" string. (4) Construct a proof object without the signatureValue, (5) canonicalize the json and use the base64 urlencoded string as "header" string.
(6) Use the provided private key to sign the String "header.payload"

Do not add the algorithm to the header as signature algorithm is specified in "proof"."type" 

# Declaration
A declaration is the principal element of the dial chain. Following sections introduce the generic schema of a declaration:

The producer of a declaration must attach a signature to that declaration. As the proof is not part of the signed payload, many signers can parallely provide signatures to be embedded into that declaration file. This means we can use a tool to produce a declaration, send it to legitimate signers. Each signer can return the signature, and we will aggregate all signatures into the multisigned declaration file.
```json
{
    "type": "Declaration",
    "declaration": [
        {
            "type": "Participant",
            "id": "z4DiXDE9t44qkq6uGmrhwWZHsTFofqmaKvuTWq687UawA",
            "created": "2021-06-24T21:36:02.970369Z",
            "controller": [
                "z4DiXDE9t44qkq6uGmrhwWZHsTFofqmaKvuTWq687UawA"
            ],
            "account": [
                {
                    "network": "org.bitcoin.production",
                    "address": "bc1qwu8ngtunq876z3szrjps83pnac0dvkmnpp5r92",
                    "control": {
                        "quorum": 1,
                        "verificationMethod": [
                            "z4DiXDE9t44qkq6uGmrhwWZHsTFofqmaKvuTWq687UawA#2021-06-24T21:36:02.970369Z#key-1"
                        ]
                    }
                }
            ],
            "verificationMethod": [
                {
                    "type": "Ed25519VerificationKey2021",
                    "id": "z4DiXDE9t44qkq6uGmrhwWZHsTFofqmaKvuTWq687UawA#2021-06-24T21:36:02.970369Z#key-0",
                    "publicKeyMultibase": "z4DiXDE9t44qkq6uGmrhwWZHsTFofqmaKvuTWq687UawA"
                },
                {
                    "type": "Secp256k1VerificationKey2021",
                    "id": "z4DiXDE9t44qkq6uGmrhwWZHsTFofqmaKvuTWq687UawA#2021-06-24T21:36:02.970369Z#key-1",
                    "publicKeyMultibase": "z4vPPSUtMuYdxBLSUAskw5xU7QeN2ksXqrxJdLBfz93LSHVn8kE9pfVkmyLVLmhKbBCvdFoUBadr1h1qBFWdmQFGD"
                }
            ],
            "assertionMethod": [
                {
                    "type": "Signature",
                    "id": "z4DiXDE9t44qkq6uGmrhwWZHsTFofqmaKvuTWq687UawA#2021-06-24T21:36:02.970369Z#am-0",
                    "verificationMethod": "z4DiXDE9t44qkq6uGmrhwWZHsTFofqmaKvuTWq687UawA#2021-06-24T21:36:02.970369Z#key-0"
                }
            ]
        }
    ],
    "proof": [
        {
            "issuer": "z4DiXDE9t44qkq6uGmrhwWZHsTFofqmaKvuTWq687UawA",
            "created": "2021-06-24T21:36:02.970369Z",
            "proofPurpose": "PoP",
            "type": "JcsBase64Ed25519Signature2021",
            "verificationMethod": "z4DiXDE9t44qkq6uGmrhwWZHsTFofqmaKvuTWq687UawA#2021-06-24T21:36:02.970369Z#key-0",
            "signatureValue": "lXJZ6nyja7KKVd84sXn9yaM1LX1c3h0zkbrsJLz7PimgHec3FpfQwnUvkMZtbB_ScDfQ0oyD3rNxqr74g-L3Bg",
            "nonce": "3cd01565-c4bc-463f-a731-09e2bf665af6"
        },
        {
            "issuer": "z4DiXDE9t44qkq6uGmrhwWZHsTFofqmaKvuTWq687UawA",
            "created": "2021-06-24T21:36:02.970369Z",
            "proofPurpose": "PoP",
            "type": "JcsBase64Secp256k1Signature2021",
            "verificationMethod": "z4DiXDE9t44qkq6uGmrhwWZHsTFofqmaKvuTWq687UawA#2021-06-24T21:36:02.970369Z#key-1",
            "signatureValue": "A06ni1Xjn4pvpVF7ATl2Adqy1k1_SL2ZtJCkgSkpfpduBehTvO6NuKCKjyXnQ8-UWRBfV8NKJcB7RnEZsPGyKw",
            "nonce": "bc008c5e-c0cf-4844-93cb-9726ae2d0d50"
        }
    ]
}
```
This declaration files is immutable and can be found on the IPFS Network under the content address 
```json
"B7NCfE8n7A7h5jYzLRHyzwavpsraT3PogzSJx22P9JYcXMCBifMnbNTh4SaS1mJH76rtPBB3RLBjrw2sqeBPS1boHFsj"
```

# Publication
A publication is the act of a validator signing the file and sharing with to order validators. The publication of the declaration above looks like:

```json
{
    "type": "Publication",
    "cid": [
        "B7NCfE8n7A7h5jYzLRHyzwavpsraT3PogzSJx22P9JYcXMCBifMnbNTh4SaS1mJH76rtPBB3RLBjrw2sqeBPS1boHFsj"
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
            "signatureValue": "74MmBkLApfDQF_HGfqeCzIoV6VYNPxFktUwLpXtdseolyOxiym4P570mnGQ2Zzg8Y57gtjz9E_yW_A6kuMw2Cg",
            "nonce": "3b438f5c-2991-4e77-8dea-a688f917639a"
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
            "signatureValue": "L8fX1-ozmL33chs1t3ljPLzQ42YhK1os1yiqGAbK4hUCzzck0gS01mzqy3XzZeSadI_Wig5cB1xhTmK9_KN_Bw",
            "nonce": "1b57468f-502a-40c3-ac47-7844cb703370"
        }
    ]
}
```
Signatures production relies on the same principles as described above. (1) Remove the proof block,
 (2) Produce a new proof and (3) add the new proof to the list of proofs and put the proof block back into the document.

A publication file is mutable, as it can be updated with validator signatures as they are provided. The actual version of the publication must be store under the ipns address of the declaration's identifier (public key identifying the declaration).

# Contoller
The controller of a declaration is the entity authorized to change the declaration. A controller can be a simple verification method, a participant or an organization identifier.

The controller block of a __Constrained Tokens__ provide the network with the possibility of constraining the exchange of that token. (1) the authenticated witness protocol requires the (new) controller of a token to provide an offchain proof of identification, while staying anonymous onchain, (2) time lock contracts will delay the time to change control of the enclosing token, (3) hash locked contracts will allow the designated participant to control the enclosing token if it presents the seed of the given hash, (4) combination thereof might also be applied to constrain token disposition.