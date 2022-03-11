# Asset
An asset is a sort of [token](Token.md) used to represent value. The value can be the mapping of an external asset or the representation of a native asset like the dial coin.

## Representation
```json
{
    "type": "Declaration",
    "declaration": [
        {
            "type": "Asset",
            "id": "unnique PublicKeyHash-MultiCodec",
            "controller": "another PublicKeyHash-MultiCodec",
            "exp": "time-utc-sec",
            "class": "dial",
            "value": "10"
        }
    ]
}
```

## Asset Aggregation
Assets of the same class can be aggreated if all aggregate fall in the same time window at the moment of aggregation. For this to happen, the holder of those aggregates has to be lucky to hold asset that are in the same neighborhood during the target time window. An aggregation declation can then allow validators of that time window to certify the declaration and thereby terminate the original asset.
