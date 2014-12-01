Overview
===

`%eyre` is our webserver. 


HTTP Methods
===

`GET`
`gog` 
`https://[ship-name].urbit.org/gog/[service]`
Owner requesting a page on her own Urbit.
`gig`
`https://[ship-name].urbit.org/gig/[user-name]/[service]`
Another user requesting a page on a foreign Urbit.

`goe`
`https://[ship-name].urbit.org/goe/[service]/[port]/[stream]/[sequence]`
`https://[ship-name].urbit.org/goe/[service]/[port]/[stream]/[sequence].json`
Pulls a specific response to her subscription on her own Urbit.
`gie`
`https://[ship-name].urbit.org/gie/[user-name]/[service]/[port]/[stream]/[sequence]`
`https://[ship-name].urbit.org/gie/[user-name]/[service]/[port]/[stream]/[sequence].json`
Pulls a specific response to her subscription on a foreign Urbit.

`PUT`
`tos`
`https://[ship-name].urbit.org/tos/[service]/[port]/[stream]/[path]`
`{oryx: [string]}`
Initiate a subscription on her own Urbit.
`tis`
`https://[ship-name].urbit.org/tis/[user-name]/[service]/[port]/[stream]/[path]`
`{oryx: [string]}`
Initiate a subscription on a foreign Urbit.

`tom`
`https://[ship-name].urbit.org/tom/[service]/[port]/[sequence]`
`{oryx: [string], xyro: [json]}`
Send a message to her Urbit with sequence number `[sequence]`.
`tim`
`https://[ship-name].urbit.org/tim/[user-name]/[service]/[port]/[sequence]`
`{oryx: [string], xyro: [json]}`
Send a message to a foreign Urbit with sequence number `[sequence]`.

`tou`
`https://[ship-name].urbit.org/tou/[service]/[port]/[stream]`
Unsubscribe from stream `[stream]` on her Urbit.
`tiu`
`https://[ship-name].urbit.org/tiu/[user-name]/[service]/[port]/[stream]`
Unsubscribe from stream `[stream]` on a foreign Urbit.


urb.js
===