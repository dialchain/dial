
# Excourse Token Management
A token management system can maintain a list of tokens. Each token can have a controller property that indicates who can modify the token. The following picture displays a database table in which the state of a single token is tracked.

![Token Management](./img/tokenMgt-1.png)

Lines bellow help understand the table:
- The column _Time_ is displayed to show that those modifications do not occur in parallel.  
- The column _TokenID_ holds a unique identifier for the token. This identifier is also a public key hash. Using a public key as identifier helps enforce proof of possession (PoP) of the corresponding private key at token creation time, thus preventing the presentation of two creation requests with the same token identifier.
- The columnn _CTL hash_ displays the hash of the public key that guards the token. This is the key used to enforce legitimate modification of the token.
- The column _Exp_ allow the maintenance of a expiration date. Token will be retired upon reaching that date unless extended by the token controller.
- The column _Token Hash_ is an information not relevant for the management of the management of the token, but might help parties ensure integrity of the content of the token.
- The column _Value_ extends the table with a simple arithmetic that allows the aggregation of tokens of the same value type.
- The column _Proof_ documents the PoP used to legitimate modification on the token. To modify a token, the controller must prove possession of the private key matching the public key found in field _CTL-hash_. This means the controller must sign the modification request with the private key matching the public key found in the _CTL-hash_ field. That signature is displayed in this _Proof_ column.

Although the simplest implementation of this token management system can be provided by a centralized database server, the resulting centralized architecture will not be suitable for the deployment of scalable, open, permissionless, and censorship resistant, nano payment capable API networks.

This last remark pushes toward the design of an equivalent system but distributed, open and permissionless.
