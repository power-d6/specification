### splitLines

Splits a multiline string into an array of strings.

#### Usage:

##### Template:

```handlebars
{{#each (splitLines self.quote) as |line| }}
> {{line}}
>
{{/each}}
```

##### Input data:

```json
{
    "self": {
        "quote": "This is a quote.\nIt involves multiple lines.\nThis is a pain to render correctly."
    },
    // ...
}
```

##### Output:

```md
> This is a quote.
>
> It involves multiple lines.
>
> This is a pain to render correctly.
>
```