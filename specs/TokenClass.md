# Token Class
A token class is a token describing a class of tokens. It also provides a schema, control rules and a unit of account for all tokens of that class. Each token resp. declaration in the dial network is instantiated from a token class. Event fudamental network rules are defined into token classes. A genesis packet provides initial files used to bootstrap the network.

# Declaration
A declaration is the fundamental unit of expression

# Control Rules

## Network Control Rule
Declaration controlled by the network can be changed using the network control rules. Network controll rules themself are declared as token and managed by the network. A typical network control rule contains following parameters:
- reputation of each voting participant at a defined reference time window
- quantity of votes in percentage of voting participants
- time frame to collect the vote in number of time windows from the reference time window

## Organization Control Rules
Beside network control rules, organization control rules can allow issuer of token classes to define conditions under which the token class can be modified.

## Sample Declaration
The folowing declaration describes the look of a network defined token class.

```json
{
    "nid":"zEruWfhngbEc16jmpZBHSk4Tx872CHDWXeNsDJfL8yHo6",
    "dec": [
        {
            "type": "Class",
            "id": "zEruWfhngbEc16jmpZBHSk4Tx872CHDWXeNsDJfL8yHo6",
            "schema": "json schema of tokens of this class",
            "controller":{
                "id": "zEruWfhngbEc16jmpZBHSk4Tx872CHDWXeNsDJfL8yHo6",
                "type": "network",
                "reputation-unit":"time-window",
                "reputation-count": "8640",
                "votes-percent":"51",
                "time-frame":"4320"
            }
        }
    ],
    "proof":[
        "signature of all genesis participants."
    ]
}
```

The reputation count 

