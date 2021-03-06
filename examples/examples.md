All examples below require the Eventerface module:

``` js
var eventerface = require('eventerface');
```

# LOCAL EVENTED INTERFACES

## NAMESPACES

### Example 01: One emitter, same listener

The following code does not print "Hey!" as is might be expected. That is because Eventerface emitters do not listen to their own events:

``` js
var emitter = eventerface.emitter();

emitter.on('hey', function () {
    console.log('Hey!');
});

emitter.emit('hey');
```

### Example 02: One emitter, different listener

The proper way to use 'eventerface' emitters is to listen to events, not to particular event emitters:

``` js
var emitter = eventerface.emitter();
var listener = eventerface.emitter();

listener.on('hey', function () {
    console.log('"hey" event fired listener!');
});

emitter.emit('hey');
```

In the previous code, 'listener' knows nothing about 'emitter', only about the 'hey' event.


### Example 03: One listener, many emitters

Since a listener only knows about events and not where they come from, they can listen to the same event even when its emitted by different emitters:

``` js
var emitter1 = eventerface.emitter();
var emitter2 = eventerface.emitter();
var listener = eventerface.emitter();

listener.on('hey', function () {
    console.log('"hey" event fired listener!');     // Prints twice
});

emitter1.emit('hey');
emitter2.emit('hey');
```

### Example 04: One emitter, many listeners

Likewise, since an emitter does not know who is going to listen to its events, many listeners can listen to the same event:

``` js
var emitter = eventerface.emitter();

var listener1 = eventerface.emitter();
var listener2 = eventerface.emitter();
var listener3 = eventerface.emitter();

listener1.on('hey', function () {
    console.log('"Hey" event fired listener #1!');
});
listener2.on('hey', function () {
    console.log('"Hey" event fired listener #2!');
});
listener3.on('hey', function () {
    console.log('"Hey" event fired listener #3!');
});

emitter.emit('hey');
```

The output of the previous code should be:
``` js
'"hey" event fired listener #1!'
'"hey" event fired listener #2!'
'"hey" event fired listener #3!'
```

### Example 05: Many emitters, many listeners

Now, combining the two previous examples, it is also possible to have a set of listeners listening to a particular event that is emitted by different emitters:

``` js
var emitter1 = eventerface.emitter();
var emitter2 = eventerface.emitter();

var listener1 = eventerface.emitter();
var listener2 = eventerface.emitter();
var listener3 = eventerface.emitter();

listener1.on('hey', function () {
    console.log('"hey" event fired listener #1!');
});
listener2.on('hey', function () {
    console.log('"hey" event fired listener #2!');
});
listener3.on('hey', function () {
    console.log('"hey" event fired listener #3!');
});

emitter1.emit('hey');

setTimeout(function () { 
    emitter2.emit('hey');
}, 1000);
```

The previous code should print three lines, and the same three lines again after 1000 ms: 
``` js
    '"hey" event fired listener #1!'
    '"hey" event fired listener #2!'
    '"hey" event fired listener #3!'
    '"hey" event fired listener #1!'  // 1000 ms later
    '"hey" event fired listener #2!'  // 1000 ms later
    '"hey" event fired listener #3!'  // 1000 ms later
```

# GLOBAL EVENTED INTERFACES

## NAMESPACES

## CHANNELS


# DISTRIBUTED EVENTED INTERFACES

## CHANNELS

## STATIONS

## WEB APIs
