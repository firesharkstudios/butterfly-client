# Butterfly.Client ![Butterfly Logo](https://raw.githubusercontent.com/firesharkstudios/Butterfly/master/img/logo-40x40.png) 

> Clients (javascript and .NET) that can subscribe real-time updates from a [Butterfly.Web](https://github.com/firesharkstudios/butterfly-web) server in C#

## Getting Started

### Install from Source Code

```git clone https://github.com/firesharkstudios/butterfly-client```

## Butterfly Client

### Overview

Butterfly Client is a javascript library that allows...

- Maintaining a connection to your server to receive subscription messages
- Mapping subscription messages received to synchronize local javascript arrays with the server

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

An *WebSocketChannelClient* instance maintains a connection to your server to receive subscription messages and an *ArrayDataEventHandler* instance maps the subscription messages to local javascript arrays to keep these local javascript arrays synchronized with your server...

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

# Wishlist

Here is an unprioritized wish list going forward...

## More Databases

Add support for the following databases...

- Mongo DB

## More Client Bindings

Add support for the following clients...

- React
- React Native
- Angular
- UWP
- WinForms
- Android
- Flutter
- Swift

## More Examples

Add examples that show...

- Getting real-time data from a  *Raspberry Pi*

## Contributing

If you'd like to contribute, please fork the repository and use a feature
branch. Pull requests are warmly welcome.

## Licensing

The code is licensed under the [Mozilla Public License 2.0](http://mozilla.org/MPL/2.0/).  
