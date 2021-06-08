# Participant
A participant is the atomic unit of decision (Entity) in the DialChain. Each participant is represented by a deccentralized identifier.

# Simple Participant
A simple participant is one that can express a cryptographic signature. The following document shows the declaration of a simple participant record.
```json
{
    "declaration": {
        "id": "mMDUwZTgwYjktZDQ5Ni00NzcyLTg2YmItMGFmZjY1ODcxOTQw",
        "entries": [
            {
                "type": "Participant",
                "id": "mM2QzNGQ1YTMtM2U3MC00YjVmLWFlMjgtN2ExYjUxZjcwMzk0",
                "created": "2021-05-12T10:12:00Z",
                "controller": [
                    "mM2QzNGQ1YTMtM2U3MC00YjVmLWFlMjgtN2ExYjUxZjcwMzk0"
                ],
                "verificationMethod": [
                    {
                        "type": "Ed25519VerificationKey2021",
                        "id": "mM2QzNGQ1YTMtM2U3MC00YjVmLWFlMjgtN2ExYjUxZjcwMzk0#2021-05-12T10:12:00Z#key-0",
                        "publicKeyMultibase": "z5xHTdS4CvCu5HAa63AGxhWQ5X4fBGtH8z9pNcdaSnTrp"
                    }
                ],
                "assertionMethod": [
                    {
                        "type": "Signature",
                        "id": "mM2QzNGQ1YTMtM2U3MC00YjVmLWFlMjgtN2ExYjUxZjcwMzk0#2021-05-12T10:12:00Z#am-0",
                        "verificationMethod": "mM2QzNGQ1YTMtM2U3MC00YjVmLWFlMjgtN2ExYjUxZjcwMzk0#2021-05-12T10:12:00Z#key-0"
                    }
                ]
            }
        ]
    },
    "proof": [
        {
            "declaration": "mMDUwZTgwYjktZDQ5Ni00NzcyLTg2YmItMGFmZjY1ODcxOTQw",
            "issuer": "mM2QzNGQ1YTMtM2U3MC00YjVmLWFlMjgtN2ExYjUxZjcwMzk0",
            "created": "2021-05-12T10:12:00Z",
            "type": "JcsBase64Ed25519Signature2021",
            "assertionMethod": [
                "mM2QzNGQ1YTMtM2U3MC00YjVmLWFlMjgtN2ExYjUxZjcwMzk0#2021-05-12T10:12:00Z#am-0"
            ],
            "signatureValue": "_Kp5fQJRHQCtGG6R7vLteUXyUNHNF3eAXc2lcqY7dkpe-9WCcwSVrKRcK83DYrSTfIzCCDaQ8U3dJNvIp3swAw",
            "nonce": "2da268ec-aa0a-41f7-8923-ede740e33a24"
        }
    ]
}
```
## "declaration"."entries"."type": "Participant"
Specifies the type of object to included in this declaration.

## "declaration"."entries"."id"
This is the unique identifier of the participant. This shall be unique as the DialChain does not allow for duplicate declarations. A new declaratation with the same id is considered a modification of the existing declaration.

### Validation Rule PTP0001
A "declaration"."entries"."id" is unique. The submission of a new declaration carrying this same id is understood  by the network as a modification request.

## "declaration"."entries"."controller"
Participant that is authorized to make changes to this declaration.

## "declaration"."entries"."verificationMethod"
Declaration of public keys used to verify proofs produced by this participant. Note that to keep schema simple and reduce ambiguity, we do not allow the controller property inside a verification relationship (like verificationMethod, assertionMethod). The global controller of the declaration is the only one allowed to modify the declaration.

## "declaration"."entries"."assertionMethod"
Reference on verificationMethods used to validate assertions produced by this participant.

## "declaration"."entries"."assertionMethod"."type":"Signature"
Defines the data format of the assertionMethod. In this case a simple signature.

## "proof"
Collects proofs associated with declarations being submitted. For a simple participant declaration, the proof allows the validation of the declared assertionMethod, thereby also allowing the validation of the referenced verificationMethod (or public key).
