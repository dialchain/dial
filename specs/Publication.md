# Publication
A publication is the act of a validator adding a file to the DialChain log. For this purpose, a validator must expose a publisher service.

## Structure of a Publication
A publication contains a reference to a declaration file produced and signed by one or many other participants. The validator will:
- make sure that declarations submitted for publication do not conflict with the current state of the DialChain.
- wrap file into a new file
- add a publication proof to the file.

The following json file displays a publication. Following element added to the file:
- a twindow entry identifying the block in which the file is inserted
- a proof sub element containing the assertion of the publishing organization (signature of validator nodes).

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
            "assertionMethod": [
                "zGCPM1TZZdBTdH1LUrP1u38Y3L89wVj94Y8iBXCLEeMqZ#2021-06-24T21:36:03.422792Z#am-0",
                "zEruWfhngbEc16jmpZBHSk4Tx872CHDWXeNsDJfL8yHo6#2021-06-24T21:36:03.409110Z#am-0"
            ],
            "verificationMethod": "zEruWfhngbEc16jmpZBHSk4Tx872CHDWXeNsDJfL8yHo6#2021-06-24T21:36:03.409110Z#key-0",
            "signatureValue": "nU81rjImBqm4sAilkHJbqWDZO8Hm0P_JviHQemr7jvhmSEcU6oOZTQN_WkZzmNhwXuIpP7Y0pO5Yo5vLio_sCg",
            "nonce": "33019ed2-99a9-4feb-984b-adfcaf0b2b39"
        },
        {
            "issuer": "zAo7AYWYkFH2cPfmfq4LEzwGk7UTJYePDbqGozztnK8Kt",
            "created": "2021-06-24T21:36:03.457066Z",
            "type": "JcsBase64Ed25519Signature2021",
            "assertionMethod": [
                "zGCPM1TZZdBTdH1LUrP1u38Y3L89wVj94Y8iBXCLEeMqZ#2021-06-24T21:36:03.422792Z#am-0",
                "zAo7AYWYkFH2cPfmfq4LEzwGk7UTJYePDbqGozztnK8Kt#2021-06-24T21:36:03.415619Z#am-0"
            ],
            "verificationMethod": "zAo7AYWYkFH2cPfmfq4LEzwGk7UTJYePDbqGozztnK8Kt#2021-06-24T21:36:03.415619Z#key-0",
            "signatureValue": "USD8oFoBTtIo4Js1EPGe7OohjE1FFJU0QMFR4MiBdvNxWBd7RNlK8qWIEKFoYTw86u8RfQXf-VaBzCMXtNOfDw",
            "nonce": "41179231-bf1f-4399-827f-50b9ebaa61bf"
        }
    ]
}
```
## Content Identifier
```json
"B7NCdGj9RF7x5AHWbMGPtPLtw4UDgVr4knpKb49Fa44vUUonFxiJCme5fouGyyn5cdjKi1Shwa53Rh2QWSXa4BH3cMTx"
```

## Publication File
Each publication is a file, identified by its content identifier.

## [type]
The DIAL file type. "Publication" means it indicates that this document is a publication.

## [cid]
Reference to documents verified by this validator and part of this publication. A validator can use a single publication to publish many unrelated declaration files.

## [twindow]
This indicates the time window (block) in which this document is published. For the genesis publication, antecedent information are missing, as we are dealing with the first publication.

## [proof][i]
A publication will be signed by 2 of 3 nodes of the same validator.

## [proof][i][issuer]
Identity of the node signing the publication.

## [proof][i][created]
Signature timestamp. This is an essential timestamp as it determines the time window (block) in which to put the publication. For this association, the timestamp of the youngest proof entry is used.

## [proof][i][assertionMethod]
The list of identifiers included in the assertion method block represents the chain of delegation:

- the first entry "zGCPM1TZZdBTdH1LUrP1u38Y3L89wVj94Y8iBXCLEeMqZ#2021-06-24T21:36:03.422792Z#am-0" represents the assertion method of the signing organization.
- the second entry "zAo7AYWYkFH2cPfmfq4LEzwGk7UTJYePDbqGozztnK8Kt#2021-06-24T21:36:03.415619Z#am-0" is the assertion method of the signing member entry

## [proof][i][verificationMethod]
The verification method associated with the last assertion method entry in the list of assertion methods. "zAo7AYWYkFH2cPfmfq4LEzwGk7UTJYePDbqGozztnK8Kt#2021-06-24T21:36:03.415619Z#key-0" is the corresponding verification method of the member entry. This directly references the public key used by the member to produce the proof.

# Publisher Service
