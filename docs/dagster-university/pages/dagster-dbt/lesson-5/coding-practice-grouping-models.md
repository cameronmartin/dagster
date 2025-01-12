---
title: 'Practice: Grouping dbt models by layer'
module: 'dagster_essentials'
lesson: '5'
---

# Practice: Grouping dbt models by layer

Override the `get_group_name` method in your `CustomizedDagsterDbtTranslator` to group each dbt model by their layer (`marts` and `staging`).

**Hint:** `dbt_resource_props` is Python dictionary with a structure that contains something like this:

```json
{
    "database": "data",
    "schema": "main",
    "name": "stg_trips",
    "resource_type": "model",
    "package_name": "analytics",
    "path": "staging/stg_trips.sql",
    "original_file_path": "models/staging/stg_trips.sql",
    "unique_id": "model.analytics.stg_trips",
    "fqn": ["analytics", "staging", "stg_trips"],
    "alias": "stg_trips",
    ... #other properties
}
```

`get_group_name` expects to return a string to group the dbt models by. What property of `dbt_resource_props` can you access (and maybe even index!) to group the models by layer (ex. `marts` or `staging`)?

---

## Check your work

The method you built should look similar to the following code. Click **View answer** to view it.

**If there are differences**, compare what you wrote to the code below and change them, as this method will be used as-is in future lessons.

```python {% obfuscated="true" %}
@classmethod
def get_group_name(cls, dbt_resource_props):
    return dbt_resource_props["fqn"][1]
```