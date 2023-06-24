# Creating modules

While it is definitely possible to create modules by hand,
the structure of the contents can be hard to manage and change over time.

However, there is an easier way to create complex modules: using directories and the [`powerd6_cli`](https://github.com/powerd6/tools) tool.

## Directory Structure

The tool can run against any directory and works in the following manner:

1. A file named `module` (regardless of extension) or all files inside the `module` directory will be used to fill the basic metadata (title, source, description) of the module.
   1. The module metadata can optionally contain types and contents definitions
2. The files inside the `types` and `content` directories will be mapped accordingly, with the following rules:
   1. If a file named `_` (regardless of extension) exists:
      - All files in that directory will be used to fill the metadata of a single entry;
      - Otherwise, each file in the directory will be mapped to their own entry.
   2. Directories contained within the current directory will be mapped under the same rules as the basic directory.
      1. The `rendering` directory is treated differently when inside the `types` directory.

### Examples

#### File structure

```bash
my_module/
├── module.json
├── types/
│   ├── attributes/
│   │   ├── _.json
│   │   ├── description.md
│   │   └── schema.json
│   │   └── rendering/
│   │       └── md.txt
│   ├── spells.yml
│   └── items.json
└── contents/
    ├── items/
    │   └── potions/
    │       ├── health_potion.json
    │       └── sleep_potion.json
    └── spells/
        ├── fireball.json
        └── heal.yaml
```

#### Resulting Module

```json
{
    "title": "",
    "description": "",
    "source": "",
    "types": {
        "attributes": {
            "rendering": {
                "md": "..."
            }
        },
        "items": {},
        "spells": {}
    },
    "contents": {
        "items_potions_health_potion": {},
        "items_potions_sleep_potion": {},
        "spells_fireball": {},
        "spells_heal": {}
    }
}
```