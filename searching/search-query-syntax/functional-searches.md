# Functional searches

In addition to searching using contents of fields, asset types and folders as criteria, Asset Tracker allows searching using search functions. To use it, type a search function name and parameters in the search box, like this:

| `search_function(parameter,parameter,...)` |
| --- |


Currently supported search functions are:

| **Function Name and Parameters** | **Description** |
| --- | --- | --- | --- | --- | --- | --- | --- |
| `id_in() ` | searches for assets with given IDs. Parameters are comma-separated IDs of assets to search for |
| `my_primary()` | searches for user's primary asset |
| `my() ` | searches for assets in which any field of type "User" is set to the current user, and the user's primary asset |
| `my_with_linked()` | searches for assets in which any field of type "User" is set to the current user, and the user's primary asset, and all assets linked to these assets, directly or indirectly |
| `user_is(username) ` | searches for assets in which any field of type "User" is set to the supplied user |
| `user_is_with_linked(username)` | searches for assets in which any field of type "User" is set to the supplied user and all assets linked to these assets, directly or indirectly |
| `linked_items(id-or-query, include-indirect, include-parent)` | searches for assets linked to the assets\(s\) defined by ID or Asset Tracker search query - directly or indirectly, depending on the `include-indirect`parameter \(`true` or `false`\). If the `include-parent` parameter is set to `true`, the list will also contain the assets defined by the first parameter. |

The list of search functions will be updated in the new Asset Tracker versions.

