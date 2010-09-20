SandboxJS
=========
### Run JavaScript code in a Sandbox for the browser

This script offers a very simple interface for JavaScript "Sandboxes".
Underneath, it uses the [magic power of `iframe`s][DeanEdwards] to create
new execution scopes for JavaScript to be evaluated inside of.


API
---

    new Sandbox() -> sandbox

Creates and returns new `Sandbox` instance.

    sandbox.global -> Global

The `global` scope of the sandbox instance. This is a convenient way
to share instances of `Object`s across scopes, or prepare the sandbox
environment with properties that scripts can use.

    sandbox.eval(jsStr:String) -> ?

Calls `eval` on the given `String` inside the sandbox. Variables declared
inside the sandbox won't be accessible globally, and global variables won't
be visible inside the sandbox. The result of the `eval` is returned.

    sandbox.load(filename:String [, callback:Function])

Loads the JavaScript file `filename` and executes it into the sandbox. `callback`
is an optional function that gets invoked when the file has finished loading and
being evaluated, or an error occurs (like the file was not found).

    sandbox.loadSync(filename:String)

Synchronously loads the JavaScript file `filename` and executes it into the
sandbox. If there is an error while loading (like the file was not found),
then this function will throw. This function is highly discouraged, since synchronous network
activity blocks the browser, making it appear to _freeze_! Also, underneath
this function uses `XMLHttpRequest`s, which are limited by the [Same Origin Policy][SameOriginPolicy].
In other words, this function will ONLY work with files from the SAME DOMAIN.

[DeanEdwards]: http://dean.edwards.name/weblog/2006/11/sandbox/
[SameOriginPolicy]: http://en.wikipedia.org/wiki/Same_origin_policy