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

# Organization
An organization is a participant that relies on the vote of it members (participants) for the production of declarations. Therefore, an organization assert with votes. 

The following json document displays the example of a simple declaration of organization.
```json
{
    "declarations": {
        "id": "declaration-uuid",
        "entries": [
            {
                "type": "Organization",
                "id": "did:sw:pt:bmcbmhkfxb3ezudwhvceraeeyp4g24",
                "created": "2020-11-20T07:30:00Z",
                "controller": ["did:sw:pt:bmcbmhkfxb3ezudwhvceraeeyp4g24"],
                "assertionMethod": [
                    {
                        "type": "Vote",
                        "id":"did:sw:pt:bmcbmhkfxb3ezudwhvceraeeyp4g24#am-0",
                        "quorum": 2,
                        "member":[
                            {
                                "id":"did:sw:pt:bmcwom2kkw7wdkgqojeodrdqsxvume",
                                "shares":1,
                            },
                            {
                                "id":"did:sw:pt:bmbjqebz6fhhjqfkdthyiubynrwk5g",
                                "shares":1,
                            },
                            {
                                "id":"did:sw:og:bmdpernypoeoxcc4mj54sycfsl5yg6",
                                "shares":1,
                            }
                        ]
                    }
                ]
            }
        ]
    },
    "proof": [
        {
            "id": "declaration-uuid",
            "issuer": "did:sw:pt:bmcwom2kkw7wdkgqojeodrdqsxvume",
            "created": "2020-11-20T07:30:00Z",
            "type": "JcsBase64Ed25519Signature2020",
            "assertionMethod": "did:sw:pt:bmcwom2kkw7wdkgqojeodrdqsxvume#am-0",
            "signatureValue": "fWcozEsDGwJO2WeYb9DH_yjcinLGhd-pTXBADiaFE2C-A6iSKAYbjD8YCu7DP3SAZFAFIHBzumetTKVY0bBCAA",
            "nonce": "b40a4e02-af7a-40dd-b4a7-b89e897d10b7"
        },
        {
            "id": "declaration-uuid",
            "issuer": "did:sw:sp:bmbjqebz6fhhjqfkdthyiubynrwk5g",
            "created": "2020-11-20T07:30:10Z",
            "type": "JcsBase64Ed25519Signature2020",
            "verificationMethod": "did:sw:sp:bmbjqebz6fhhjqfkdthyiubynrwk5g#am-2",
            "signatureValue": "2jH7RJ6Ut2rhj3xlda4Y2Z3Wu8fos0nMHGhLVnsZksUCDsIKRxz2_1tjUhDyWH9woJSiPicg7l3_PvpOH8jYCQ",
            "nonce": "fbb51d69-b106-40a5-9412-5ae2a0aa1408"
        },
        {
            "id": "declaration-uuid",
            "issuer": "did:sw:gs:bmdpernypoeoxcc4mj54sycfsl5yg6",
            "created": "2020-11-12T09:12:00Z",
            "type": "JcsBase64Ed25519Signature2020",
            "verificationMethod": "did:sw:gs:bmdpernypoeoxcc4mj54sycfsl5yg6#am-0",
            "signatureValue": "DRdy5l6HlDVJUblISqN708zv40dh4pzjKeZmNiIXCKyAsDllQBr-Svvj6YP3f35jn_VP2ntkzaKReqsfSUX2AQ",
            "nonce": "aad7e781-d87f-4404-a6c1-b2a0a9917af7"
        }
    ]
}
```
## "declaration"."entries"."type":"Vote"
This is a reference to the data structure used in the assertionMethod subelement.

## "declaration"."entries"."assertionMethod"."id"
This is the identifiier of this assertion method. A DiD can contain many assertion methods.

## "declaration"."entries"."assertionMethod"."member"
Members entries reference other participants (simple or organization) that can vote to the extend of shares they hold.

## "declaration"."entries"."assertionMethod"."member"."shares"
State the number of shares assigned to this member.

### Validation Rule PTP0002
Shares value must be a natural number higher than zero.

## "declaration"."entries"."assertionMethod"."quorum"
The quorum defines the number of shares needed for a valid assertion.

### Validation Rule PTP0003
The quorum must be natural number higher zero and less or equals the total of shares listed in the member subelement.

## "proof"
As the example above displays, the declaration of an organization must provide a valid assertion of each member.