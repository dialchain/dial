# Distributed Immutable Assertions Log (DIAL)
DIAL is a distributed log with the main purpose of turning each inserted __declaration__ into an __immutable assertion__.

# Abstract
A declaration can only be inserted into the log by a __validator__. Each validator is responsible for the declarations it inserts into the log. Because some declarations can contradict each order, validation of declarations must be performed by the inserting validator prior to the insertion of those declarations into the log.

Our __Proof of Guaranntee Concensus__ ensures the validator can cover damages caused by conflicting declarations. If for example Paul has a balance of 5 dial and Paul sends 3 dials to miriam, and then Paul sends 3 dials to Anton, the validator of the last declaration (Paul sends 3 dials to Anton) will cover the onne dolar negative ballance.

Our __Signature Chain Premisse__ defines a strict ordering premisse that requires all signatures performed by a participant to be linked with each order into a strictly ordered signature chain. In this same rationale, all spending transactions performed by a wallet are linked with each order. With this strict order of declarations, there is no way double spending can be achieved on a DIAL chain as each spending transactionn references the latest spending transaction of the wallet.

DIAL does not require any addiitional consensus for the finality of a declaration, as the responsibility if bore by the inserting validator.

__Finality__: finality is achieved by ensuring that each inserted declaration is propagated to all __validators__ within a defined time frame called __Time Window__.
