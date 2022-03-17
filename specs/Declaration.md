# Declaration
A declaration is the fundamental unit of expression in a Dial. A dleclaration always refers to a token and carries the identifier of that token. A declaration therefore must be used to create, modify or retire a token. For this purpose, each declaration exposes a controller property that defines modification rules of the underlyinng token.

# Delaration Class
The folowing json file displays the definition of a declaration. We will use JSon for readability purpose. The main message format used by the Dial is a CBOR representation of JSon objects described here.

```json
{
    "nid":"identifier of the network.",
    "dec": [
        {
            "type": "type of this declaration",
            "id": "id of this declaration class.",
            "ctl":"hash of the controller state of this declaration.",
            "exp":"expiration timestamp in seconds since epoch",
            "pyld":"hash of the token payload"
        }
    ],
    "proof":[
        "proof of possession of the crator of this document. For creation, signature of id, for modification, controll rule, payload of the authorization state"
    ],
    "pow" : [
        "payment or proof of works associated with this declaration."
    ]
}
```

## nid
The network identifier. This is the identifier of the etwork for which this file is defined. This can be the main net, the test net, another network.

## dec
This is the declaration block. It contains a list of declaration entries. 

### dec.type
Refers to the type of this declaration. Declaration can represent:
- a token : represent aany identifiable entity. Justifies the presence aof a pyld field containing the hash of the token payload.
- a performance : represents a performance declaration. Justify the presence of a srv block.
- a protocol : represents a protocol, containing the merkel tree.
- an asset : represents a token that can be given a value. Justifies the presence of the assetType (atyp) and assetValue (aval) field.

### dec.id
Each decalration in the list has a proper identifier. 
- The identifier references the token underlying this declaration. 
- The identifier is the hash of a public key
- for the creation of the new token, controller must prove possession of the corresponding a private key (in the proof block).

All declarations entries in a declaration file must fall in the same neighborhood for the given time window.

### dec.ctl
This is the hash of a controller state file. The controller state file will be presented to publisher with the next modification request.

### dec.exp
The expiration timestamp. This is the date at which the token will be abandonned by the Dial.

A controller can submit a declaration to extend the expiration date of a token.

### dec.pyld
The paayload is the hash of the payload of the token.

## Proof
The proof block contains the proof of control  of a declaration. Each proof entry references a declaration entry. The proof entry also presents a controller state block whose hash matches the ctl block of the declaration.

## PoW
The proof of work provided payment associated with the declaration.

# Token
A declaration is a document used to create or modify a token. For this purpose, each declaration exposes a controller property that defines modification rules of the underlyinng token.

## Creating a Token
A token is created by providing a declaration with a new public key hash. The declaration is signed with the corresponding private key. In order to be modifiable, a token must be created with a controller property.

The publisher of a new declaration must only verify that the declaration is correctly signed with the private key of the public key used to build the token identifier.

## Modifying a Token
In order to change the token (properties CTL, EXP, CID), the current controller must sign and submit a declaration for publication.

## Publishing a Declaration
The purpose of the Dial is to finalize declarations by publishing them in the Dial. Publishing is done by applying following rules:
- Anyone can submit a declaration to create a token. Creator must sign the initial declaration with the private key matching the declaration identifier.
- Once created, only the latest controller of a token can sumit a modification on the token by signing the modifying declaration with the private key matching the identifier of the controller property (CTL) of the token.

In order to publish a declaration,
- The controller of the underlying token submits the declaration to all publishers of the neighborhood for that token (THost).
- A THost publisher upon reception of a publication request,
  - proceeds with the formal validation of the contained declaration (mandatory information like ID), then
  - matches the declaration against the current state of the token (controller identifier),
  - proceeds with the verification of control rules (signature of the current controller), then
  - produces a verification certificate (VCert) and returns it to the requesting participant. 
- The controller upon receiving more than half of the responses (VCerts), submits the declaration for publication to all publishers hosting the token's neighborhood (NHost)
- An NHost publisher upon reception of the publication request,
  - verifies the legitimacy of all included VCerts including the majority rule
  - enforces the verification of remaining publishers of the THost if missing
  - produces a publication certificate (PCert) and returns it to the requesting participant

The declaraation is considered published when the controller (requesting participant) holds more than half of the PCerts.
