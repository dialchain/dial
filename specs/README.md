# Specs

## DialChain
This is a set of files documenting declarations. These files are grouped and chained together into blocks.

## DIAL Network
The DIAL Network is a group of participants that all aggree on the same state of the DialChain. 

## Participant
A [participant](./Participant.md) is an entity that has a representation in the DialChain. A computer in the network, an app on the user's mobile phone can be seen as participants if they are given a unique identifier.

A participant asserts by the mean of generating digital signatures of some declarations.

## Organization
An organization is a participant composed out of other participants. The assertion of an organization is generally a member vote. Introducing the notion of an organization is essential to bridge the path to real word business cases.

## Validator Organization
A [validator](Validator.md) is a organization that can publish entries to the log. DIAL requires each validator to have atleast 3 physically separated validator nodes. This way, the assertion of a validator allways contains two signatures.

# DiD Method DIAL
The DialChain borrows the schema design of [DiD Core](https://www.w3.org/TR/did-core/) to define its organizational structure.

# Proof
A proof is the vehicle we use to document the signature of a declaration. A proof has the following structure:
- It is a JWS detached signature
- The signature payload is file content without the proof subelement.
- The JWS protected header field will be the base64 encoded, canonicalize content of the __"proof"__ block without the __"signatureValue"__ element. 

To produce a signature, 
1- drop the proof subelement, cannonicalize the remaining json file, and compute the base64url encoded string to for the "payload" string.
2- construct a proof object without the signatureValue, cannonicalize the json and use the base64url encoded string as "header" string.
Use the provided private key to sign the String "header.payload"

Do nnot add the alg to the header as signature algorithm is specified in "proof"."type" 

# Declaration
A declaration is the principal element of the DialChain. Following sections introduce the generic schema of the DialChain:

The producer of a declaration will generally attach a signature to that declaration. As the proof is not part of the signed payload, many signers can parallely provide signatures to be embedded into that declaration file. This means we can use a tool to produce a declaration, send it to legitimate signers. Each signer can return the signature, and we will merge all signatures into the multisigned declaration file.
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
This declarationn file can be found in the ipfs under the address 
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
Signatures production relies on the same principles as described above.
1- Remove the proof block
2- Produce a new proof and add to the list of proofs and put the proof block bacck into the document.

Publication only references the declaration file. This way many validators can paralelly publish the same declaration file, each as a proof they validated declarations included in the file.
