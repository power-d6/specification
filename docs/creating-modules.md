# Creating modules

While it is definitely possible to create modules by hand,
the structure of the contents can be hard to manage and change over time.

However, there is an easier way to create complex modules: using directories and the [`powerd6_cli`](https://github.com/powerd6/tools) tool. The [core rules](https://github.com/powerd6/core-rules) are a good example of this being used.

## Directory Structure

The tool can run against any directory and works in the following manner:

### Module metadata

The file named `module` (regardless of extension) or the files inside the directory `module` fill the basic metadata (title, source, description) of the module.

The module metadata can also optionally contain types and contents definitions, but this is **not** recommended.

### Types and Content

The files inside the `types` and `contents` directories will be mapped accordingly, with the following rules:

If a file named `_` (regardless of extension) exists, then all files in that directory will be used to fill the metadata of a single entry. Otherwise, each file in the directory will be mapped to their own entry.

Other sub-directories contained within the current directory are mapped under the same rules. The one exception is the `rendering` subdirectory, where it's files will be added to the parent entry.

For each created entry, their identifier is an underscore (`_`) separated list of the folder and file names between the first directory (`types` or `contents`) and the entry.

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
            "description": "",
            "schema": {},
            "rendering": {
                "md": ""
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