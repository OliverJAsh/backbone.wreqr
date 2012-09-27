# Backbone.Wreqr

A simple message bus for Backbone and Backbone.Marionette

## Downloads And Source

Grab the source from the `src` folder above. Grab the most recent builds
from the links below.

### Standard Builds

* Development: [backbone.wreqr.js](https://raw.github.com/marionettejs/backbone.wreqr/master/lib/backbone.wreqr.js)

* Production: [backbone.wreqr.min.js](https://raw.github.com/marionettejs/backbone.wreqr/master/lib/backbone.wreqr.min.js)

### RequireJS (AMD) Builds

* Development: [backbone.wreqr.js](https://raw.github.com/marionettejs/backbone.wreqr/master/lib/amd/backbone.wreqr.js)

* Production: [backbone.wreqr.min.js](https://raw.github.com/marionettejs/backbone.wreqr/master/lib/amd/backbone.wreqr.min.js)

## Basic Use

### Event Aggregator

An event aggregator implementation. It extends from `Backbone.Events` to
provide the core event handling code in an object that can itself be
extended and instantiated as needed.

```js
var vent = new Backbone.Wreqr.EventAggregator();

vent.on("foo", function(){
  console.log("foo event");
});

vent.trigger("foo");
```

### Commands And Request / Response

Wreqr can be used by instantiating a `Backbone.Wreqr.Commands`
or `Backbone.Wreqr.RequestResponse` object. These objects provide an
`addHandler` method to add a handler for a named request or command.
Commands can then be executed with the `execute` method, and 
request/response can be done through the `request` method.

### Commands

```js
var commands = new Backbone.Wreqr.Commands();

commands.addHandler("foo", function(){
  console.log("the foo command was executed");
});

commands.execute("foo");
```

### Request/Response

```js
var reqres = new Backbone.Wreqr.RequestResponse();

reqres.addHandler("foo", function(){
  return "foo requested. this is the response";
});

var result = reqres.request("foo");
console.log(result);
```

### Removing Handlers

Removing handlers for commands or requests is done the
same way, with the `removeHandler` or `removeAllHandlers`
functions.

```js
reqres.removeHandler("foo");

commands.removeAllHandlers();
```

### Extending Wreqr Objects

The EventAggregator, Commands and RequestResponse objects can all be
extended using Backbone's standard `extend` method.

```js
var MyEventAgg = Backbone.Wreqr.EventAggregator.extend({
  foo: function(){...}
});

var MyCommands = Backbone.Wreqr.Commands.extend({
  foo: function(){...}
});

var MyReqRes = Backbone.Wreqr.RequestResponse.extend({
  foo: function(){...}
});
```

## License

MIT - see [LICENSE.md](https://raw.github.com/marionettejs/backbone.wreqr/master/LICENSE.md)
