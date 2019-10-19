# Butterfly.Client ![Butterfly Logo](https://raw.githubusercontent.com/firesharkstudios/Butterfly/master/img/logo-40x40.png) 

> Clients (javascript and .NET) that can subscribe real-time updates from a [Butterfly.Web](https://github.com/firesharkstudios/butterfly-web) server in C#

# Install from Source Code

```git clone https://github.com/firesharkstudios/butterfly-client```

# Butterfly.Client.Web

## Overview

*Butterfly.Client.Web* is a plain vanilla javascript library that works 
with any framework and allows subscribing to channels in a [Butterfly.Web](https://github.com/firesharkstudios/butterfly-web) 
server to keep local javascript arrays automatically updated.

The easiest way to install Butterfly Client is with npm...

```
npm install butterfly-client
```

You can then include the Butterfly Client with a script import like...

```html
<script src="./node_modules/butterfly-client/lib/butterfly-client.js"></script>
```

Or include the classes you need with an appropriate ES6 import like...

```
import { ArrayDataEventHandler, WebSocketChannelClient } from 'butterfly-client'
```

### Example

An *WebSocketChannelClient* instance maintains a connection to your 
server to receive subscription messages and an *ArrayDataEventHandler* 
instance maps the received messages to local javascript arrays to keep 
these local javascript arrays synchronized with your server...

```js
let channelClient = new WebSocketChannelClient({
    url: `ws://localhost:8080/ws`,
    onStateChange(newState) {
        console.debug(`newState=${newState}`);
    },
    onSubscriptionsUpdated(newSubscriptions) {
        console.debug(`newSubscriptions=${newSubscriptions}`);
    },
});
channelClient.connect('Authorization : Bearer xyz');

let list1 = [];
let list2 = [];
channelClient.subscribe(
    channel: 'todos',
    handler: new ArrayDataEventHandler({
        channel: 'my-channel',
        vars: {
            someInfo: 'Some Info',
        },
        arrayMapping: {
            tableName1: list1,
            tableName2: list2,
        }
    })
);
```

See the examples at [Butterfly.Server](https://github.com/firesharkstudios/butterfly-server) on how to use the *butterfly-client* client to communicate with a [Butterfly.Web](https://github.com/firesharkstudios/butterfly-web) server.

## Contributing

If you'd like to contribute, please fork the repository and use a feature
branch. Pull requests are warmly welcome.

## Licensing

The code is licensed under the [Mozilla Public License 2.0](http://mozilla.org/MPL/2.0/).  
