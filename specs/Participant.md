# Participant
A participant is the atomic unit of decision (Entity) in the DialChain. Each participant is represented by a decentralized identifier.

# Simple Participant
A simple participant is one that can express a cryptographic signature. The following document shows the declaration of a simple participant record.
```json
{
    "type": "Declaration",
    "declaration": [
        {
            "type": "Participant",
            "id": "zEruWfhngbEc16jmpZBHSk4Tx872CHDWXeNsDJfL8yHo6",
            "created": "2021-06-24T21:36:03.409110Z",
            "controller": [
                "zEruWfhngbEc16jmpZBHSk4Tx872CHDWXeNsDJfL8yHo6"
            ],
            "account": [
                {
                    "network": "org.bitcoin.production",
                    "address": "bc1qsnkmknavy85xqvya8p4hykpuwaf2kx77w402rq",
                    "control": {
                        "quorum": 1,
                        "verificationMethod": [
                            "zEruWfhngbEc16jmpZBHSk4Tx872CHDWXeNsDJfL8yHo6#2021-06-24T21:36:03.409110Z#key-1"
                        ]
                    }
                }
            ],
            "verificationMethod": [
                {
                    "type": "Ed25519VerificationKey2021",
                    "id": "zEruWfhngbEc16jmpZBHSk4Tx872CHDWXeNsDJfL8yHo6#2021-06-24T21:36:03.409110Z#key-0",
                    "publicKeyMultibase": "zEruWfhngbEc16jmpZBHSk4Tx872CHDWXeNsDJfL8yHo6"
                },
                {
                    "type": "Secp256k1VerificationKey2021",
                    "id": "zEruWfhngbEc16jmpZBHSk4Tx872CHDWXeNsDJfL8yHo6#2021-06-24T21:36:03.409110Z#key-1",
                    "publicKeyMultibase": "z5NQ1z6E3S6rVbbfTWxT8VX4NUAYsD2Y6p9EMkZjdov4wEpoWXceM7vY5fZTdkPJt6kKEpVu9TLMExCqoCj1T5mT6"
                }
            ],
            "assertionMethod": [
                {
                    "type": "Signature",
                    "id": "zEruWfhngbEc16jmpZBHSk4Tx872CHDWXeNsDJfL8yHo6#2021-06-24T21:36:03.409110Z#am-0",
                    "verificationMethod": "zEruWfhngbEc16jmpZBHSk4Tx872CHDWXeNsDJfL8yHo6#2021-06-24T21:36:03.409110Z#key-0"
                }
            ]
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
        },
        {
            "issuer": "zEruWfhngbEc16jmpZBHSk4Tx872CHDWXeNsDJfL8yHo6",
            "created": "2021-06-24T21:36:03.409110Z",
            "proofPurpose": "PoP",
            "type": "JcsBase64Secp256k1Signature2021",
            "verificationMethod": "zEruWfhngbEc16jmpZBHSk4Tx872CHDWXeNsDJfL8yHo6#2021-06-24T21:36:03.409110Z#key-1",
            "signatureValue": "b5yQFpG7wSD87PzO1cElBWx-IXKhS8Ad-s-cE2vBpUsRjFOm-fDakZ6rs5M1CFh-LPkmdEdCpsPKPHGTNp5Ptg",
            "nonce": "097d3da2-95f8-47d3-8961-8fee21f7dd48"
        }
    ]
}
```

## Content Identifier
A declation is performed in a declaration file. A declaration file can contain many declarations. Each file is identified by it's ipfs content identifier (In this version: v1 raw sha256 base58). The v1 cid of the file above is.
```json
"B7NChg31x9cAYMU68RBZNG5opUkZJEVsxZfCSikWsGma3JM4KqMaZ3kyv67NNNf4pqv3bVPmJ2XLfKVTdehmd33gwqSt"
```
This content identifier will be used to reference the file in publications.

### Validation Rule DIAL00001:
Each dial file can be referenced using its content identifier.

## [type]
Type of the dial file. In this case a declaration.

### Validation Rule DIAL00002:
Each dial file has a predefined type held in the top level element named __type__. There is no unknown type.

## [declaration]
This top level element holds the list of declarations included in this DIAL file.

## [declaration][i]
Defines a single decclaration entry.

## [declaration][i][type]
Type of the declaration entry. In this case "Participant"

## [declaration][i][id]
The unique identifier of the declaration. If this is a participant declaration, [id] will be the unique identifier of the participant. This shall be unique as the DialChain does not allow for duplicate declarations. A new declaratation with the same [id] is considered a modification of the existing declaration. 

The id is always a public key in base58. The producer of this declaration mus innclude the corresponding verification method in the declaration file and a proof (signature) with the purpose "PoP", proving access to the corresponding private key.

The key used produce the id of this declaration can (but must not be) the one later used to produce assertions.

### Validation Rule DIAL00003
Each declaration ha a unique identifier. The submission of a new declaration carrying this same [id] is understood  by the network as a modification request. Validator will make sure modificator proves conntrol of the document as defined by the controller block of the latest version of this declaration.

If the producer of a declaration file can not prove possession of the corresponding private key, the declaration will be deemed invalide.

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
Specifies how to use the declared verification method. For example: __Ed25519VerificationKey2021__ describes how to read and consume the ed25519 public key included in this sub element.

## [declaration][i][verificationMethod][id]
Networkwide unique identifier used to reference this veriification method inside this declaration file and outside this declaration file.

### Valdidation Rule DIAL00006
This identifier of a verification method must allways be prefixed with the identifier of the enclosing declaration entity (participant, validator, ...). Dereferencing the verificcation method identifier (string before the first #) returns the identifier of the enclosing declaration entiry.

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
Collects proofs associated with declarations being submitted.

## [proof][i][document]
References the document subject of this proof. In this case the id of the containing DIAL file.

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