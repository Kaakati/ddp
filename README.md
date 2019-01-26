# Flutter DDP - MeteorJS

A Flutter library to connect to Meteor Servers.

## Getting Started

#### Import Library
```
import 'package:ddp/ddp.dart';
```

#### Initilize a client.
```
DdpClient client;

_initMeteorClient() {
    client = DdpClient("meteor", "ws://192.168.1.12:3000/websocket", "meteor");
    client.connect();
    client.addStatusListener((status) {
      if (status == ConnectStatus.connected) {
        connectionStatus = "connected";
        client.subscribe("babies.public", (done) {
          collection = done.owner.collectionByName("Babies");
          updateBabiesNames();
          collection.addUpdateListener(subListener);
        }, []);
        setState(() {});
      }
    });
}
```

#### Initilize a collection
```
Collection collection;
```

#### Method Call
````
client.call("babies.remove", [this.babiesNames[index]["_id"]]);
````

#### findAll
```
collection.findAll()
  ..forEach((String _id, Map document) {
  document["_id"] = _id;
  babiesNames.add(document);
  });
```

For help getting started with Flutter, view our online [documentation](https://flutter.io/).

For help on editing package code, view the [documentation](https://flutter.io/developing-packages/).
