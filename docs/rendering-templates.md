# Rendering Templates

When defining a type, it is important to also define how to render it into the screen.

The supported mechanism for rendering templates uses [handlebars](https://handlebarsjs.com/) files, that define how each piece of content of the given type must be rendered.

## Data input

The advantages of handlebars templates is that it allows for some lightweight logic to be embedded into them, allowing for somewhat complex behaviors, like referencing, counting and conditionals.

The handlebars engine will receive, for each type it tries to render, the following object structure:

```json
{
    "self": {},
    "module": {}
}
```

In this structure, the `self` property hold the value of the content piece being rendered, and `module` holds a copy of the entire module tree.

This structure allows for content pieces to cross-reference each-other, for example, this is how a piece of content would include the `name` of other content pieces, referenced by their identifier:

```handlebars
# {{self.name}}

{{self.description}}

## References:
{{#each self.references as |reference_id|}}
{{#with (lookup ../module.content [reference_id]) as | reference |}}
- {{reference.name}}
{{/with}}
{{/each}}
```