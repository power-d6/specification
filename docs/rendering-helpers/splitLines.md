### splitLines

Splits a multiline string into an array of strings.

#### Usage:

```handlebars
{{#each (splitLines self.example_concept) as |line| }}
> {{line}}
>
{{/each}}
```