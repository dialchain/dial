# Participant
A participant is the atomic unit of decision (Entity) in the DialChain. Each participant is represented by a decentralized identifier.

# Simple Participant
A simple participant is one that can express a cryptographic signature. The following document shows the declaration of a simple participant record.
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

## [id]
Identifier of __DIAL file__.

### Validation Rule DIAL00001:
Each dial file has a unique identifier held in the top level element named __id__.

## [type]
Type of the dial file. In this case a declaration.

### Validation Rule DIAL00002:
Each dial file has a predefined type held in the top level element named __type__. There is no unknown type.

## [declaration]
This top level element holds the list of declarations included in this DIAL file.

## [declaration][i]
Defines a single decclaration entry.

## [declaration][i][type]
Type of the declaration entry.

## [declaration][i][id]
The unique identifier of the declaration. If this is a participant declaration, [id] will be the unique identifier of the participant. This shall be unique as the DialChain does not allow for duplicate declarations. A new declaratation with the same [id] is considered a modification of the existing declaration. 

### Validation Rule DIAL00003
Each declaration ha a unique identifier. The submission of a new declaration carrying this same [id] is understood  by the network as a modification request. Validator will make sure modificator prooves conntrol of the document as defined by the controller block of the latest version of this declaration.

## [declaration][controller]
Rules that authorize changes made on this declaration.

### Valdidation Rule DIAL00004
A declaration without a controller block can never be modified.

## [declaration][i][account]
Declares an account associated with this declaration.

## [declaration][i][account][network]
DLT network hosting this account. For the case above, "org.bitcoin.production" is the main net of bitcoin.

## [declaration][i][account][address]
The address of this account as known to the network. E.g. bc1qdnlhfq2jhll0ntsa36es6uxldczeu23q4cvqv8 is the P2WPKH address of this accounnt in the bitcoin's mainnet.

## [declaration][i][account][control]
Optional definition of rules cotroling operations on the enclosing account in the given network.

## [declaration][i][account][control][verificationMethod]
In this case, we are exposing a verification method that can be used to control access to that account inn the given network.

## [declaration][i][account][control][quorum]
In this case just for completeness. In case a conntrol block has many verification methods, a quorum will define the number n of verfication methods that muss be  performed  to exercise control.

## [declaration][i][verificationMethod]
Declaration of public keys associated with this declaration. In this case public keys used to produce proofs by this participant. Note that to keep schema simple and reduce ambiguity, we do not allow the controller property inside a verification relationship (like verificationMethod, assertionMethod). The global controller of the declaration is the only one allowed to modify the declaration.

### Valdidation Rule DIAL00005
The producer of a verification method, must proove possession of the verification method inside the same  declaration file.

## [declaration][i][verificationMethod][type]
Specifies how to use the declare verification method. For example: __Ed25519VerificationKey2021__ describes how to read and consume the ed25519 public key included in this block.

## [declaration][i][verificationMethod][id]
Networkwide unique identifier used to reference this veriification method inside this declaration file and outside this declaration file.

### Valdidation Rule DIAL00006
This identifier of a verification method must allways be prefixed with the identifier of the enclosing deccclaration entity (participant, validator, ...). Dereferencing the verificcation method identifier (string before the first #) returns the identifier of the enclosing declaration entiry.

## [declaration][i][verificationMethod][publicKeyMultibase]
The multibase representation of the public key of this verificcation method.

## [declaration][i][assertionMethod]
Reference on verificationMethods used to validate assertions produced by the encclosing entity.

## [declaration][i][assertionMethod][type]
Defines the data format of the assertionMethod. In this case "Signature" stands for a simple signature.

## [declaration][i][assertionMethod][id]
Networkwide unique identifier used to reference this assertion method inside this declaration file and outside this declaration file.

## [declaration][i][assertionMethod][verificationMethod]
Reference to the verification method used to perform this assertion method.

## [proof]
Collects proofs associated with declarations being submitted. For a simple participant declaration, the proof allows the validation of the declared  verificationMethod (or public key).

## [proof][i][document]
References the document subject of this proof. In this case the id of the ccontaining DIAL file.

## [proof][i][issuer]
Identifier of the declaration entity issuing this proof. In this case the id of the participant.

## [proof][i][created]
Date of production of this proof.

## [proof][i][proofPurpose]
The purpose of this proof. In this case PoP stands for proof of possession. The participant signs the self produced declaration to proove possession of the private key associated with the publick key in the referenced verification method.

## [proof][id][type]
The type of this proof. Defines how the proof is produced and validated.

## [proof][id][verificationMethod]
The verification method associated with the proof. This is the source of the public key used to verify the proof.

## [proof][id][signatureValue]
The value of the signature.

## [proof][id][nonce]
Optional nonce included in the signature, as defined by the "type" element of the proof.