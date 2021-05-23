# Distributed Immutable Assertions Log (DIAL)
The DialChain is a distributed log with the main purpose of turning each inserted __declaration__ into an __immutable assertion__.

# Abstract
A declaration can only be inserted into the log by a __validator__. Each validator is responsible for declarations it inserts into the log. But because the effect of a declaration can conflict with the effect of another declaration, validation of declarations must be performed prior to their insertion into the log.

Our __Proof of Guaranntee Consensus__ ensures that the validator, if required, can cover damages caused by the insertion of the conflicting declaration.

Further, __Finality__ is achieved by ensuring that each inserted declaration is propagated to all __validators__ within a defined time frame called __Time Window__. All declarations of a closed time window are final, immutable assertions and non conflicting with each order.