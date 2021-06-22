# Publication
A publication is the act of a validator adding a file to a DialChain. For this purpose, a validator  must expose a publisher service.

## Structure of a Publication
A publication contains a declaration file produced and signed by one or many other participants. The validator will:
- make sure that declation submitted for publication do not conflict with the current state of the DialChain.
- wrap file into a new file
- add a publication proof to the file.

The following json file displays a publication. Following element added to the file:
- a twindow entry identifying the block in which the file is inserted
- a proof sub element containing signature of the publishinng organization's validator node.

```json
{
    "id": "mMDYzN2VjMzktMjhhOC00MjU5LWFkYmEtNGMwNTkzYTAyYmI1",
    "type": "Publication",
    "document": {
        "id": "mODI4ZTFkMjAtY2NkMC00YjBjLWFjNjUtMDVjMzRkNTg4NGJm",
        "type": "Declaration",
        "declaration": [ "content of the organization declaration, including voting rules."],
        "proof": ["assertions (signatures) of all members of the organization."]
    },
    "twindow": {
        "start": "2021-06-20T00:00:00Z",
        "end": "2021-06-21T00:00:00Z",
        "missing": "a_closinng & a_hash are not available in the genesis records, as these are the first records."
    },
    "proof": [
        {
            "document": "mMDYzN2VjMzktMjhhOC00MjU5LWFkYmEtNGMwNTkzYTAyYmI1",
            "issuer": "mY2VlZjZjOTItYzM5Yi00MzBlLTljMGMtMjI0MjZiMTY0Yzdl",
            "created": "2021-06-20T00:04:36.462561Z",
            "type": "JcsBase64Ed25519Signature2021",
            "assertionMethod": [
                "mNGI5YjBmNTgtODBmMy00NmQwLTk5YmMtNTUwNWI0MTJiZWJh#2021-06-20T00:04:31.742503Z#am-0",
                "mY2VlZjZjOTItYzM5Yi00MzBlLTljMGMtMjI0MjZiMTY0Yzdl#2021-06-20T00:04:31.723188Z#am-0",
                "mY2VlZjZjOTItYzM5Yi00MzBlLTljMGMtMjI0MjZiMTY0Yzdl#2021-06-20T00:04:31.723188Z#key-0"
            ],
            "signatureValue": "QPtPQVqQmFJLaImsXe1QOZfStmcvP6NZ2N7cbIU35jSX2ShbFKcTu6vMnFeIZmv9r9JdOsacwQMzQwwq3WEeDg",
            "nonce": "68dc7243-655c-4521-bdfb-6c6b83718981"
        },
        {
            "document": "mMDYzN2VjMzktMjhhOC00MjU5LWFkYmEtNGMwNTkzYTAyYmI1",
            "issuer": "mNDA5MTVkNzMtZDU3Mi00YzgwLWI3OWEtMDFjZDI4NGNlNGU0",
            "created": "2021-06-20T00:04:36.462561Z",
            "type": "JcsBase64Ed25519Signature2021",
            "assertionMethod": [
                "mNGI5YjBmNTgtODBmMy00NmQwLTk5YmMtNTUwNWI0MTJiZWJh#2021-06-20T00:04:31.742503Z#am-0",
                "mNDA5MTVkNzMtZDU3Mi00YzgwLWI3OWEtMDFjZDI4NGNlNGU0#2021-06-20T00:04:31.731667Z#am-0",
                "mNDA5MTVkNzMtZDU3Mi00YzgwLWI3OWEtMDFjZDI4NGNlNGU0#2021-06-20T00:04:31.731667Z#key-0"
            ],
            "signatureValue": "mBv7BNpY9-ZD1thqglMmTK_oRu1MjXZ6GGxDe-T8UFto7Uki4soMoaFVIoeVEG3QcoCrjzltjot2B5J4OoVeBQ",
            "nonce": "0ac6719e-fa3f-4a9d-bf9b-f4a069b7e612"
        }
    ]
}
```
## General Items
The structure of this document is very similar to the one defined in [Participant](./Participant.md). Therefore similar elements will not be explained here.

## [type]
The DIAL file type. "Publicationn" means it indicates that this document is a publication.

## [document]
The declaration file is embedded in the document element of this publicattion file.

## [twindow]
This indicates the time window (block) in which this document is published. For the genesis publication, antecedant information are missing, as we are dealing with the first publication.

## [proof]
This element documents the signature of nodes of this validator. In the simplest case, 2 of 3 nodes have to sign each publication for it to be considered valid by other validators of the network.

## [proof][assertionMethod]
The list of identifiers included in he assertion method block represent the chain of delegation:

- the first entry mNGI5YjBmNTgtODBmMy00NmQwLTk5YmMtNTUwNWI0MTJiZWJh#2021-06-20T00:04:31.742503Z#am-0 representts the assertionn method of the signing organization.
- the second entry mY2VlZjZjOTItYzM5Yi00MzBlLTljMGMtMjI0MjZiMTY0Yzdl#2021-06-20T00:04:31.723188Z#am-0 is tthe assertion mehod of the member entry
- the thrid entry mY2VlZjZjOTItYzM5Yi00MzBlLTljMGMtMjI0MjZiMTY0Yzdl#2021-06-20T00:04:31.723188Z#key-0 is the corresponding verification method of the member entry. This directly references the public key used by the member to produce the proof.

# Publisher Service
