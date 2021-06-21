# Validator
A validator is a form of organization supported in the dial chain.

An organization is a participant that relies on the vote of it members (participants) for the production of declarations. Therefore, an organization assert with votes. 

The following json document displays the example of a simple declaration of organization (that can be used by a validator).
```json
{
    "id": "mZGE0N2QwZjQtMmZjZi00ZmQ4LThlMzAtYTIzMDVhNmFlNjQw",
    "type": "Declaration",
    "declaration": [
        {
            "type": "Organization",
            "id": "mNWYwMWU5ZTUtMjBlNS00OGE5LWE3ZDYtOWM1NjI2ZDBiYjhj",
            "created": "2021-06-19T19:32:06.145319Z",
            "controller": [
                "mNWYwMWU5ZTUtMjBlNS00OGE5LWE3ZDYtOWM1NjI2ZDBiYjhj"
            ],
            "account": [
                {
                    "network": "org.bitcoin.production",
                    "address": "34twR8mKvijuNg2eHXMhPS7GoKH34YuP8k",
                    "control": {
                        "quorum": 2,
                        "verificationMethod": [
                            "mMGExY2RjMDAtNjA1MC00OGJiLTlmMzEtMTIxNDVhMjJlMmM3#2021-06-19T19:32:05.602146Z#key-1",
                            "mYjJiZGI1MGQtNjJhOC00YWFhLWI2M2YtZGMwMmFhYzZlMjI2#2021-06-19T19:32:06.124560Z#key-1",
                            "mNDcyOTYzMjUtYjczZi00ZWE3LWIwNjAtNjI4NjA2YTMxMDlk#2021-06-19T19:32:06.133235Z#key-1"
                        ]
                    }
                }
            ],
            "assertionMethod": [
                {
                    "type": "Vote",
                    "id": "mNWYwMWU5ZTUtMjBlNS00OGE5LWE3ZDYtOWM1NjI2ZDBiYjhj#2021-06-19T19:32:06.145319Z#am-0",
                    "quorum": 2,
                    "member": [
                        {
                            "id": "mMGExY2RjMDAtNjA1MC00OGJiLTlmMzEtMTIxNDVhMjJlMmM3",
                            "shares": 1
                        },
                        {
                            "id": "mYjJiZGI1MGQtNjJhOC00YWFhLWI2M2YtZGMwMmFhYzZlMjI2",
                            "shares": 1
                        },
                        {
                            "id": "mNDcyOTYzMjUtYjczZi00ZWE3LWIwNjAtNjI4NjA2YTMxMDlk",
                            "shares": 1
                        }
                    ]
                }
            ],
            "service": [
                {
                    "type": "PublisherService",
                    "id": "mNWYwMWU5ZTUtMjBlNS00OGE5LWE3ZDYtOWM1NjI2ZDBiYjhj#2021-06-19T19:32:06.145319Z#PublisherService-0",
                    "serviceEndpoint": "https://node0.first-dial-validator.io/publisher",
                    "assertionMethod": "mNWYwMWU5ZTUtMjBlNS00OGE5LWE3ZDYtOWM1NjI2ZDBiYjhj#2021-06-19T19:32:06.145319Z#am-0"
                },
                {
                    "type": "PublisherService",
                    "id": "mNWYwMWU5ZTUtMjBlNS00OGE5LWE3ZDYtOWM1NjI2ZDBiYjhj#2021-06-19T19:32:06.145319Z#PublisherService-1",
                    "serviceEndpoint": "https://node1.first-dial-validator.io/publisher",
                    "assertionMethod": "mNWYwMWU5ZTUtMjBlNS00OGE5LWE3ZDYtOWM1NjI2ZDBiYjhj#2021-06-19T19:32:06.145319Z#am-0"
                },
                {
                    "type": "PublisherService",
                    "id": "mNWYwMWU5ZTUtMjBlNS00OGE5LWE3ZDYtOWM1NjI2ZDBiYjhj#2021-06-19T19:32:06.145319Z#PublisherService-2",
                    "serviceEndpoint": "https://node2.first-dial-validator.io/publisher",
                    "assertionMethod": "mNWYwMWU5ZTUtMjBlNS00OGE5LWE3ZDYtOWM1NjI2ZDBiYjhj#2021-06-19T19:32:06.145319Z#am-0"
                },
                {
                    "type": "LookupService",
                    "id": "mNWYwMWU5ZTUtMjBlNS00OGE5LWE3ZDYtOWM1NjI2ZDBiYjhj#2021-06-19T19:32:06.145319Z#LookupService-0",
                    "serviceEndpoint": "https://open.first-dial-validator.io/lookup",
                    "assertionMethod": "mNWYwMWU5ZTUtMjBlNS00OGE5LWE3ZDYtOWM1NjI2ZDBiYjhj#2021-06-19T19:32:06.145319Z#am-0"
                }
            ]
        }
    ],
    "proof": [
        {
            "document": "mZGE0N2QwZjQtMmZjZi00ZmQ4LThlMzAtYTIzMDVhNmFlNjQw",
            "issuer": "mMGExY2RjMDAtNjA1MC00OGJiLTlmMzEtMTIxNDVhMjJlMmM3",
            "created": "2021-06-19T19:32:14.815489Z",
            "type": "JcsBase64Ed25519Signature2021",
            "assertionMethod": [
                "mNWYwMWU5ZTUtMjBlNS00OGE5LWE3ZDYtOWM1NjI2ZDBiYjhj#2021-06-19T19:32:06.145319Z#am-0",
                "mMGExY2RjMDAtNjA1MC00OGJiLTlmMzEtMTIxNDVhMjJlMmM3#2021-06-19T19:32:05.602146Z#am-0",
                "mMGExY2RjMDAtNjA1MC00OGJiLTlmMzEtMTIxNDVhMjJlMmM3#2021-06-19T19:32:05.602146Z#key-0"
            ],
            "signatureValue": "yokTqDatzGLBkDBHIlepNxdtldALQep-XZvMPqaM86QrAaU5oTEAJSXNPeQZpQvR4M50uXsyTUr4LpyKZJcPAw",
            "nonce": "fb03d487-f415-4daf-b693-f4aebecf69be"
        },
        {
            "document": "mZGE0N2QwZjQtMmZjZi00ZmQ4LThlMzAtYTIzMDVhNmFlNjQw",
            "issuer": "mYjJiZGI1MGQtNjJhOC00YWFhLWI2M2YtZGMwMmFhYzZlMjI2",
            "created": "2021-06-19T19:32:14.825683Z",
            "type": "JcsBase64Ed25519Signature2021",
            "assertionMethod": [
                "mNWYwMWU5ZTUtMjBlNS00OGE5LWE3ZDYtOWM1NjI2ZDBiYjhj#2021-06-19T19:32:06.145319Z#am-0",
                "mYjJiZGI1MGQtNjJhOC00YWFhLWI2M2YtZGMwMmFhYzZlMjI2#2021-06-19T19:32:06.124560Z#am-0",
                "mYjJiZGI1MGQtNjJhOC00YWFhLWI2M2YtZGMwMmFhYzZlMjI2#2021-06-19T19:32:06.124560Z#key-0"
            ],
            "signatureValue": "ptYLE8oW89qDBinaukO0caz-hUs-cZKqe9Os2XOVjQvEJupUZtJyMA3kQ-dEHBV1axGV8D3MkI1ZeL_JCOhqBQ",
            "nonce": "d1272d23-fa77-4788-a244-b0046dd7a1d7"
        },
        {
            "document": "mZGE0N2QwZjQtMmZjZi00ZmQ4LThlMzAtYTIzMDVhNmFlNjQw",
            "issuer": "mNDcyOTYzMjUtYjczZi00ZWE3LWIwNjAtNjI4NjA2YTMxMDlk",
            "created": "2021-06-19T19:32:14.831698Z",
            "type": "JcsBase64Ed25519Signature2021",
            "assertionMethod": [
                "mNWYwMWU5ZTUtMjBlNS00OGE5LWE3ZDYtOWM1NjI2ZDBiYjhj#2021-06-19T19:32:06.145319Z#am-0",
                "mNDcyOTYzMjUtYjczZi00ZWE3LWIwNjAtNjI4NjA2YTMxMDlk#2021-06-19T19:32:06.133235Z#am-0",
                "mNDcyOTYzMjUtYjczZi00ZWE3LWIwNjAtNjI4NjA2YTMxMDlk#2021-06-19T19:32:06.133235Z#key-0"
            ],
            "signatureValue": "k6-3HpuAf9pm_6WX2NWKWy7INlgVttnbXL9oIgLe2ggR-jeps3e4Oxws2hVaQ6xtczba87nexKh_RMvPQvDFCw",
            "nonce": "2e6f882b-f57d-454e-8da8-18e4c58ad2ce"
        }
    ]
}
```
## General Items
The structure of this document is very similar to the one defined in [Participant](./Participant.md). Therefore similar elements will not be explained here.

## [declaration][i][type]
The type of this declaration.

## [declaration][i][account][address]
Despite the case of the single particcipant, this organization bitcoin address is a multisig acount, that requires 2  of 3 signatures to spend.

## [declaration][i][account][control]
References the verificcation methods to be used by members to spend from this account. Corresponding members public keys are loccated in the declaration files that can be found derefencing the verification method ids.

## [declaration][i][type]
This is a reference to the data structure used in the assertionMethod subelement. In this case a Vote.

## [declaration][i][assertionMethod][id]
This is the identifiier of this assertion method. A declaration can contain many assertion methods.

## [declaration][i][assertionMethod][member]
Members entries reference other participants (simple or organization) that can vote to the extend of shares they hold.

## [declaration][i][assertionMethod][member][shares]
States the number of shares assigned to this member.

### Validation Rule DIAL00101
Shares value must be a natural number higher than zero.

## [declaration][i][assertionMethod][quorum]
The quorum defines the number of shares needed for a valid assertion.

### Validation Rule DIAL00102
The quorum must be natural number higher zero and less or equals the total of shares listed in the member subelement.

## [declaration][i][service]
A service record describes a service provided by an organization. In the case above, the validator exposes three PublisherServices and one LookupService.

## [proof]
As the example above displays, the declaration of an organization must provide a valid assertion of each member.