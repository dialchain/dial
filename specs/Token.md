# Token
A token is the unit of existence in the dial network.

## Data Structure
```javascript
/*
The unique identifier of a token. 

It is the hash of the public key generated for the purpose of identifying
that token. The underlying  keypair is used to legitimate the token 
declaration (proof of execution) at creation.

The current format is: sha256. 

The omission of a network identifier is intentional.
*/
token-id = (id: bytes .size 32)
issuer-id = token-id

/*
The token representation contains sufficient information to keep track 
of a token in the Dial. Fields modif and work can be used to determine 
if the token still has some available resources to support maintenance
in the Dial.

The token representation is only modified when the controller sends 
a modification request of the underlying token.
*/
token = {
    /* id
    The unique identifier of a token.     
    */
    token-id, 

    /* modif
    Creation or last modification timestamp in seconds since epoch. 
    
    This is essential to indicate the version of cryptographic 
    materials used to produce certificates. e.g.: 1648467741
    */
    modif: int,

    /* work
    Amount of work units (wu) held by the token. 

    If we assume that a token spends a work unit per time window to stay in 
    the log, the work value of 24 wu will indicate that the token can still 
    be carried through 24 time windows and then forgotten. e.g. 2312.

    The notion of work implicitely creates an expiration time for the token. 
    Means the token expires when the work carries the value zero.

    The work does not include the payment required to verify the PoE of the 
    controller script. The effort needed to verify the PoE of the controller 
    script is denpendent on the complexity of the script. The resulting amount
    is to be paid for the verification of the PoE. This amount is provided by 
    the participant submitting the change declaration.
    */
    work: int,

    /* reptn
    The reputation credit attached to this token.

    Every single work unit spent by a token is added to the reputation credit 
    of that token. The value of the _rep_ field can be awarded to the 
    participant if the participant provides a reputation token with the 
    next modification request. e.g. 35
    */
    reptn: int,
}

/*
Type of proof. e.g. JcsBase64Ed25519Signature2021. Only enumeration
entry available  for the moment.
*/
verification-method-type = &("JcsBase64Ed25519Signature2021": 1)

/*
A certificate is a proof of reception and optionaly verification of an information.
*/
certificate = {
    /* iss
    Unique identifier of the issuer of this certificate. 
    
    Muss be a multihash of the public key of the issuer.
    */
    issuer-id,

    /* ts
    Signature timestamp

    Dial does not expect the same issuer to provide two certifiates for
    the same information in the same second. e.g.: 1648467741
    */
    ts: int,

    /* type
    Type of verification method.
    */
    type: verification-method-type,

    /* vm 
    verification-method.
    
    Issuer public key in the format specified by the given type
    method. Recall that the public key also matches the hash to 
    the given iss field.
    */
    vm: bytes,

    /* hash
    This is the hash of the content to be signed. 
    
    Used to build the neighborhood token protocol.
    */
    hash: multihash, 

    /* nonce
    Random nonce bytes. Limited to 32 bytes.
    */
    nonce: bytes .size 32,

    /* sig
    Signature bytes, in the format specified by the type field.
    */
    sig: bytes,
}

/*
The token state holds information necessary to document modifications 
on the token. The token state is mainly held by the controller of the token,
and presented with the next modification request to publishers.

As  publishers are not required to archive protoccols and token states, 
a participant can use the _modif_ field to derive the neighborhood 
carying the protocol of this last modification. The neighborhood identifier
might in turn be used to retrieve those verification data 
(protocols and token states) from deliberate archiving services.
*/
token-state = {
    /* id
    Token representation as described above.
    */
    ~token, 

    /* ctl
    Multihash of the controller script.

    This is the hash of the controller script whose successfull execution 
    is required for the next modification on this token. This script is 
    not disclosed before the that modification request.

    The simplest version of the script is a public key and 
    the corresponding signature algorithm. The corresponding 
    proof of execution (PoE) is therefore a signature of the 
    modification request with the corresponding private key.

    A more complex script might contain multiple signers, hash, 
    time or discrete lock constraints, or more complex execution rules 
    like smart contracts. The way the script is executed is not 
    in the scope of the Dial. But the verification of the proof 
    of execution (PoE) must be performable by each publisher of the Dial. 

    The extent of execution rules allowed is documented by the Dial. 
    As the verification of the successfull execution of each script 
    type has to be performable by each Dial publisher.

    The cost of verifying the PoE of a script determines the payment 
    needed for the submission of the request modifying the token 
    guarded by that script. This is different from the cost and effort 
    needed to move an unmodified script from one time window 
    to another, this last one is constant.
    */ 
    ctl: multihash,

    /* data
    Multihash of the token underlying asset. Not evaluated by the Dial.

    This is held at the discretion of the token controller and is neither
    used nor modified by the Dial.

    The uderlying meaningful content of the token shall be exchanged 
    off chain between transacting parties and do not need to ever 
    be disclosed to the Dial.
    */ 
    data: multihash,

    /*
    List of certificates associated with this token.
    */
    crt: [* certificate],
}

token-hash = {
    /*
    This is the hash of the token representation. Used to build the 
    neighborhood token protocol.
    */
    head: multihash, 

    /* crt
    This is the merkel root of all certificates produced by publishers of
    the given neighborhood. 
    
    The crt field is used to build the neighborhood certification
    protocol.

    As the number of publishers of a neighborhood is known in advanced, 
    if a publisher has not returned a certificate, the corresponding crt entry 
    will still be present, but with the only field iss.

    CBOR cannonicalization rules are also applied to ensure repeatable 
    production of identical input data.

    The list of crt is sorted aaccording to the lexicographical representation 
    of the crt.iss field (identifier of the issuer).
    */
    crt: multihash, 
}

token-ref = {
    /* id
    Token representation as described above.
    */
    token: token,

    /*
    Documentation of the token representation and publication certificates
    */
    hash: token-hash,
}
```

## Declaration
In order to create or modify a token, a participant must send a declaration file to the neighborhood hosting the token identifier.

### Declaration File
The following document displays the top level structure of a declarationn file.
```javascript
{
    /* decl
    Holds the list of declatrations provided to creates or modify tokens. 

    If there is more than one declaration in the list, we assume the file 
    is submitting an arithmetic operation. Following conditions must apply:
    - all tokens and payments addressed in a declaration file must fall in 
    the same neighborhood for the given time window.
    - the arithmetic sum of all tokens minus proccessing fees must be zero.
    - all target _ctl_ entries must be identical. Means all declarations 
    must transact to the same target controller script.
    - each declaration can provide a target _rep_ token to collect the 
    reputation earned from the operation.    
    */
    decl: [+ declaration],

    /* coin
    List of coin declarations for payment

    The coin entry holds the list of coin declarations attached to the file.
    These are independent of the main declarations.

    All coin declarations provided must transact to the same target ctl 
    entry used in the main decclarations, as those are going to be 
    redistributed by the publishers of the target neighborhood.
    */
    coin:[* coin],

    /* pow
    List of PoW declarations for payment

    In the same perspective, the pow entry holds all proof of work 
    provided for the operation.

    All PoW declarations provided must transact to the same target 
    ctl entry used in the main decclaration, as those are going to be 
    redistributed by the publishers of the target neighborhood.

    The proof of work might contain a reputation entry, that helps 
    reduce the amount of computation to be performed by the submitting 
    participant for a work unit. The reputation can transaact to any 
    ctl value. A separated certificate will release this proof of 
    work a the closing of the time window.    
    */
    pow: [* pow],
}
```

### Declaration Entry
A single declaration entry provides (1) , (2) , (3) the new state of the token, and (4) the proof of execution of the controller script.

```javascript
/*
The controller entry is held at the discretion of the controlling participant.

The script is generaly disclosed with the next modification request and shall
not be reused.
*/
controller = {
    /* type
    Type of verification method.
    */
    type: verification-method-type,

    /* vm 
    verification-method.
    
    Issuer public key in the format specified by the given type
    method. Recall that the public key also matches the hash to 
    the given iss field.
    */
    vm: bytes,

    /* nonce
    Random nonce bytes. Limited to 32 bytes.
    */
    nonce: bytes .size 32,
}

declaration = {
    /*
    The current state of the token as known to the Dial
    */
    state: token-state,
    
    /*
    The content of the current controller script. Must match the multihash
    documented in the field token-state.ctl.
    */
    ctl: controller,    

    /*
    New token state. This is used to produce the content of the signature,
    as a proof of execution of the current controller script.
    */
    token: {
        /* id
        The unique identifier of a token. 
        */
        id: token-id, 
        
        /*
        New controller script multihash
        */
        ctl: multihash,

        /*
        New token data multihash
        */
        data: multihash,

        /*
        Work unit to be carried with the token.
        */
        work: int,
        
        /*
        Reputation identifier, where to accumulate earned reputation
         */
        rep: token-id
    },

    /* poe
    Proof of execution.

    e.g. Signature NJlKbI7fqMzkm_PWpfd4jCPdVghxaH3gYw3tH22Ht29xen6...

    For each declaration, the controller must provide a proof of execution 
    of the current controller script of the referenced token. If the token 
    is new, the controller must provide a proof of execution of the public 
    key hash representing the identifier of that token. 

    In the case of a new token, the field state is not present. The field 
    ctl contains the description of the public key producing 
    the token identifier.
    */
    poe: bytes,
}
```

Note that part of the new token state is the merkel root of the current state as found in the protocol of the dial.

## Publishing Process
### Verifying a Declaration
In order to verify a declaration, the publisher must be in possession of:
- the last time window protocol, that aggregates neighborhood protoccols. This protocol is verifiable as it aggregates to the time window hash universally available,
- the protocol of the neighborhood hosting the token in that time window. This protocol is verifiable, as the merkel root is a leaf of the time window protocol,
- the last state of the token. This is provided by the submitting controller as part of the submitted declaration. The token state is verifiable as the merkel root is the part of the token entry forming the leaf of the time window protocol,
- the controller script referenced in that token state. This script is verifiable as the hash is documented in the field _ctl_ of the token state.

After verifying the authenticity of the controller script, the publisher will hash the new token state (field "token") included in the declaration and use the algorithm and hash included in the controller script to verify the proof of execution provided in the field poe.

### Publishing a Declaration
Upon successful verification, the publisher will produce and return a certificate to the submitting participant. The certificate will have the following format:
```javascript
declaration-response = {
    /* id
    Token representation as described above.
    */
   token: token, 

    /* ctl
    Multihash of the controller script.
    */ 
    ctl: multihash,

    /* data
    Multihash of the token underlying asset. Not evaluated by the Dial.
    */ 
    data: multihash,

    /*
    List of certificates associated with this token.
    */
    crt: certificate,
}
```

### No Archivinng of Proofs
Publishers are required to hold the certificates until custodianship on the token is passed over to a new neighborhood. In which case publishers of the new neighborhood can verify the token before acceptance and are then free to forget the certificates.

The dial network does not require publishers to archive document they certify. The network assumes each controller of a token has an economic interest in keeping the last active version of the token declaration and the supporting certificates.

The sole information to be maintained by publishers for the purpose of performing their duties are neighborhood protocols.

