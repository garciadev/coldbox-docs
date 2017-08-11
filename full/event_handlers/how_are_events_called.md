# How are events called?

<img src="/images/request-lifecycle.png">

Events are determined via a special variable that can be sent in via the FORM, URL, or REMOTELY called `event`.  If no event is detected as an incoming variable, the framework will look in the configuration directives for the `DefaultEvent` and use that instead. If you did not set a `DefaultEvent` setting then the framework will use the following [convention](../configuration/conventions.md) for you: `main.index`

> **Hint** : You can even change the `event` variable name by updating the `EventName` setting in your `coldbox` configuration directive.

Please note that ColdBox supports both normal variable routing and [URL mapping routing](../routing/index.md), usually referred to as pretty URLs.

## Event Syntax
In order to call them you will use the following event syntax notation format:

```js
event={module:}{package.}{handler}{.action}
```

* **no event** : Default event by convention is `main.index`
* **event={handler}** : Default action method by convention is `index()`
* **event={handler}.{action}** : Explicit handler + action method
* **event={package}.{handler}.{action}** : Packaged notation
* **event={module}:{package}.{handler}.{action}** : Module Notation (See [ColdBox Modules](../modules/index.md))

This looks very similar to a java or CFC method call, example: String.getLength(), but without the parentheses. Once the event variable is set and detected by the framework, the framework will tokenize the event string to retrieve the CFC and action call to validate it against the internal registry of registered events. It then continues to instantiate the event handler CFC or retrieve it from cache,  finally executing the event handler's action method.

**Examples**

```
// Call the users.cfc index() method
index.cfm?event=users.index
// Call the users.cfc index() method implicitly
index.cfm?event=users
// Call the users.cfc index() method via URL mappings
index.cfm/users/index
// Call the users.cfc index() method implicitly via URL mappings
index.cfm/users
```
