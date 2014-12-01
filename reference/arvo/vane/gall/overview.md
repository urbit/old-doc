Overview
===

`%gall` services store and distribute data. 


Service Models
===

`%rush`

`%rust`

`%mean`

`%nice`


Service Gates
===

`++poke`
Handles incoming messages. Most commonly with an associated `%logo`. 
For example `++poke-json` handles an incoming JSON request from `%eyre`.

`++peer`
Handles incoming subscriptions. 

`++pull`
Handles dropping subscribers.

`++pour`
Handles responses to `%pass` moves.

`++park`
Save state on update.

`++prep`
Load state on update.