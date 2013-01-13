jRespond: Responsive JS & CSS
=============================

Available [on GitHub](https://github.com/dcporter/jrespond).

jRespond is a jQuery plugin for implementing the JavaScript side of responsive, or for mimicking CSS
media queries on platforms that don't support them.

You can use jRespond to respond to changes in height, width, or aspect ratio (width / height). Using it
is as simple as specifying the thresholds you care about, the name of each state, and the javascript
callback (or CSS selector). It looks like this:

```
function windowWidthDidChange(namespace, currentState, priorState) {
  console.log(namespace + ' moved from "' + priorState + '" to "' + currentState + '".');
}
var states = ['narrow', 'medium', 'wide', 'x-wide'];
var thresholds = [350, 500, 800, 1000];
$.respondToWidths('my-width-namespace', states, thresholds, windowWidthDidChange);

// On resizing from 499 to 500 pixels:
> my-width-namespace moved from medium to wide.
```

The namespacing feature allows you to specify as many sets of independent thresholds as you like, on
window height, width or aspect ratio. You can specify a callback, to be fired when thresholds are
crossed. You can also pass in a jQuery selector string; this will be used to apply state classes to
elements, allowing you to support media query-like behavior in IE8.

Since jRespond only ever attaches one resize event, it provides a more efficient way to respond to
window size in disparate areas of code. Different areas can listen for the changes they care
about, without worrying about - or even knowing about - what other parts of your app are doing.

API
---

### respondToHeights, respondToWidths, respondToAspectRatios

- namespace: All sets of thresholds must be namespaced. This allows you to set up multiple threshold
  sets on each dimension. It is also used when retrieving current states, and when removing a threshold
  set. Namespaces must be unique, so your width namespace can be 'width', but other threshold sets must
  use different names (for example 'header-width').
- states: An array of Strings with the names of each state, in ascending order. For example, you might
  pass ['narrow', 'medium', 'wide'].
- thresholds: An array of numbers with the thresholds between each state. In the above example, you
  might pass in [350, 600]. That there must always be one fewer threshold than state. Note that
  height & width thresholds are pixel counts, while aspect ratio thresholds are decimal ratios of
  width to height.
- callback: An optional callback method with signature (namespace, newState, priorState). Called whenever
  the window is resized past a threshold. (You can explore "this" in your callback for extra information
  about the threshold.)
- selector: An optional jQuery selector. If provided, then the specified elements will have stateful
  classes appended to them. For example, if the "header-width" namespace is in "narrow" state, then specified
  elements will have the class "header-width-narrow" appended to them. You can use this feature to emulate CSS
  media queries on legacy platforms that don't support them natively.

### respondCurrentState(namespace)

Returns the current state for the specified namespace.

### respondCancel(namespace)

Cancels the specified namespace.

License
-------

jRespond copyright (c) 2013 Dave Porter.

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License
[here](http://www.apache.org/licenses/LICENSE-2.0).

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
