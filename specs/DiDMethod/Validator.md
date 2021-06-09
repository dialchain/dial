# Validator
A validator is a form of organization supported in the dial chain.

An organization is a participant that relies on the vote of it members (participants) for the production of declarations. Therefore, an organization assert with votes. 

The following json document displays the example of a simple declaration of organization (that can be used by a validator).
```json
{
    "id": "mMTM0MGRkNTItNzVlMy00YjY3LWFmMDEtZjE0MzhjZDY1YzMy",
    "type": "Declaration",
    "declaration": [
        {
            "type": "Organization",
            "id": "mZWYyYzE1MjItMjU2NS00MzAwLWExNGQtMGYwODNlMzMyMzk1",
            "created": "2021-06-09T03:42:26.705853Z",
            "controller": [
                "mZWYyYzE1MjItMjU2NS00MzAwLWExNGQtMGYwODNlMzMyMzk1"
            ],
            "assertionMethod": [
                {
                    "type": "Vote",
                    "id": "mZWYyYzE1MjItMjU2NS00MzAwLWExNGQtMGYwODNlMzMyMzk1#2021-06-09T03:42:26.705853Z#am-0",
                    "quorum": 2,
                    "member": [
                        {
                            "id": "mN2I3NTM2MTItMDhlNi00OWU5LWFkMTItMWJlMjRmYWI5Mjlj",
                            "shares": 1
                        },
                        {
                            "id": "mZjQwN2ZiMGMtMGQxMi00ZjQ3LWEwZDQtZmIwYzM0ODg4NzNm",
                            "shares": 1
                        },
                        {
                            "id": "mZmRlNzEwMDgtZjQxMC00OTMwLTkyMWEtY2ZmMTdkN2RjMGIx",
                            "shares": 1
                        }
                    ]
                }
            ],
            "service": [
                {
                    "type": "PublisherService",
                    "id": "mZWYyYzE1MjItMjU2NS00MzAwLWExNGQtMGYwODNlMzMyMzk1#2021-06-09T03:42:26.705853Z#PublisherService-0",
                    "serviceEndpoint": "https://node0.first-dial-validator.io/publisher",
                    "assertionMethod": "mZWYyYzE1MjItMjU2NS00MzAwLWExNGQtMGYwODNlMzMyMzk1#2021-06-09T03:42:26.705853Z#am-0"
                },
                {
                    "type": "PublisherService",
                    "id": "mZWYyYzE1MjItMjU2NS00MzAwLWExNGQtMGYwODNlMzMyMzk1#2021-06-09T03:42:26.705853Z#PublisherService-1",
                    "serviceEndpoint": "https://node1.first-dial-validator.io/publisher",
                    "assertionMethod": "mZWYyYzE1MjItMjU2NS00MzAwLWExNGQtMGYwODNlMzMyMzk1#2021-06-09T03:42:26.705853Z#am-0"
                },
                {
                    "type": "PublisherService",
                    "id": "mZWYyYzE1MjItMjU2NS00MzAwLWExNGQtMGYwODNlMzMyMzk1#2021-06-09T03:42:26.705853Z#PublisherService-2",
                    "serviceEndpoint": "https://node2.first-dial-validator.io/publisher",
                    "assertionMethod": "mZWYyYzE1MjItMjU2NS00MzAwLWExNGQtMGYwODNlMzMyMzk1#2021-06-09T03:42:26.705853Z#am-0"
                },
                {
                    "type": "LookupService",
                    "id": "mZWYyYzE1MjItMjU2NS00MzAwLWExNGQtMGYwODNlMzMyMzk1#2021-06-09T03:42:26.705853Z#LookupService-0",
                    "serviceEndpoint": "https://open.first-dial-validator.io/lookup",
                    "assertionMethod": "mZWYyYzE1MjItMjU2NS00MzAwLWExNGQtMGYwODNlMzMyMzk1#2021-06-09T03:42:26.705853Z#am-0"
                }
            ]
        }
    ],
    "proof": [
        {
            "document": "mMTM0MGRkNTItNzVlMy00YjY3LWFmMDEtZjE0MzhjZDY1YzMy",
            "issuer": "mN2I3NTM2MTItMDhlNi00OWU5LWFkMTItMWJlMjRmYWI5Mjlj",
            "created": "2021-06-09T03:42:26.754921Z",
            "type": "JcsBase64Ed25519Signature2021",
            "assertionMethod": [
                "mZWYyYzE1MjItMjU2NS00MzAwLWExNGQtMGYwODNlMzMyMzk1#2021-06-09T03:42:26.705853Z#am-0",
                "mN2I3NTM2MTItMDhlNi00OWU5LWFkMTItMWJlMjRmYWI5Mjlj#2021-06-09T03:42:26.317366Z#am-0"
            ],
            "signatureValue": "H5vF6u7jMeBm0QS5KPDjZt_hb-Gdh5X4oWMS-rV3BzzsIReBb_1Tr0Z8HyubiZ5xQV34t7Y7VuiK44uysjH7Bg",
            "nonce": "dfea6186-b710-46a5-8451-64185c9af1d8"
        },
        {
            "document": "mMTM0MGRkNTItNzVlMy00YjY3LWFmMDEtZjE0MzhjZDY1YzMy",
            "issuer": "mZjQwN2ZiMGMtMGQxMi00ZjQ3LWEwZDQtZmIwYzM0ODg4NzNm",
            "created": "2021-06-09T03:42:26.767556Z",
            "type": "JcsBase64Ed25519Signature2021",
            "assertionMethod": [
                "mZWYyYzE1MjItMjU2NS00MzAwLWExNGQtMGYwODNlMzMyMzk1#2021-06-09T03:42:26.705853Z#am-0",
                "mZjQwN2ZiMGMtMGQxMi00ZjQ3LWEwZDQtZmIwYzM0ODg4NzNm#2021-06-09T03:42:26.697626Z#am-0"
            ],
            "signatureValue": "jngrOrEwZSCx-lHKUfhwHipjnNal6vk2Wv0_fDmhGNRfxuBStERuutiS_vsXe24sdhVdxATsfJtxQt5ggSucBA",
            "nonce": "94f8f4c0-cf44-4b31-9245-ee50f3a2e693"
        },
        {
            "document": "mMTM0MGRkNTItNzVlMy00YjY3LWFmMDEtZjE0MzhjZDY1YzMy",
            "issuer": "mZmRlNzEwMDgtZjQxMC00OTMwLTkyMWEtY2ZmMTdkN2RjMGIx",
            "created": "2021-06-09T03:42:26.773016Z",
            "type": "JcsBase64Ed25519Signature2021",
            "assertionMethod": [
                "mZWYyYzE1MjItMjU2NS00MzAwLWExNGQtMGYwODNlMzMyMzk1#2021-06-09T03:42:26.705853Z#am-0",
                "mZmRlNzEwMDgtZjQxMC00OTMwLTkyMWEtY2ZmMTdkN2RjMGIx#2021-06-09T03:42:26.701615Z#am-0"
            ],
            "signatureValue": "VvUwUBUM9pl9vT_sLP6Gosnb4g4rWGvG3vrm8ON_5jzeSwI3H12pndaWqUXakjl1ITLt8C1WQUFwxBOFc0JJDQ",
            "nonce": "f1b0ede0-4015-4fad-9b1b-407d0e300010"
        }
    ]
}
```
## "declaration"."type":"Vote"
This is a reference to the data structure used in the assertionMethod subelement.

## "declaration"."assertionMethod"."id"
This is the identifiier of this assertion method. A declaration can contain many assertion methods.

## "declaration"."assertionMethod"."member"
Members entries reference other participants (simple or organization) that can vote to the extend of shares they hold.

## "declaration"."assertionMethod"."member"."shares"
States the number of shares assigned to this member.

### Validation Rule PTP0002
Shares value must be a natural number higher than zero.

## "declaration"."assertionMethod"."quorum"
The quorum defines the number of shares needed for a valid assertion.

### Validation Rule PTP0003
The quorum must be natural number higher zero and less or equals the total of shares listed in the member subelement.

## "declaration"."service"
A service record describes a service provided by an organization. In the case above, the validator exposes three PublisherServices and one LookupService.

## "proof"
As the example above displays, the declaration of an organization must provide a valid assertion of each member.