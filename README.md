# Distributed Immutable Assertions Log (DIAL)
The DialChain is a distributed log with the main purpose of turning each inserted __declaration__ into an __immutable assertion__. The DialChain is unique in its kind of offering an __unlimited block size__ and a __deterministic ordering and execution protocol__ (__DETOX__).

# Abstract
A declaration can only be inserted into the log by a __validator__. Each validator is responsible for declarations it inserts into the log. But because the effect of a declaration can conflicts with the effect of another declaration, validation of declarations must be performed prior to their insertion into the DialChain log.

Our __Proof of Guarantee Consensus__ ensures that the validator, if required, can cover damages caused by the insertion of a conflicting declaration.

Further, __Finality__ is achieved by ensuring that each inserted declaration is propagated to all __validators__ within a defined time frame called __Time Window__. All declarations of a closed time window are final and non-conflicting with each order. Finality turns each declaration into an __immutable assertion__.

The DialChain is unique in its kind of offering an unlimited block size and a deterministic ordering and execution protocol. This might sound negligeable at first but will later be proven essential for the sustainability of blockchain networks and the adoption of blockchain technology by other industries.