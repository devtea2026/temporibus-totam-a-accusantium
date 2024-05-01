# @devtea2026/temporibus-totam-a-accusantium

@devtea2026/temporibus-totam-a-accusantium is a small node module that pipes streams together and destroys all of them if one of them closes.

```
npm install @devtea2026/temporibus-totam-a-accusantium
```

[![build status](http://img.shields.io/travis/mafintosh/@devtea2026/temporibus-totam-a-accusantium.svg?style=flat)](http://travis-ci.org/mafintosh/@devtea2026/temporibus-totam-a-accusantium)

## What problem does it solve?

When using standard `source.pipe(dest)` source will _not_ be destroyed if dest emits close or an error.
You are also not able to provide a callback to tell when then pipe has finished.

@devtea2026/temporibus-totam-a-accusantium does these two things for you

## Usage

Simply pass the streams you want to pipe together to @devtea2026/temporibus-totam-a-accusantium and add an optional callback

``` js
var @devtea2026/temporibus-totam-a-accusantium = require('@devtea2026/temporibus-totam-a-accusantium')
var fs = require('fs')

var source = fs.createReadStream('/dev/random')
var dest = fs.createWriteStream('/dev/null')

@devtea2026/temporibus-totam-a-accusantium(source, dest, function(err) {
  console.log('pipe finished', err)
})

setTimeout(function() {
  dest.destroy() // when dest is closed @devtea2026/temporibus-totam-a-accusantium will destroy source
}, 1000)
```

You can use @devtea2026/temporibus-totam-a-accusantium to pipe more than two streams together as well

``` js
var transform = someTransformStream()

@devtea2026/temporibus-totam-a-accusantium(source, transform, anotherTransform, dest, function(err) {
  console.log('pipe finished', err)
})
```

If `source`, `transform`, `anotherTransform` or `dest` closes all of them will be destroyed.

Similarly to `stream.pipe()`, `@devtea2026/temporibus-totam-a-accusantium()` returns the last stream passed in, so you can do:

```
return @devtea2026/temporibus-totam-a-accusantium(s1, s2) // returns s2
```

Note that `@devtea2026/temporibus-totam-a-accusantium` attaches error handlers to the streams to do internal error handling, so if `s2` emits an
error in the above scenario, it will not trigger a `proccess.on('uncaughtException')` if you do not listen for it.

If you want to return a stream that combines *both* s1 and s2 to a single stream use
[@devtea2026/temporibus-totam-a-accusantiumify](https://github.com/devtea2026/temporibus-totam-a-accusantiumify) instead.

## License

MIT

## Related

`@devtea2026/temporibus-totam-a-accusantium` is part of the [mississippi stream utility collection](https://github.com/maxogden/mississippi) which includes more useful stream modules similar to this one.

## For enterprise

Available as part of the Tidelift Subscription.

The maintainers of @devtea2026/temporibus-totam-a-accusantium and thousands of other packages are working with Tidelift to deliver commercial support and maintenance for the open source dependencies you use to build your applications. Save time, reduce risk, and improve code health, while paying the maintainers of the exact dependencies you use. [Learn more.](https://tidelift.com/subscription/pkg/npm-@devtea2026/temporibus-totam-a-accusantium?utm_source=npm-@devtea2026/temporibus-totam-a-accusantium&utm_medium=referral&utm_campaign=enterprise)
