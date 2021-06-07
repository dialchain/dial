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
    "declaration": {
        "id": "declaration-uuid-multibase",
        "entries": [
            {
                "type": "ref",
                "cid": "cid-value-0"
            },
            {
                "type": "declaration-type",
                "string-field": "value",
                "list-field": [],
                "object-field": {}
            }
        ]
    },
    "proof": [
        {
            "declaration": "declaration-uuid-multibase",
            "issuer": "issuer-id-multibase",
            "created": "2020-11-20T07:30:00Z",
            "type": "JcsBase64Ed25519Signature2020",
            "assertionMethod": ["issuer-id-multibase#timestamp#am-0"],
            "signatureValue": "fWcozEsDGwJO2WeYb9DH_yjcinLGhd-pTXBADiaFE2C-A6iSKAYbjD8YCu7DP3SAZFAFIHBzumetTKVY0bBCAA",
            "nonce": "b40a4e02-af7a-40dd-b4a7-b89e897d10b7"
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
            "declaration": "declaration-uuid-multibase",
            "issuer": "issuer-id-multibase",
            "created": "2020-11-20T07:30:00Z",
            "type": "JcsBase64Ed25519Signature2020",
            "assertionMethod": ["issuer-id-multibase#timestamp#am-0"],
            "signatureValue": "fWcozEsDGwJO2WeYb9DH_yjcinLGhd-pTXBADiaFE2C-A6iSKAYbjD8YCu7DP3SAZFAFIHBzumetTKVY0bBCAA",
            "nonce": "b40a4e02-af7a-40dd-b4a7-b89e897d10b7"
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
    "declaration": {
        "id": "declaration-uuid",
        "entries": [{"...":"..."}]
    },
    "proof": [{"...":"..."}],
    "twindow": {
        "start": "2020-11-12T00:00:00Z",
        "end": "2020-11-12T23:59:59Z",
        "a_hash": "2ZSF5H6MLUKFLDMBDCX55JQ7MSEITFPXPZJ734OWO2SFDDEDW3U7H4YDUK6SXXGHRT4LZHP66ONNHGMZ7RUXJTBUZRJLQESSF4GY5PY"
    },
    "publication": [
        {
            "issuer": "did:sw:gs:bmdpernypoeoxcc4mj54sycfsl5yg6",
            "created": "2020-11-12T09:12:00Z",
            "type": "JcsBase64Ed25519Signature2020",
            "assertionMethod": ["did:sw:sp:bmcbmhkfxb3ezudwhvceraeeyp4g24#am-0", "did:sw:pt:bmdpernypoeoxcc4mj54sycfsl5yg6#am-3"],
            "signatureValue": "aDby05Axtn1ECKt3xgjjgFP8iL8SdlarR1ac6pMeMLA6wxpSVO017X7A9LBKez5OzDKQDsuitMFaRhPLP5L9Dg",
            "nonce": "43bdb2b7-a6c2-40c5-a41c-67d6b8b6c718"
        },
        {
            "issuer": "did:sw:sp:bmbjqebz6fhhjqfkdthyiubynrwk5g",
            "created": "2020-11-12T09:14:10Z",
            "type": "JcsBase64Ed25519Signature2020",
            "assertionMethod": ["did:sw:sp:bmcbmhkfxb3ezudwhvceraeeyp4g24#am-0", "did:sw:pt:bmbjqebz6fhhjqfkdthyiubynrwk5g#am-3"],
            "signatureValue": "Lm8MA4X7VGerun1BOldu_JPBpsUgyEzsZ3-N07ENNfm6tTFSiXkoV09YITurfPQIuAkNDk4lxHTdCXk-lQfUAA",
            "nonce": "bea26c23-b90e-44bb-843e-993b35cbf056"
        }

    ]
}
```

The publication entries are allways attached. The signature data is everything else in the file except the __"publication"__ entry itself. Single publication entries can be produced paralelly.

## "publication"."assertionMethod", "proof"."assertionMethod"
In the default configuration, a publication will be signed by two of three members of the validator organization, reducing the risk of verification mistakes and the risk of spam publications due to the lost a validator node's private key.

- The first entry in the list of assertionMethods references the signature rule defined in the DiD declaration of the validator organization.
- The second entry references the assertionMethods defined in the DiD document of the validator node (member).

In the following expression:
```json
{
    "assertionMethod": ["did:sw:sp:bmcbmhkfxb3ezudwhvceraeeyp4g24#am-0", "did:sw:pt:bmbjqebz6fhhjqfkdthyiubynrwk5g#am-3"]
}
```

- __did:sw:sp:bmcbmhkfxb3ezudwhvceraeeyp4g24#am-0__ is the asertionMethod as defined in the organization declaration file.
- __did:sw:pt:bmbjqebz6fhhjqfkdthyiubynrwk5g#am-3__ is the assertionMethod as defined in the node declaration file.

### Validation Rule DECL0001
The last element in the list of assertionMethod must allways be the assertion method of a simple participant.

### Validation Rule DECL0002
The list of assertionMethod must form a directed delegation chain (means can not be circcular).
  
### Validation Rule DECL0003
Event though there is no limit on the dept of the assertion chain, the deeper the delegation chain, the most complicated is the validation. Therefore the more expensive will be the insertion into the chain.