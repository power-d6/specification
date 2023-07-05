# 5. Switch rendering template

Date: 2023-07-05

## Status

Accepted

## Context

When implementing the core rules, [an issue](https://github.com/sunng87/handlebars-rust/issues/592) arose with the rendering of a specific template.

While the issue seems to be related to the library used to render the template- and not with the reference implementation of the rendering engine- the lack of feature (and bug) parity might cause problems down the line.

The following template languages (and their implementing libraries) are under consideration:

- Handlebars:
  - [handlebars-rust](https://crates.io/crates/handlebars)
  - Fallback to locally installed [`handlebars`](https://handlebarsjs.com/) command
- Jinja2:
  - [minijinja](https://crates.io/crates/minijinja)
- Liquid:
  - [liquid](https://crates.io/crates/liquid)

### Tests

To validate the viability of each library, some tests will be performed.

All test will have the same input data structure:

```json
{
    "data": {
        "name": "John",
        "related": {
            "mary": {
                "relationship": "Siblings"
            }
        }
    },
    "other": {
        "contents": {
            "john": {
                "name": "John",
                "related": {
                    "mary": {
                        "relationship": "Siblings"
                    }
                }
            },
            "mary": {
                "name": "Mary"
            }
        }
    }
}
```

#### Handlebars

```handlebars
# {{data.name}}

{{#each data.related as |related|}}
{{#with (lookup ../other.contents @key) as | other_related |}}
## [{{other_related.name}}](/{{@key}})
{{related.relationship}}
{{/with}}
{{/each}}
```

#### Jinja2

```jinja2
# {{data.name}}

{%- for related in data.related %}
## [{{other.contents[related[0]].name}}](/{{related[0]}})
{{related[1].relationship}}
{%- endfor %}
```

#### Liquid

```liquid
# {{data.name}}

{%- for related in data.related %}
## [{{other.contents[related].name}}](/{{related}})
{{data.related[related].relationship}}
{%- endfor %}
```

## Decision

The change that we're proposing or have agreed to implement.

## Consequences

What becomes easier or more difficult to do and any risks introduced by the change that will need to be mitigated.
