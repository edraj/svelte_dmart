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
  "type": "search",
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
    type={QueryType.search}
    space_name={"myspace"}
    subpath={"/"}
    scope={"public"}
/>

and you can also add a search bar for the list view:

<ListView
    type={QueryType.search}
    space_name={"myspace"}
    subpath={"/"}
    isSearchable={true}
    scope={"public"}
/>

or with a predefined search text:
<ListView
    type={QueryType.search}
    space_name={"myspace"}
    subpath={"/"}
    searchValue={"test"}
    scope={"public"}
/>