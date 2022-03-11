# Publication
A publication is the act of a validator asserting correctnes of a declaration by signing that declaration.

## Publicaion Process

### Participant
- Participant produces a declaration
- Participant signed the declaration.
  - If this is a new declaration, participant signs using the generated keypair.
  - If this is a modification, participant signs using the controller key pair found on the lates declaration.
- Participant sends the curent and the last declaration to each validator of the target ime window.

### Validator 
- Validator receives the declaration from the participant. Including the preceeding validation in the case of a modificcation.
- The validator uses the Id of the submited declaration to:
  - Find out the previous neighborhood responsible for the declaration
  - Issues a request to all validators of that neighborhood to obtain the partial merkel tree associated with the declaration.
  - Previous validators will return nothing if they don know the declaration
  - Will return each a partial merkel tree if hey know the declaration
- The validator will use this information to verify
  - Legitimacy of the current controller in the case of a modification
  - The non existance of such a declation in the ccase of a new declaration
- The validator will then
  - Sign the declaration and return it to the participant
  - Include the cid of the signed declaration to the new protocol.

A single proof block returned to the requesting participant has the following structure:
```json
{
    "type": "Publication",
    "cid": [
        "B7NCdnaDQvwipw4YLV58MHb1yCkW6rTamgwCXwVNHtqijxRroN6wDa86LG1myQCthekWsf3sNLJrU1M4YNa61hQXdYBz"
    ],
    "proof": [
        {
            "issuer": "zEruWfhngbEc16jmpZBHSk4Tx872CHDWXeNsDJfL8yHo6",
            "created": "2021-06-24T21:36:03.457066Z",
            "type": "JcsBase64Ed25519Signature2021",
            "signatureValue": "sigBytes",
            "nonce": "33019ed2-99a9-4feb-984b-adfcaf0b2b39"
        }
    ]
}
```
It contains:
- The cid of the new version of the declaration
- The signature of the validator including metadata. 

## Structure of a Publication
A publication contains a reference to a declaration file produced and signed by one or many other participants. A publication is put toghether by the requesting participant, as he is in charge of keeping record of all validators assertions.

The following json file displays a publication.
```json
{
    "type": "Publication",
    "cid": [
        "B7NCdnaDQvwipw4YLV58MHb1yCkW6rTamgwCXwVNHtqijxRroN6wDa86LG1myQCthekWsf3sNLJrU1M4YNa61hQXdYBz"
    ],
    "proof": [
        {
            "issuer": "zEruWfhngbEc16jmpZBHSk4Tx872CHDWXeNsDJfL8yHo6",
            "created": "2021-06-24T21:36:03.457066Z",
            "type": "JcsBase64Ed25519Signature2021",
            "signatureValue": "sigBytes",
            "nonce": "33019ed2-99a9-4feb-984b-adfcaf0b2b39"
        },
        {
            "issuer": "zAo7AYWYkFH2cPfmfq4LEzwGk7UTJYePDbqGozztnK8Kt",
            "created": "2021-06-24T21:36:03.457066Z",
            "type": "JcsBase64Ed25519Signature2021",
            "signatureValue": "sigBytes",
            "nonce": "41179231-bf1f-4399-827f-50b9ebaa61bf"
        }
    ]
}
```

## Publication File
A publication file does not need to be maintained anywhere. It is held by the participant controlling (owner of) the asset. This will be used to prove ownership of the asset during the next transfer of the asset to a new controller.

## [type]
The DIAL file type. "Publication" means it indicates that this document is a publication.

## [cid]
Reference to documents verified by this validator and part of this publication. A validator can use a single publication to publish many unrelated declaration files.

## [proof][i]
A publication will be signed by one or many validators.

## [proof][i][issuer]
Identity of the node signing the publication.

## [proof][i][created]
Signature timestamp. This is an essential timestamp as it determines the time window (block) in which to put the publication. For this association, the timestamp of the youngest proof entry is used.
