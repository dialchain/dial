# Participant
A participant is the atomic unit of decision (Entity) in the DialChain. Each participant is represented by a deccentralized identifier.

# Simple Participant
A simple participant is one that can express a cryptographic signature. The following document shows the declaration of a simple participant record.
```json
{
    "id": "mYzRiZGIzMTItNmUxOC00ZDE1LThjNmYtMDgxYWE4YTY5Yzk1",
    "type": "Declaration",
    "declaration": [
        {
            "type": "Participant",
            "id": "mN2I3NTM2MTItMDhlNi00OWU5LWFkMTItMWJlMjRmYWI5Mjlj",
            "created": "2021-06-09T03:42:26.317366Z",
            "controller": [
                "mN2I3NTM2MTItMDhlNi00OWU5LWFkMTItMWJlMjRmYWI5Mjlj"
            ],
            "verificationMethod": [
                {
                    "type": "Ed25519VerificationKey2021",
                    "id": "mN2I3NTM2MTItMDhlNi00OWU5LWFkMTItMWJlMjRmYWI5Mjlj#2021-06-09T03:42:26.317366Z#key-0",
                    "publicKeyMultibase": "zEHwiDynVvinC6jjzH5RR4MwgxYPq4xiRagfksAyUPyjv"
                }
            ],
            "assertionMethod": [
                {
                    "type": "Signature",
                    "id": "mN2I3NTM2MTItMDhlNi00OWU5LWFkMTItMWJlMjRmYWI5Mjlj#2021-06-09T03:42:26.317366Z#am-0",
                    "verificationMethod": "mN2I3NTM2MTItMDhlNi00OWU5LWFkMTItMWJlMjRmYWI5Mjlj#2021-06-09T03:42:26.317366Z#key-0"
                }
            ]
        }
    ],
    "proof": [
        {
            "document": "mYzRiZGIzMTItNmUxOC00ZDE1LThjNmYtMDgxYWE4YTY5Yzk1",
            "issuer": "mN2I3NTM2MTItMDhlNi00OWU5LWFkMTItMWJlMjRmYWI5Mjlj",
            "created": "2021-06-09T03:42:26.317366Z",
            "type": "JcsBase64Ed25519Signature2021",
            "assertionMethod": [
                "mN2I3NTM2MTItMDhlNi00OWU5LWFkMTItMWJlMjRmYWI5Mjlj#2021-06-09T03:42:26.317366Z#am-0"
            ],
            "signatureValue": "o_Nna_q_skVE7-5r3mj8HMAvPBSo1LIiJxbbjT0AWWLJnOWGThWxLLU7-t5_fH0yiv0pd1OyfwjLLU3sUAfeBQ",
            "nonce": "38aab536-9433-47c9-ba17-259bb40a2cad"
        }
    ]
}
```
## "declaration"."type": "Participant"
Specifies the type of object to included in this declaration.

## "declaration"."id"
This is the unique identifier of the participant. This shall be unique as the DialChain does not allow for duplicate declarations. A new declaratation with the same id is considered a modification of the existing declaration.

### Validation Rule PTP0001
A "declaration"."id" is unique. The submission of a new declaration carrying this same id is understood  by the network as a modification request.

## "declaration"."controller"
Participant that is authorized to make changes to this declaration.

## "declaration"."verificationMethod"
Declaration of public keys used to verify proofs produced by this participant. Note that to keep schema simple and reduce ambiguity, we do not allow the controller property inside a verification relationship (like verificationMethod, assertionMethod). The global controller of the declaration is the only one allowed to modify the declaration.

## "declaration"."assertionMethod"
Reference on verificationMethods used to validate assertions produced by this participant.

## "declaration"."assertionMethod"."type":"Signature"
Defines the data format of the assertionMethod. In this case a simple signature.

## "proof"
Collects proofs associated with declarations being submitted. For a simple participant declaration, the proof allows the validation of the declared assertionMethod, thereby also allowing the validation of the referenced verificationMethod (or public key).
