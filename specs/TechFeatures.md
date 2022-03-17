
# Core Characteristics
## Instant Finality
Instant Finality is provided as the ENP defines a small enougth set of publishers (11 in THost and 11 in NHost) to take care of each token during the open time window. A participant being presented 6 PCerts can be assured that the state change of the token will be part of the time window protocol and therefore assume finality.

Double spending can only occur with the complicity of the majority of publishers in the THost and NHost, meaning about 6 + 6, 12 publishers. 

A single party must have enougth participants to achieve a situation where it controls the majority of publishers of a THost and NHost.

## Organic Scalability
Organic Scalability is provided as (1) the Dial is designed to allow each participant (e.g mobile phone) to perform the duty of a publisher, (2) growing number of end users leads to a growing number of publishers, (3) growing number of publishers leads to a growinng number of neighborhoods.

## Throughput
The Dial does not know the concept of a block size. The Diaal scales with the number of registered publishers. As there is a maximum number of token processable by a neighborhood, the Dial expect more publishers to join as the number of token maintained grows and some publishers to leave as the publication insentive drops due decreasing number of tokens.

## DETerministic Ordering of EXecution (DETOX)
DETOX is essential for the adoption of blockchain by other industries. As the Dial does nto have blocks, front running a declaraation will require the complicity of all publishers of THost.

## Spam Resistance
Spam Resistance is provided despite the open and permissionless character of the Dial. All service operation are payable. Payment ist performed either using existing acquired coins or proof of work done to generate aa coin. In both cases the price is set such aas to make it unatttractive for a participant to generate sapmy declarations.

## Constrained Tokens
The Dial provide the network with the possibility of constraining the exchange of some tokens. (1) the __authenticated withness protocol (AuthWith)__ requires the (new) controller of a token to provide an off chain proof of identification, while staying anonymous on chain, (2) __time lock contracts__ will delay the time to change control of the enclosing token, (3) __key locked contracts__ will allow the designated participant to control the enclosing token if it presents the proof of possession of a key, (4) combination thereof might also be applied to constrain token disposition.
