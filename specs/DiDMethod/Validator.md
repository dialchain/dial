# Validator
A validator is a form of organization supported in the dial chain.

An organization is a participant that relies on the vote of it members (participants) for the production of declarations. Therefore, an organization assert with votes. 

The following json document displays the example of a simple declaration of organization (that can be used by a validator).
```json
{
    "declaration": {
        "id": "mNDFmNTkyZDgtMTZmNC00MzVjLWJkZWYtNjViNTU4YmZmYzZk",
        "entries": [
            {
                "type": "Organization",
                "id": "mZGRmNjc3NWEtZmMzMy00MmMzLWE0ZTctZGNjN2E3ODQ3NWNh",
                "created": "2021-06-08T14:15:42.876447Z",
                "controller": [
                    "mZGRmNjc3NWEtZmMzMy00MmMzLWE0ZTctZGNjN2E3ODQ3NWNh"
                ],
                "assertionMethod": [
                    {
                        "type": "Vote",
                        "id": "mZGRmNjc3NWEtZmMzMy00MmMzLWE0ZTctZGNjN2E3ODQ3NWNh#2021-06-08T14:15:42.876447Z#am-0",
                        "quorum": 2,
                        "member": [
                            {
                                "id": "mZmNiMmY5NzMtNWVlNC00Y2JkLWI4NTMtMmY4YmU5ZDA0OTFj",
                                "shares": 1
                            },
                            {
                                "id": "mMjQzNTNkMzQtOTNhMS00ZDFhLTgxMDMtOTdhZjA3MjQ1MjY4",
                                "shares": 1
                            },
                            {
                                "id": "mZWM0YjVkYTQtMmFhOC00ZmU2LThmYWMtYWVhZTA4YTU3MDZl",
                                "shares": 1
                            }
                        ]
                    }
                ],
                "service": [
                    {
                        "type": "PublisherService",
                        "id": "mZGRmNjc3NWEtZmMzMy00MmMzLWE0ZTctZGNjN2E3ODQ3NWNh#2021-06-08T14:15:42.876447Z#PublisherService-0",
                        "serviceEndpoint": "https://node0.first-dial-validator.io/publisher",
                        "assertionMethod": "mZGRmNjc3NWEtZmMzMy00MmMzLWE0ZTctZGNjN2E3ODQ3NWNh#2021-06-08T14:15:42.876447Z#am-0"
                    },
                    {
                        "type": "PublisherService",
                        "id": "mZGRmNjc3NWEtZmMzMy00MmMzLWE0ZTctZGNjN2E3ODQ3NWNh#2021-06-08T14:15:42.876447Z#PublisherService-1",
                        "serviceEndpoint": "https://node1.first-dial-validator.io/publisher",
                        "assertionMethod": "mZGRmNjc3NWEtZmMzMy00MmMzLWE0ZTctZGNjN2E3ODQ3NWNh#2021-06-08T14:15:42.876447Z#am-0"
                    },
                    {
                        "type": "PublisherService",
                        "id": "mZGRmNjc3NWEtZmMzMy00MmMzLWE0ZTctZGNjN2E3ODQ3NWNh#2021-06-08T14:15:42.876447Z#PublisherService-2",
                        "serviceEndpoint": "https://node2.first-dial-validator.io/publisher",
                        "assertionMethod": "mZGRmNjc3NWEtZmMzMy00MmMzLWE0ZTctZGNjN2E3ODQ3NWNh#2021-06-08T14:15:42.876447Z#am-0"
                    },
                    {
                        "type": "LookupService",
                        "id": "mZGRmNjc3NWEtZmMzMy00MmMzLWE0ZTctZGNjN2E3ODQ3NWNh#2021-06-08T14:15:42.876447Z#LookupService-0",
                        "serviceEndpoint": "https://open.first-dial-validator.io/lookup",
                        "assertionMethod": "mZGRmNjc3NWEtZmMzMy00MmMzLWE0ZTctZGNjN2E3ODQ3NWNh#2021-06-08T14:15:42.876447Z#am-0"
                    }
                ]
            }
        ]
    },
    "proof": [
        {
            "declaration": "mNDFmNTkyZDgtMTZmNC00MzVjLWJkZWYtNjViNTU4YmZmYzZk",
            "issuer": "mZmNiMmY5NzMtNWVlNC00Y2JkLWI4NTMtMmY4YmU5ZDA0OTFj",
            "created": "2021-06-08T14:15:42.896070Z",
            "type": "JcsBase64Ed25519Signature2021",
            "assertionMethod": [
                "mZGRmNjc3NWEtZmMzMy00MmMzLWE0ZTctZGNjN2E3ODQ3NWNh#2021-06-08T14:15:42.876447Z#am-0",
                "mZmNiMmY5NzMtNWVlNC00Y2JkLWI4NTMtMmY4YmU5ZDA0OTFj#2021-06-08T14:15:42.466223Z#am-0"
            ],
            "signatureValue": "VU9hpUWH_LV4_-nvAzD2Lp43XAIx6Bhq1Rr9UZgKbWFjNO4jyMPAMk2ogfMqJ8T9ut5c6ZFEi06baZHFvB2yAA",
            "nonce": "91a36c6a-2833-41d3-876e-de3ad70ee5ee"
        },
        {
            "declaration": "mNDFmNTkyZDgtMTZmNC00MzVjLWJkZWYtNjViNTU4YmZmYzZk",
            "issuer": "mMjQzNTNkMzQtOTNhMS00ZDFhLTgxMDMtOTdhZjA3MjQ1MjY4",
            "created": "2021-06-08T14:15:42.908260Z",
            "type": "JcsBase64Ed25519Signature2021",
            "assertionMethod": [
                "mZGRmNjc3NWEtZmMzMy00MmMzLWE0ZTctZGNjN2E3ODQ3NWNh#2021-06-08T14:15:42.876447Z#am-0",
                "mMjQzNTNkMzQtOTNhMS00ZDFhLTgxMDMtOTdhZjA3MjQ1MjY4#2021-06-08T14:15:42.868761Z#am-0"
            ],
            "signatureValue": "LJRZ_B14OcQlnuHawdN9WMhhsj0hAfiTynTpF5ChxnJzvjv-_uLeaekmsuXv-0VW3QhZxxwhZSTDfrslPkepCg",
            "nonce": "1dd3a855-b534-4f2a-acc2-8fde98bd029c"
        },
        {
            "declaration": "mNDFmNTkyZDgtMTZmNC00MzVjLWJkZWYtNjViNTU4YmZmYzZk",
            "issuer": "mZWM0YjVkYTQtMmFhOC00ZmU2LThmYWMtYWVhZTA4YTU3MDZl",
            "created": "2021-06-08T14:15:42.913471Z",
            "type": "JcsBase64Ed25519Signature2021",
            "assertionMethod": [
                "mZGRmNjc3NWEtZmMzMy00MmMzLWE0ZTctZGNjN2E3ODQ3NWNh#2021-06-08T14:15:42.876447Z#am-0",
                "mZWM0YjVkYTQtMmFhOC00ZmU2LThmYWMtYWVhZTA4YTU3MDZl#2021-06-08T14:15:42.872480Z#am-0"
            ],
            "signatureValue": "tJBTYbJIxuWdO2EqMmJVim8NqcjLM4NbbsluiCNCkiXvrVjqustjpteXGKS8i7sXMyIC81RphvrU67yRn0OJAQ",
            "nonce": "80f4ed3a-6cc8-4ab7-a8d1-8206d4247e4b"
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

## "declaration"."entries"."service"
A service record describes a service provided by an organization. In the case above, the validator exposes three PublisherServices and one LookupService.

## "proof"
As the example above displays, the declaration of an organization must provide a valid assertion of each member.