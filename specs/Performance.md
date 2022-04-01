# Performance
Performance is the act of providing a service in the Dial network. Well known services are:
- Relay Service provided by __Router Nodes__
- Gateway Service provided by __Gateway Nodes__
- Data Service provided by __Data Nodes__
- Publishing Service provided by __Publisher Nodes__

As we can notice in the naming, only Relay and Gateway services require permanent presence in the network. Those need static ip addresses so they can be permanently reachable by other network participants.

Both data and publisher nodes can rely on the the service of gateway nodes to provide for reachability.

Because of the permissionless nature of the DialChain, it is difficult to tell when a service provider joins or leaves the network. Therefore, the Dial requires service providers to pre-announce readyness for performance. We call this announcement a __Performance Declaration__. Performannce declarations are binding. E.g. in order for a service provider to perform in time window __tw__, it needs to publish its readyness in time window __tw-1__, before the intermediary neighborhoods protocol is produced. This concept is essential for the stability of the network, as a participant consuming a service must rely on commited providers being available.

The following file shows the structure of a performance declaration:

```json
{
    "decl": [{
        "state": {
            "id": "token unnique publicKey multihash",
            "ctl": "controller script multihash",
            "wrk": 1799,
            "rep": 1,
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
        "target":{
            "id": "unnique publicKey multihash",
            "ctl": "new controller script multihash",
            "hash": "new token data multihash",
            "wrk":1100,
            "rep": "reputation identifier, where to accumulate earned reputation",
            "service": [
                {
                    "type": "publish",
                    "id": "z597FwdoYuc71oKc1wvR13o8D7Sdx4u6W3sySp1pVTRXU#pub-0",
                    "endpoint": "https://node0.first-dial.io/z597FwdoYuc71oKc1wvR13o8D7Sdx4u6W3sySp1pVTRXU/publish"
                },
                {
                    "type": "publish",
                    "id": "z597FwdoYuc71oKc1wvR13o8D7Sdx4u6W3sySp1pVTRXU#pub-1",
                    "endpoint": "https://node23.all-cloud.net/z597FwdoYuc71oKc1wvR13o8D7Sdx4u6W3sySp1pVTRXU/publish"
                },
                {
                    "type": "publish",
                    "id": "z597FwdoYuc71oKc1wvR13o8D7Sdx4u6W3sySp1pVTRXU#pub-2",
                    "endpoint": "https://www1.empire.us/z597FwdoYuc71oKc1wvR13o8D7Sdx4u6W3sySp1pVTRXU/publish"
                }
            ]
        },
        "poe": "signature e.g. NJlKbI7fqMzkm_PWpfd4jCPdVghxaH3gYw3tH22Ht29xen6...",
    }],
    "coin":["List of coin declarations for payment"],
    "pow": ["List of PoW declarations for payment"],
}
```
The resulting service record in the dial will have the following conntent.
```json
{
    "id": "unique publicKey multihash",
    "mod": 20220323121835,
    "wrk": 1099,
    "rep": 1,
    "mr": "merkel root multihash",
    "service": [
        {
            "type": "publish",
            "id": "z597FwdoYuc71oKc1wvR13o8D7Sdx4u6W3sySp1pVTRXU#pub-0",
            "endpoint": "https://node0.first-dial.io/z597FwdoYuc71oKc1wvR13o8D7Sdx4u6W3sySp1pVTRXU/publish"
        },
        {
            "type": "publish",
            "id": "z597FwdoYuc71oKc1wvR13o8D7Sdx4u6W3sySp1pVTRXU#pub-1",
            "endpoint": "https://node23.all-cloud.net/z597FwdoYuc71oKc1wvR13o8D7Sdx4u6W3sySp1pVTRXU/publish"
        },
        {
            "type": "publish",
            "id": "z597FwdoYuc71oKc1wvR13o8D7Sdx4u6W3sySp1pVTRXU#pub-2",
            "endpoint": "https://www1.empire.us/z597FwdoYuc71oKc1wvR13o8D7Sdx4u6W3sySp1pVTRXU/publish"
        }
    ]
}
```

## Service Records
The performance declaration also exposes service records, associated endpoints and corresponding authentication credentials (assertion method). A single service record has the following architecture:
```json
{
    "type": "publish",
    "id": "z597FwdoYuc71oKc1wvR13o8D7Sdx4u6W3sySp1pVTRXU#pub-2",
    "endpoint": "https://www1.empire.us/z597FwdoYuc71oKc1wvR13o8D7Sdx4u6W3sySp1pVTRXU/publish"
}
```

### type
Indicate the type of service as decribed in the Dial type registry.

### Endpoint
This is the network endpoint receiving service calls on behalf of the participant. The reason for registering many service endpoints is to increase availability. Those endpoints might be operated by gateway services independent of the registering service provider.

### Identifier (id)
The identifier exposes the hash of a public key. This can be considered a controller script and used by participant to transact with the service provider.
