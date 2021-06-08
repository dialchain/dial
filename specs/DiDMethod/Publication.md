# Publication
A publication is the act of a validator adding a file to a DialChain. For this purpose, a validator  must expose a publisher service.

## Initial Self Publication of a Validator
At the bootstraping of the DialChain, each validator will publish their own genesis reccord to the chain. This consists of:

- The declaration record of all 3 nodes
- The declaration record of the validator

We will therefore be dealing with four files per validators. These files will be exposed on a bootstrap server, exposed in the project source repository.

```json
{
    "declaration": {
        "id": "mMTYxODdmN2ItODBlOC00YTI2LWE4NGEtZjg4MTRmMTI3ZjQ2",
        "entries": [
            {
                "type": "Organization",
                "id": "mYTlkMWNiZWItZjY4Mi00MmQyLWFjNjgtOGY2OTU2MGQ5ZmEy",
                "created": "2021-06-08T12:38:16.767996Z",
                "controller": [
                    "mYTlkMWNiZWItZjY4Mi00MmQyLWFjNjgtOGY2OTU2MGQ5ZmEy"
                ],
                "assertionMethod": [
                    {
                        "type": "Vote",
                        "id": "mYTlkMWNiZWItZjY4Mi00MmQyLWFjNjgtOGY2OTU2MGQ5ZmEy#2021-06-08T12:38:16.767996Z#am-0",
                        "quorum": 2,
                        "member": [
                            {
                                "id": "mZTgyMThlYWUtOTY2NC00ZGQ0LWE4YzgtODE5YmYxYzUyMjVm",
                                "shares": 1
                            },
                            {
                                "id": "mZDcyYzllOWEtMzg1Yy00N2NkLWFiYzYtNTE3ZDRlZWVlZTRm",
                                "shares": 1
                            },
                            {
                                "id": "mNjBkMjg1OTItNWUzNC00ZjU2LThhODgtMGViYWM3YTRmYjBl",
                                "shares": 1
                            }
                        ]
                    }
                ]
            }
        ]
    },
    "proof": [
        {
            "declaration": "mMTYxODdmN2ItODBlOC00YTI2LWE4NGEtZjg4MTRmMTI3ZjQ2",
            "issuer": "mZTgyMThlYWUtOTY2NC00ZGQ0LWE4YzgtODE5YmYxYzUyMjVm",
            "created": "2021-06-08T12:38:16.783095Z",
            "type": "JcsBase64Ed25519Signature2021",
            "assertionMethod": [
                "mYTlkMWNiZWItZjY4Mi00MmQyLWFjNjgtOGY2OTU2MGQ5ZmEy#2021-06-08T12:38:16.767996Z#am-0",
                "mZTgyMThlYWUtOTY2NC00ZGQ0LWE4YzgtODE5YmYxYzUyMjVm#2021-06-08T12:38:16.400195Z#am-0"
            ],
            "signatureValue": "RftNhIKe1NGOzAnqvWoqEL0wOibQ5v8XEkHKRsEZ3w1km6E1xAKb_Te4HNd8MgHuYX52IHtZtDfARcAHxSVoDA",
            "nonce": "f116c829-5297-4fd1-ae39-666ba1693dd0"
        },
        {
            "declaration": "mMTYxODdmN2ItODBlOC00YTI2LWE4NGEtZjg4MTRmMTI3ZjQ2",
            "issuer": "mZDcyYzllOWEtMzg1Yy00N2NkLWFiYzYtNTE3ZDRlZWVlZTRm",
            "created": "2021-06-08T12:38:16.791482Z",
            "type": "JcsBase64Ed25519Signature2021",
            "assertionMethod": [
                "mYTlkMWNiZWItZjY4Mi00MmQyLWFjNjgtOGY2OTU2MGQ5ZmEy#2021-06-08T12:38:16.767996Z#am-0",
                "mZDcyYzllOWEtMzg1Yy00N2NkLWFiYzYtNTE3ZDRlZWVlZTRm#2021-06-08T12:38:16.760267Z#am-0"
            ],
            "signatureValue": "Lq91BPN9TBfhDvly2_-UPc2gCP2A6Qs6vnqtMAf6wnjahWTFzFEJguu10EIaASq4t_F5p2G0mZtJ3piRqZzUBQ",
            "nonce": "a3820ad9-d9c4-4b8b-ae5d-ee619ac1fd6f"
        },
        {
            "declaration": "mMTYxODdmN2ItODBlOC00YTI2LWE4NGEtZjg4MTRmMTI3ZjQ2",
            "issuer": "mNjBkMjg1OTItNWUzNC00ZjU2LThhODgtMGViYWM3YTRmYjBl",
            "created": "2021-06-08T12:38:16.793984Z",
            "type": "JcsBase64Ed25519Signature2021",
            "assertionMethod": [
                "mYTlkMWNiZWItZjY4Mi00MmQyLWFjNjgtOGY2OTU2MGQ5ZmEy#2021-06-08T12:38:16.767996Z#am-0",
                "mNjBkMjg1OTItNWUzNC00ZjU2LThhODgtMGViYWM3YTRmYjBl#2021-06-08T12:38:16.764800Z#am-0"
            ],
            "signatureValue": "5oh5HC1LiTchEP3ugbcS8CXstCUkTT55dypbnmonUjQmrHwZk6BmoA70jqhqpipGBQYtux-1whVJTpFtgcp_Cw",
            "nonce": "c16afd96-939d-4b50-8fe8-a9b5477fe79f"
        }
    ]
}
```
## "declaration"."entries"."type":"Vote"
This is a reference to the data structure used in the assertionMethod subelement.

## "declaration"."entries"."assertionMethod"."id"
This is the identifiier of this assertion method. A declaration can contain many assertion methods.

## "declaration"."entries"."assertionMethod"."member"
Members entries reference other participants (simple or organization) that can vote to the extend of shares they hold.

## "declaration"."entries"."assertionMethod"."member"."shares"
States the number of shares assigned to this member.

### Validation Rule PTP0002
Shares value must be a natural number higher than zero.

## "declaration"."entries"."assertionMethod"."quorum"
The quorum defines the number of shares needed for a valid assertion.

### Validation Rule PTP0003
The quorum must be natural number higher zero and less or equals the total of shares listed in the member subelement.

## "proof"
As the example above displays, the declaration of an organization must provide a valid assertion of each member.