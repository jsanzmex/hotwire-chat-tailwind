# Hotwire Chat

Demos Hotwire and Stimulus with a simple real-time chat application.

To test the demo run `bin/dev` then browse to:

http://127.0.0.1:3000/rooms

# About Stimulus

The new Rails-Stimulus integration shim ships with an autoloader for your controllers. This is done within **import maps** ordered by ES module shim, and the _unprocess?_ ES6 controller code that's loaded by the browser directly via ESM. You can of course continue to use Stimulus with your existing JS bundler and transpiler, but this gives you a taste of how far we are able to get with native browser controls now.

# Naming Stimulus Controllers

If the Stimulus Controller is named `reset_form_controller.js`, then you shpuld invoke it like this in your Rails views:

```ruby
controller: "reset-form", action: "turbo:submit-end->reset-form#reset
```

# About Redis and ActionCable

Action Cable is no longer a gem you have to add, it is already included in every Rails project.
So in order to leverage the power of Action Cable in your project you just have to make sure Redis is up and running.
You can esasily spin-up a Redis instance with docker just run this command:

```sh
docker run --name some-redis -p 6379:6379 --rm redis
```

The advantage of above's command is that the Redis instance is stoppend and removed on closing/stopping the terminal.

# What are Shims and Polyfills

## Shim

If you are familiar with the adapter pattern, then you know what a shim is. Shims intercept API calls and create an abstract layer between the caller and the target. Typically shims are used for backward compatibility. For instance the es5-shim npm package will let you write ECMAScript 5 (ES5) syntax and not care if the browser is running ES5 or not. Take Date.now as an example. This is a new function in ES5 where the syntax in ES3 would be new Date().getTime(). If you use the es5-shim you can write Date.now and if the browser you’re running in supports ES5 it will just run. However, if the browser is running the ES3 engine es5-shim will intercept the call to Date.now and just return new Date().getTime() instead. This interception is called shimming. The relevant source code from es5-shim looks like this:

```js
if (!Date.now) {
    Date.now = function now() {
        return new Date().getTime();
    };
}
```

## Polyfill

Polyfilling is really just a specialized version of shimming. Polyfill is about implementing missing features in an API, whereas a shim wouldn’t necessarily be as much about implementing missing features as it is about correcting features. I know these seems overly vague, but where shims are used as a more broader term, polyfill is used to describe shims that provide backward compatibility for older browsers. So while shims are used for covering up old sins, polyfills are used for bringing future enhancements back in time. As an example there is no support for sessionStorage in IE7, but the polyfill in the sessionstorage npm package will add this feature in IE7 (and older) by using techniques like storing data in the name property of the window or by using cookies.
 No newline at end of file
