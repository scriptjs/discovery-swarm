# discovery-swarm

A network swarm that uses [discovery-channel](https://github.com/maxogden/discovery-channel) to find and connect to peers.

This module implements peer connection state and builds on discovery-channel which implements peer discovery. This uses TCP sockets by default and has experimental support for UTP.

```
npm install discovery-swarm
```

[![build status](http://img.shields.io/travis/mafintosh/discovery-swarm.svg?style=flat)](http://travis-ci.org/mafintosh/discovery-swarm)

## Usage

``` js
var swarm = require('discovery-swarm')

var sw = swarm()

sw.listen(1000)
sw.add('ubuntu-14.04') // can be any id/name/hash

sw.on('connection', function (connection) {
  console.log('found + connected to peer')
})
```

## API

#### `var sw = swarm()`

Create a new swarm

#### `sw.add(key)`

Add `key` (usually a name, hash or id, must be a **Buffer** or a **string**) to the list of keys to use to discover and connect to peers. After adding will immediately search for peers advertising this key, and re-announce on a timer.

#### `sw.remove(key)`

Remove `key` from the list of keys

#### `sw.connecting`

Number of peers we are trying to connect to

#### `sw.queued`

Number of peers discovered but not connected to yet

#### `sw.connections`

List of active connections to other peers

#### `sw.on('connection', connection)`

Emitted when you connect to another peer

#### `sw.listen(port)`

Listen on a specific port. Should be called before add

## License

MIT
