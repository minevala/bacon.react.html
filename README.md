[![npm version](https://badge.fury.io/js/bacon.react.html.svg)](http://badge.fury.io/js/bacon.react.html)

This library allows you to embed [Bacon](https://github.com/baconjs/bacon.js)
streams into React Virtual DOM.

## Usage

Import the elements and other utilities you need, e.g.

```jsx
import {set, toggle, Div, Input, Label, P} from "bacon.react.html"
```

and you can then use them like ordinary HTML tags, but with Bacon streams in
properties or as children.  For example, you could write

```jsx
import {set, Input} from "bacon.react.html"

<Input type="text"
       mount={c => c && c.focus()}
       value={value}
       onChange={set(value)}/>
```

where `value` refers to a [Bacon.Model](https://github.com/baconjs/bacon.model)
and `mount` does the same thing as `ref`: JSX/React treats it as a special case,
so it had to be renamed.

A single lifted tag, like `Input` above, lifts Bacon streams only when they are
immediately contained properties or children.  So, you can safely write

```jsx
<Div>
  <Label htmlFor="likes-bacon">Bacon is tasty</Label>
  <Input type="checkbox"
         id="likes-bacon"
         checked={checked}
         onChange={toggle(checked)}/>
  <P hidden={checked}>Are you sure?</P>
</Div>
```

Note, however, that those elements that immediately contain streams must to be
lifted (React will choke on plain Bacon).  So, the above could also have been
written as:

```jsx
<div>
  <label htmlFor="likes-bacon">Bacon is tasty</label>
  <Input type="checkbox"
         id="likes-bacon"
         checked={checked}
         onChange={toggle(checked)}/>
  <P hidden={checked}>Are you sure?</P>
</div>
```

## Longer examples

* [TodoMVC](https://github.com/polytypic/atomi-todomvc)
