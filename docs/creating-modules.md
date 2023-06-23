# Creating modules

> ⚠️ **Important**: This page is a work-in-progress and is incomplete.
> The tool being developed for this use-case is currently located in
> [another repository](https://github.com/powerd6/tools).

While it is definitely possible to create modules by hand,
the structure of the contents can be hard to manage and change over time.

However, there is an easier way to create complex modules: using directories.

This is can be accomplished by installing the [`powerd6_cli`](https://github.com/powerd6/tools) tool.

## Directory Structure

The tool can run against any directory and works in the following manner:

1. A file named `module` (regardless of extension) or all files inside the `module` directory will be used to fill the basic metadata (title, source, description) of the module.
2. The module metadata can optionally contain types and contents definitions
3. The files inside the `types` and `content` directories will be mapped accordingly, with the following rules:
   1. If a file named `_` (regardless of extension) exists, all files in that directory will be used to fill the metadata of a single entry
   2. Otherwise, each file in the directory will be mapped to their own entry
   3. Directories contained within the current directory will be mapped under the same rules as the basic directory, with the exception of the `rendering` directory inside a type.

## Examples

### File structure

```bash
my_module/
├── module.json
├── types/
│   ├── spells.yml
│   ├── items.json
│   └── attributes/
│       ├── _.json
│       ├── description.md
│       └── schema.json
│       └── rendering/
│           └── md.txt
└── contents/
    ├── spells/
    │   ├── fireball.json
    │   └── heal.yaml
    └── items/
        └── potions/
            ├── health_potion.json
            └── sleep_potion.json
```

### Resulting Module

```json
{
    "title": "",
    "description": "",
    "source": "",
    "types": {
        "spells": {},
        "items": {},
        "attributes": {
            "rendering": {
                "md": "..."
            }
        }
    },
    "contents": {
        "spells_fireball": {},
        "spells_heal": {},
        "items_potions_health_potion": {},
        "items_potions_sleep_potion": {}
    }
}
```