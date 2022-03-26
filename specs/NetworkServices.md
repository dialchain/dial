# Network Services
One goal of the Dial is to achieve the broadest possible decentralization. This can only be achieved by keeping the Dial simple, such as to allow for common devices like mobile phones or IOT devices to play the publisher role and therefore participate to the Dial economy.

Dial network service providers deploy simple communication infrastructure components, that will allow network limited devices to act as first class citizen in the Dial network.

Dial network services are simple enougth to allow for consumer grade home based computers with static ip addresses to be deployed and operated as Dial network services. The operation of a Dial network component shall allow the owner to cover all incured costs. The service shall be simple enougth not to require special computer skills for the operation of network nodes.

## Relay Service
A relay service allows parties to exchange point to point messages with each other. Each message sent to a relay is accopanied with a payment token. The request for reading that message is also accompanied with a token.

If two different messages are sent to the same relay address, the second message overrides the first message.

A relay is open, permissionless and offers 3 methods:
- POST(url, data, exp, payment): allowing the caller to deposit a message for pickup with the relay.
- GET(url, payment): allowing the caller to collect a message
- DEL(url): allowing the removal of a message no longer needed.

The payment amount is dependent on the size of the message and expiration of the message. The Dial defines standard packet sizes and prices for the relay service.

## Gateway Service
A gateway service allows a Dial participant to expose a permanent endpoint at which it can receive messages. Therefore, a single gateway address holds a queue of messages. The deposition and the collection of a message from a gateway endpoint is payable. A gateway supports following operations:
- POST(url, data, exp, payment): allowing the caller to deposit a message for pickup to the gateway endpoint with the address url.
- GET(url, payment, PoP): allowing the caller to collect and delete the next message in the queue
The get request to a gateway address provides a proof of possession of the endpoint url.

## Broadcast Service
A broadcast service allows a Dial participant to expose a url where authenticated information can be pushed for the rest of network participants. A broadcast endpoint generally holds one file that is updated by the controller of that broadcast address. The deposition and the collection of a messaage from a broadcast endpoint is payable. A broadcast supports following operations:
- POST(url, data, pop, payment-1): allowing a participant to update the file held at the endpoint og a broadcast address.
- GET(url, payment-2): allowing the caller to collect the file
- DEL(url, pop): allowing the removal of a message no longer needed
The broadcast url contains public key hash. Posting or deleting the file at that url requires the proof of possession of the corresponding private key. Each file posted at that location is also signed with the corresponding private key


## Service Registration
Network service providers must register their services with the Dial by submitting corresponding performance declarations to the Dial. Following the same rationales as explained for publishers, a network service provider must register the performance declaration for __tw__ in __tw-1__ before the producction of the INP. A performance declaration is binding. In the same logic of publishers, coin earned in a time window can only be rediemed in the subsequent time window, after presentation of the proof of performance.