# Schemas

## Table of Contents
<!-- toc -->
---

## Module

**Download:** [json-schema file](./module.json)

**Example:**

```json
{{#include module.example.json}}
```

## Type

**Download:** [json-schema file](./type.json)

> ❗️ **Gotcha**: When defining custom schemas for your types, make sure to not disallow additional properties.
> 
> This is required for the validator to property combine the [base content schema](#content) with your custom schema correctly.
>
> This is a limitation of JSON Schema, a more detailed explanation is available [here](https://json-schema.org/understanding-json-schema/reference/object.html?highlight=additionalproperties#unevaluated-properties).

**Example:**

```json
{{#include type.example.json}}
```

## Content

**Download:** [json-schema file](./content.json)

**Example:**

```json
{{#include content.example.json}}
```