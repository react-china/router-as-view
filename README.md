
Router View for React
----

> Location bar is a view of store

This project is based on `react` and `immutable-js`.

Demo http://router-view.mvc-works.org/

### Core ideas

In time travelling debugger, router is not controlled.
So I suggest location bar being regarded as a view of store.

### Usage

```
npm i --save router-view
```

```coffee
Addressbar = require 'router-view'
utilPath = require 'router-view/lib/util/path'

rules = [
  ['home', '/']
  ['demo', '/demo']
  ['skip', '/skip/~']
  ['team', 'team/:teamId']
  ['room', 'team/:teamId/room/:roomId']
  ['404', '~']
]

oldAddress = "#{location.pathname}#{location.search}"
# oldAddress = location.hash.substr(1)
router = utilPath.getCurrentInfo(utilPath.expandRoutes(rules), oldAddress)
store = store.set 'router', router

Addressbar
  route: store.get('router')
  rules: routes
  onPopstate: (info) ->
  inHash: false
```

`~` refers to "any path" in this library. And in store the route information is like:

```coffee
name: 'room'
data:
  teamId: '12'
  roomId: '34'
query:
  isPrivate: 'true'
```

Parameters and querystrings are supported. Get this from store and render the page.

### License

MIT
