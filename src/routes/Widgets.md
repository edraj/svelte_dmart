<script>
  import {QueryType} from "@edraj/tsdmart";
  import ListView from "@/lib/ListView.svelte";
</script>

# List view

Now you can do a full text search or an attribute based search for that field.
for example, lets say we want to retrieve all sub-folders under **mysapce** space

we call the `/query` API with the following request body

```json
{
  "filter_shortnames": [],
  "type": "subpath",
  "search": "",
  "space_name": "myspace",
  "subpath": "/",
  "exact_subpath": true,
  "limit": 15,
  "offset": 0,
  "retrieve_json_payload": true,
  "sort_type": "ascending",
  "sort_by": "created_at"
}
```

And the results would be:

<ListView
type={QueryType.subpath}
space_name={"myspace"}
subpath={"/"}
is_clickable={false}
scope={"public"}
/>