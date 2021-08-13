# Declaration
A declaration is the fundamental unit of expression in a dial nework. Even the devinition of the network is provided through declarations. A dleclaration always refers to a token and carries the id of the underlying token. A declaration therefore must be used to create, modify or retire a token.

# Delaration Class
The folowing json file displays the definitionn of a declaration class/

```json
{
    "nid":"id of the network. Will be used to publish genesis files under ipfs/ipns address",
    "dec": [
        {
            "type": "Class",
            "Class": "Class Name. Appear as type in the declaration file.",
            "id": "id of this declaration class.",
            "vmt": "type of publicKey",
            "schema": "Schema of the declaration",
            "controller":{
                "id": "zEruWfhngbEc16jmpZBHSk4Tx872CHDWXeNsDJfL8yHo6",
                "type": "network",
                "reputation-count": "8640",
                "votes-percent":"51",
                "vote-period":"4320",
                "grace-period":"720"
            }
        }
    ],
    "proof":[
        "pop of the crator of this document. For creation, signature of id, for modification, controll rule."
    ],
    "pow" : [
        "proof of works associated with this declaration." For each proof provided above, aseparated proof of work will be included here".
    ]
}
```

## nid
The network id. This is the identifier of the etwork for which this file is defined. This can be the main net, the test net.

## dec
This is the declaration block. ITt is generally a list. Each decalration in the list has a proper identifier. The identifier references the token underlying this declaration. (1) for the creation of the new token, the identifier must be a public key. (2) The vmt (__Verification Method Type__)  entry references the type of key used to generate the id. (3) The schema describes the structure of an instance. (4) the controller entry defines control rules, for the modification of this definition.

### dec.controller
the controller entry defines control rules, for the modification of this class. The proof 

# Publication of the Delaration Class
The declaration class has to be published by genesis participants. This is done by having them sign the declaration.
```json
{
    "pub": [
        "B7NCdnaDQvwipw4YLV58MHb1yCkW6rTamgwCXwVNHtqijxRroN6wDa86LG1myQCthekWsf3sNLJrU1M4YNa61hQXdYBz"
    ],
    "proof": [
        "Assertions of validators certifying this publication. One entry per validators."
    ],
    "pow" : [
        "proof of works associated with proofs. One pow per proof".
    ]
}
```

The pub entry contains the list of cid of declaration files validated.

