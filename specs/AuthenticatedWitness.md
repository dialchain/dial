# Authenticated Witness
In order to allow business to use blockchain technology in accordance with law and legistations contrrolling their environment, we introduce the concept of __authenticated witness (AuthWit)__. AuthWit allows some tokens issuers to limit the transaction of those tokens to authenticated users, without nevertheless disclosing the identity of those users onchain.

The authenticated withness is the participant that can witness the identity of the controller of a declaration. The authenticated withness entry of a declaration can therefore not be changed by the controller of that declaration.

The following declaration contains an authennticated witness entry:
```json
{
    "type": "Declaration",
    "declaration": [
        {
            "type": "Participant",
            "id": "zEruWfhngbEc16jmpZBHSk4Tx872CHDWXeNsDJfL8yHo6",
            "created": "2021-06-24T21:36:03.409110Z",
            "authenticatedWitness": [
                "z6Sdi3MYqAr1d3UvSKUAqyrZcy4u676rRnqUg7kitioAe"
            ],
            "controller": [
                { 
                    "type" : "AuthWit",
                    "id" : "zEruWfhngbEc16jmpZBHSk4Tx872CHDWXeNsDJfL8yHo6",
                    "proof": [
                        {
                            "issuer": "z6Sdi3MYqAr1d3UvSKUAqyrZcy4u676rRnqUg7kitioAe",
                            "proofPurpose": "Assertion",
                            "type": "JcsBase64Secp256k1Signature2021",
                            "verificationMethod": "z6Sdi3MYqAr1d3UvSKUAqyrZcy4u676rRnqUg7kitioAe#2021-03-12T12:23:01.305216Z#key-3",
                            "signatureValue": "b5yQFpG7wSD87PzO1cElBWx-IXKhS8Ad-s-cE2vBpUsRjFOm-fDakZ6rs5M1CFh-LPkmdEdCpsPKPHGTNp5Ptg",
                            "nonce": "097d3da2-95f8-47d3-8961-8fee21f7dd48"
                        }
                    ]
                }
            ],
            "rest...": "ignored for display ..."
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
        }
    ]
```

## Proof
The proof entry proves possession of the identifier of the creator of the token.

## AuthWit
The controller entry contains a proof certifying the identity of the new controller of the token. It is the signature of the public key bytes of the controller (embedded in the controllers multibase id string). Like all dial nnetwork documents, this proof is the signature of the AuthWit document without the proof block. For annonymity purpose, this AuthWit document must not conntain a signature or creation date.

## Validations
- A validator will never allow a controller to change the AuthWit entry.
- A validator will always make sure the the AuthWit proof appies to the controller id mentioned above.