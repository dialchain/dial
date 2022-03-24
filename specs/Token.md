# Token
A token is the unit of existence in the dial network. There is nothing else in the dial network but tokens.

## Json-CBOR Representation
Note that (1) we will use Json to describe the structure of document in prose, (2) We will use [CBOR](https://datatracker.ietf.org/doc/html/rfc8152) as the underlying serialization format, (3) we will use [multicodec](https://github.com/multiformats/multicodec) to prefix all binary representations of keys, hashes and content identifiers.

## Token Reference
A token reference is the representation of a token as it appears in a neighborhood protocol.

### Json
```json
{
    "id": "unique publicKey multihash",
    "mod": 20220323121835,
    "wrk": 1800,
    "mr": "merkel root multihash"
}
```

### Identifier (id)
The unique identifier of a token is the hash of the public key generated for the purpose of identifying this token. The underlying keypair is used to legitimate the token declaration (proof of execution) at creation.

### Modified (mod)
This is either the creation or the last modification timestamp. This is essential to indicate the version of cryptographic materials used to produce the certificates.

### Work (wrk)
The work is the amount of work unit held by the token. If we assume that a token spends a work unit per time window to stay in the log, the work value of 24 will indicate that the token can still be carried thru 24 time windows and then forgotten.

The notion of work implicitely creates an expiration time for the token. Means the token expires when the work carries the value zero.

### Merkel Root (mr)
This is the merkel root of the token state as verified by the publisher of the last modification. This information is not present for the creation record.

The token state is mainly held by the controller of the token, and presented with the next modification request to publishers.

As  publishers are not required to archive protoccols and token states, a participant can use the _mod_ field to derive the neighborhood carying the protocol of this last modification. The neighborhood identifier might in turn be used to retrieve those verification data (protocols and token states) from deliberate archiving services.

## Token State
The token state holds information necessary to document modifications on the token.

### Json
```json
{
    "id": "unique publicKey multihash",
    "mod": 20220323121835,
    "wrk": 1800,
    "ctl": "controller script multihash",
    "hash": "token data multihash",
    "crt": [
        {
            "iss": "issuer identifier unnique publicKey multihash",
            "ts": 20220323121835,
            "ppse": "proof purpose e.g. PoP",
            "type": "proof type e.g. JcsBase64Ed25519Signature2021",
            "vm": "issuer publicKey multihash",
            "sig": "NJlKbI7fqMzkm_PWpfd4jCPdVghxaH3gYw3tH22Ht29xen6DW0anTps...",
            "nonce": "43102c83-c20f-4e38-bfe0-b805bf54c6e2"
        },
        "additional certificates"
    ],
    "mr": "merkel root multihash"
}
```

### Controller (ctl)
This is the hash of the controller script whose successfull execution is required for the next modification on this token. This script is not disclosed before the that modification request.

The simplest version of the script is a public key and the corresponding signature algorithm. The corresponding __proof of execution (PoE)__ is therefore a signature of the modification request with the corresponding private key.

A more complex script might contain multiple signers, hash, time or discrete lock constraints, or more complex execution rules like smart contracts. The way the script is executed is not in the scope of the Dial. But the verification of the proof of execution (PoE) must be performable by each publisher of the Dial. 

The extent of execution rules allowed is documented by the Dial. As the verification of the successfull execution of each script type has to be performable by each Dial publisher.

The cost of verifying the PoE of a script determines the payment needed for the submission of the request modifying the token guarded by that script. This is different from the cost and effort needed to move an unmodified script from one time window to another, this last one is constant.

### Work (wrk)
The amount of work units sustaining this token at the given date. Recall that the a token will spend one work unit to get accross one time window. The work can therefore be seen as the time to live (TTL) of the token.

Recall that the work does not include the payment required to verify the PoE of the controller script. The effort needed to verify the PoE of the controller script is denpendent on the complexity of the script. The resulting amount is to be paid for the verification of the PoE. This amount is provided by the participant submitting the change declaration.

### Token Hash (hash)
The is the multihash of the token content. This is held at the discretion of the token controller and is neither used nor modified by the Dial.

The uderlying meaningful content of the token shall be exchanged off chain between transacting parties and do not need to ever be disclosed to the Dial.

### Certificates (crt)
Publication certificates are issued by publishers and are a proof that the token is part of the Dial. Those certificates are:
- produced by publishers
- returned to controllers
- included in the computation of the merkel root of the token state.

No entity other than the controller of the token is required to hold a copy of those certificates. The controller will present those certificates to Dial publishers with the next modification request.

For the production of the signature input data of a certificate, the token state is striped off:
- all other certificate entries
- the _sig_ field of the current certificate
- the _mr_ field

resulting to the following file. AAdditionnaly, [Cannonical CBOR](https://datatracker.ietf.org/doc/html/rfc7049#section-3.9) rules are applied for the repeatable production of signature input data.

```json
{
    "id": "unique publicKey multihash",
    "mod": 20220323121835,
    "wrk": 1800,
    "ctl": "controller script multihash",
    "hash": "token data multihash",
    "crt":[
        {
            "iss": "issuer identifier unnique publicKey multihash",
            "ts": 20220323121835,
            "ppse": "proof purpose e.g. PoP",
            "type": "proof type e.g. JcsBase64Ed25519Signature2021",
            "vm": "issuer public key multihash",
            "nonce": "43102c83-c20f-4e38-bfe0-b805bf54c6e2"
        }
    ]
}
```

### Merkel Root
The merkel root of the token state is computed out of:
- leaf-1: all field of the token state except the field _crt_ aand _mr_
- leaf-2..n : all crt provided by publishers.

As the number of publishers of a neighborhood is known in advanced, if a publisher hasn't returned a certificate, the corresponding _crt_ entry will still be present, but with the only field _iss_.

CBOR cannonicalization rules are also applied to ensure repeataable production of identical input data.

The list of _crt_ is sorted aaccording to the lexicographical representation of the _crt.iss_ field (identifier of the issuer). The entry will look like:

```json
{
    "iss": "publisher identifier unnique publicKey multihash"
}
```

## Declaration
In order to create or modify a token, a participant must send a declaration file to the neighborhood hosting the token identifier.

### Declaration File
A declaration file will generally contain many declarations.
- the declaration referencing the main token being modified
- the declaration referencing payment tokens

```json
{
    "decl": ["List of declarations"],
    "pymt": 
    {
        "coin":["List of identifiers of coins used for the payment, identifier listed above"],
        "pow": ["proof of work provided to support the declaration. evtl supported with reputations listed aabove."]
    }
}
```
Recall that all tokens and payments addressed in a declaration file must be custodied in the same neighborhood for the given time window.

### Declaration Entry
A single declaration entry provides (1) the current state of the token as known to the Dial, (2) the content of the current controller script, (3) the new state of the token, and (4) the proof of execution of the controller script.
```json
{
    "state": {
        "id": "token unnique publicKey multihash",
        "ctl": "controller script multihash",
        "wrk": 1300,
        "hash": "token data multihash",
        "crt": ["... additional certificates"],
        "mr": "merkel root of the last state of the token"
    },
    "ctl": {
        "ppse": "proof purpose e.g. PoE",
        "vm": "issuer publicKey multihash",
        "type": "proof type e.g. JcsBase64Ed25519Signature2021",
        "nonce": "e.g. 43102c83-c20f-4e38-bfe0-b805bf54c6e2"
    },    
    "token":{
        "id": "unnique publicKey multihash",
        "ctl": "new controller script multihash",
        "hash": "new token data multihash",
    },
    "poe": "signature e.g. NJlKbI7fqMzkm_PWpfd4jCPdVghxaH3gYw3tH22Ht29xen6...",
}
```

Note that part of the new token state is the merkel root of the current state as found in the protocol of the dial.

### Proof of Execussion (PoE)
For each declaration, the controller must provide a proof of execution of the current controller script of the referenced token. If the token is new, the controller must provide a proof of execution of the public key hash representing the identifier of that token. 

In the case of a new token, the field _state_ is not present. The field _ctl_ contains the description of the public key producing the token identifier.

### Verifying a Declaaration
In order to verify a declaration, the publisher must be in possession of:
- the last time window protocol, that aggregates neighborhood protoccols. This protocol is verifiable as it aggregates to the time window hash universally available,
- the protocol of the neighborhood hosting the token in that time window. This protocol is verifiable, as the merkel root is a leaf of the time window protocol,
- the last state of the token. This is provided by the submitting controller as part of the submitted declaration. The token state is verifiable as the merkel root is the part of the token entry forming the leaf of the time window protocol,
- the controller script referenced in that token state. This script is verifiable as the hash is documented in the field _ctl_ of the token state.

After verifying the authenticity of the controller script, the publisher will haash the new token state (field "token") included in the declaration and use the algorithm and hash included in the controller script to verify the proof of execution provided in the field poe.

### Publishing a Declaration
Upon successful verification, the publisher will produce and return a certificate to the submitting participant. The certificate will have the following format:
```json
{
    "id": "token unnique publicKey multihash",
    "ctl": "controller script multihash",
    "wrk": 1300,
    "hash": "token data multihash",
    "crt":{
        "n":"N2022032312-13",
        "iss": "issuer identifier unnique publicKey multihash",
        "ts": 20220323121835,
        "ppse": "proof purpose e.g. PCert",
        "type": "proof type e.g. JcsBase64Ed25519Signature2021",
        "vm": "issuer publicKey multihash",
        "sig": "signature e.g. NJlKbI7fqMzkm_PWpfd4jCPdVghxaH3gYw3tH22...",
        "nonce": "e.g. 43102c83-c20f-4e38-bfe0-b805bf54c6e2"
    }
}
```
The certificate displays following fields:
- n : the neighborhood identifier. Also implicitly references the time window.
- iss: the identifier of the publisher.
- sig: the signature of the publisher. Signature data is everything else in the block except the "crt.sig" field.

### No Archivinng of Proofs
Publishers are required to hold the certificates until custodianship on the token is passed over to a new neighborhood. In which case publishers of the new neighborhood can verify the token before acceptance and are then free to forget the certificates.

The dial network does not require publishers to archive document they certify. The network assumes each controller of a token has an economic interest in keeping the last active version of the token declaration and the supporting certificates.

The sole information to be maintained by publishers for the purpose of performing their duties are neighborhood protocols.

