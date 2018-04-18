# REST API

## Introduction {#Remote(REST)API-Introduction}

Asset Tracker uses very powerful remote API. This API is used by the Asset Tracker front-end \(its web pages\), but it can also be used by external agents, to query Asset Tracker for information about assets, as well as for creating and updating asset information.

## Using Asset Tracker REST API {#Remote(REST)API-UsingAssetTrackerRESTAPI}

In order to use Asset Tracker REST API, you need to perform HTTP requests to URLs that begin with the base address **&lt;jira-base-url&gt;/rest/com-spartez-ephor/1.0. **When describing the Asset Tracker REST API, addresses relative to this URL will be listed.

#### **Request Types** {#Remote(REST)API-RequestTypes}

As is standard with typical REST API, Asset Tracker uses HTTP **GET** requests to query for information, **POST** to add new entities, **PUT** to update existing entities and **DELETE** to remove entities. Because some network proxies do not let requests other than GET and POST through, it is possible to only use GET and POST requests, and specify the "real" request that is intended by setting the `X-HTTP-Method-Override` header appropriately.

#### **Authentication** {#Remote(REST)API-Authentication}

Asset Tracker REST API can use either session cookie authentication \(this is used by Asset Tracker front-end\). Session cookie can be received by logging in to Jira. 

Alternatively, [basic authentication](https://en.wikipedia.org/wiki/Basic_access_authentication) can be used to authenticate REST calls - this method is likely to be used by external tools accessing Asset Tracker.

#### **Data Structures** {#Remote(REST)API-DataStructures}

Asset Tracker REST API returns all data in JSON format. The input that it accepts is mostly also in JSON \(`application/json)` format, with some resources also using "form" \(`application/x-www-form-urlencoded`\) data - see descriptions of resources below. Input format must be specified in the Content-Type request header. Additionally, some parameters are passed to resources as URL parameters.

## Available Resources {#Remote(REST)API-AvailableResources}

This section lists available REST resources and methods of accessing, creating and modifying them.

### **Item** {#Remote(REST)API-Item}

The REST resources with paths starting with `/item` operate on Ephor items/assets.

| Path \(with parameters\) | **Method** | **URL Parameters** | **Data Parameters** | **Description** |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| `/item` | GET | category |   | Returns items from a folder given by the **category** parameter, which is either numerical folder ID, or its path \(e.g. "/Electronics/Computers/Laptops"\) |
|   | POST |   | JSON | Creates a new asset. Data paremeter is a JSON like this:`{    typeName: "my.computer.type",    categoryName: "/my/folder/path",    fields: [        { typeName: "field.type.one", values: [ "value1"` `] },        { typeName: "field.type.two", values: [ "value2"` `] }    ]}`Returns a newly created asset |
| `/item/`**`{itemId}`** | GET |   |   | Returns asset with a given ID |
|   | DELETE |   |   | Deletes asset with a given ID |
| `/item/`**`{itemId}`**`/links` | GET |   |   | Returns links incoming to and outgoing from asset with a given ID |
|   | POST |   | JSON | Links an asset to another asset using a link of a given type \(see [link types](rest-api.md#link-types)\). Data parameter is a JSON like this:`{    type: { id: 10000 },    inbound: { id: 10001 },    outbound: { id: 10002 }}`Returns a newly created lnk |
| `/item/`**`{itemId}`**`/links/`**`{linkId}`** | DELETE |   |   | Deletes an asset link |
| `/item/`**`{itemId}`**`/linkgraph` | GET | levels |   | Returns a graph of links for an asset with a given ID. **levels** parameter specifies the depth of a graph \(default is 3\) |
| `/item/`**`{itemId}`**`/history` | GET |   |   | Returns a history of asset with a given ID |
| `/item/bulkdelete` | DELETE | ids |   | Deletes assets in bulk. **ids** is a comma-separated list of asset IDs |
| `/item/addorupdate` | POST | matchingQueryuniquetypecategory | JSON | Searches for assets using **matchingQuery**. If assets are found, they are updated using the supplied data parameter, which looks like this:`[    { typeName: "field.type.one", values: [ "value1"` `] },    { typeName: "field.type.two", values: [ "value2"` `] }]`If the **unique** parameter is set to **true** and more than one asset is found, a "NOT ACCEPTABLE" \(406\) HTTP error is returned and assets are not updated.If no assets are found using **matchingQuery**, an asset is created. Its type is specified by the **type** parameter \(either numerical type ID, or type dotted name\) and the asset is put in the folder specified by the **category** parameter \(either numerical ID or folder path\) |
| `/item/field` | POST |   | JSON | Bulk-updates a field of specified assets. Assets and fields to update and values to set are specified in the data parameter, which looks like this:`{    itemIds: [ 10001, 10002, 10003 ],    fieldType: 10000,    values: [ "value1"` `]}`Note that the field type must be specified as a numerical value \(not a dotted name\) |
| `/item/`**`{itemId}`**`/field/`**`{idOrName}`** | POST | fielddef | JSON | Sets a value of an asset field, both specified as path parameters, where **idOrName**can either be a field ID or its dotted name. If field ID is -1, it is assumed that the field does not yet exist in an asset and it is added. The type of the field to add is specified by the **fielddef **URL parameter, which is a dotted name of a field type.Values to set in a field are specified as JSON list of strings in the data parameter |
| `/item/`**`{itemId}`**`/category` | POST |   | Form:catId | Moves an asset to a folder specified by the **catId** form parameter. The parameter can either by a numerical category ID or folder path. |
| `/item/category/bulkmove` | POST |   | Form:idscatId  | Bulk moves assets with a given **ids** \(list of numerical IDs\) to a folder given by the **catId**parameter. |

### **Search** {#Remote(REST)API-Search}

The resources with paths starting with `/search `are for searching for items and for managing saved searches.

| **Path \(with parameters\)** | **Method** | **URL Parameters** | **Data Parameters** | **Description** |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| `/search` | GET | querymaxcountoffset |   | Searches for assets given by the **query **parameter \(read more on [Search query syntax](../searching/search-query-syntax/)\). **maxcount** and **offset**parameters can be used for paging results |
| `/search/searches/my` | GET |   |   | Returns a list of personal saved searches |
|   | PUT |   | JSON | Replaces a list of personal saved searches with a given list of`{    name: "my search name",    nql: "type = Computer"}` |
| `/search/searches/my/`**`{id}`** | PUT |   | JSON | Updates a personal saved search with a given ID with a supplied value \(see above for the format of data\) |
|   | DELETE |   |   | Deletes a personal saved search with a given ID |
| `/search/searches/public` | GET |   |   | Returns a list of public saved searches |
|   | PUT |   | JSON | Replaces a list of public saved searches with a given list \(see above for the format\) |
| `/search/searches/public/`**`{id}`** | PUT |   |   | Updates a public saved search with a given ID with a supplied value \(see above for the format of data\) |
|   | DELETE |   |   | Deletes a public saved search with a given ID |

### **Folders** {#Remote(REST)API-Folders}

The resources with paths starting with `/category` are for operations on Asset Tracker folders.

| **Path \(with parameters\)** | **Method** | **URL Parameters** | **Data Parameters** | **Description** |
| --- | --- | --- | --- | --- | --- | --- | --- |
| `/category` | GET | recursive |   | Returns a root folder. If **recursive** is set to **true**, the whole tree of folders is returned |
|   | POST |   | JSON | Creates a new folder, specified by the following structure:`{    parentId: 10000,    name: "My Folder"`  `}`Returns a new folder |
| `/category/`**`{idOrPath}`** | GET | recursive |   | Returns a folder given by numerical ID or folder path \(e.g. "/Electronics/Computers/Laptops"\). If **recursive** is set to **true**, returns a subfolder tree |
|   | POST |   | Form:moveTo  | Moves a folder to a different parent. A new parent is given by the **moveTo** parameter \(a numerical folder ID\) |
|   | PUT |   | JSON | Updates a folder given by a numerical ID or folder path \(see above for the data format\) |
|   | DELETE |   |   | Deletes a folder given by a numerical ID or folder path |
| `/category/`**`{idOrPath}`**`/parents` | GET |   |   | Returns a list of parents of a given folder, starting from the root folder |

### **Asset and Field Type** {#Remote(REST)API-AssetandFieldType}

The resources with paths starting with `/itemtype` are for operations on Asset Tracker asset types.

| Path \(with parameters\) | Method | URL Parameters | Data Parameters | Description |
| --- | --- | --- | --- | --- | --- |
| `/itemtype` | GET |   |   | Returns all asset types defined in an Asset Tracker instance |
|   | POST |   | JSON | Adds a new asset type. Data format is:`{    dottedName: "my.asset.type",    name: "Display Name of type",  }`Returns a newly created item type |
| `/itemtype/`**`{idOrName}`** | GET |   |   | Returns an asset type given by a numerical ID or dotted name |
|   | PUT |   | JSON | Updates an asset type given by a numerical ID or dotted name. See above for the data format. |
|   | DELETE |   |   | Deletes an asset type given by a numerical ID or dotted name |

The resources with paths starting with `/fieldtype` are for operations on Asset Tracker [field types](../guide/defining-an-asset-field.md). Field types are not directly tied to asset types - the same field type can exist in multiple asset types. They are associated with asset types using the `/itemtypefield` resources, which define a given field type parameters, such as label title, position, size and colors, when it is used in a concrete asset type.

| **Path \(with parameters\)** | **Method** | **URL Parameters** | **Data Parameters** | **Description** |
| --- | --- | --- | --- | --- | --- |
| `/fieldtype` | GET |   |   | Gets all field types defined in an Asset Tracker instance |
|   | POST |   | JSON | Creates a new field type. Data format is:`{    name: "dotted.field.type.name",    defaultTitle: "Default field label title",    templateName: "singlesel",    allowedValues: [ "option1", "option2"` `]}`The **templateName** can be one of:stringlineuserglobaliditemtypeidstringareaimagedateintegerdoublesingleselmultiselhyperlinkcheckboxThe **singlesel** and **multisel **templates should have **allowedValues**list defined. |
| `/fieldtype/`**`{idOrName}`** | GET |   |   | Returns a field type given by a numerical ID or dotted name |
|   | PUT |   | JSON | Updates a field type given by a numerical ID or dotted name. See above for the data format |
|   | DELETE |   |   | Deletes a field type given by a numerical ID or dotted name |

The resources with paths starting with `/itemtypefield` are for operations on fields associated with concrete asset types.

| **Path \(with parameters\)** | **Method** | **URL Parameters** | **Data Parameters** | **Description** |
| --- | --- | --- | --- | --- | --- | --- |
| `/itemtypefield/`**`{idOrName}`** | GET |   |   | Get fields definitions for an asset type given by a numerical ID or dotted name |
|   | POST |   | JSON:FieldRepresentation | Adds a new field definition to an item type, using default values of position, title, size, color and other parameters. A data parameter is:`{    type: 10000,    name: "My label for a field"}  `The type has to specify a field type \(see above\) by its numerical ID \(not its dotted name\) |
|   | PUT |   | JSON | Update asset type fields positions, sizes, title, colors and other parameters.The data parameter is a list of`{    id: 10000,    title: "My field label title",    type: 10000,    posx: 1,    posy: 0,    width: 1,    height: 1,    mobiley: 0,    css: "color: red",    labelCss: "color: blue",    requiredInCreate: true}` |
| `/itemtypefield/`**`{typeIdOrName}`**`/`**`{fieldIdOrName}`** | GET |   |   | Gets a field definition specified by **fieldIdOrName**for an asset type specified by **typeIdOrName** |
|   | PUT |   | Form:titlebgColortextColorlabelColorrequiredInCreate | Updates a field definition specified by **fieldIdOrName** for an asset type specified by **typeIdOrName**. Parameters that can be set are specified by a form |
|   | DELETE |   |   | Deletes a field definition specified by **fieldIdOrName** for an asset type specified by **typeIdOrName**. |

### **Link Types** {#Remote(REST)API-LinkTypes}

The resources with paths starting with `/linktype` are for operations on types of links between assets.

| **Path \(with parameters\)** | **Method** | **URL Parameters** | **Data Parameters** | **Description** |
| --- | --- | --- | --- | --- | --- |
| `/linktype` | GET |   |   | Gets all link types defined in an Asset Tracker instance |
|   | POST |   | JSON |  Adds a link type. Data parameter is:`{    name: "Link name",    inboundName: "Inbound end name",    outboundName: "Outbound end name"}`Returns a new link type |
| `/linktype/`**`{id}`** | GET |   |   | Returns a link type given by its numerical ID |
|   | PUT |   | JSON | Updates a link type given by its numerical ID \(see above for the data format\) |
|   | DELETE |   |   | Deletes a link type given by its numerical ID |

### Operation Sequences {#Remote(REST)API-OperationSequences}

The resources with paths starting with `/stored-operation` are for defining and executing [Defining operation sequences](../how-to/how-to-define-and-execute-pre-packaged-operation-sequences-on-assets/defining-operation-sequences.md).

| Path \(with parameters\) | Method | URL Parameters | Data Parameters | Description |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Path \(with parameters\) | Method | URL Parameters | Data Parameters | Description |
| `/stored-operation` | GET |   |   | Gets all stored operation sequences visible by the current user |
|   | POST |   | JSON |  Adds a stored operation sequence. Data parameter is:`{    publicOpSet: true,    name: "A public operation sequence"}`Returns a new operation sequence |
| `/stored-operation/field-hints` | GET |   |   | Returns all usage hints for all field types defined in Asset Tracker |
| `/stored-operation/`**`{id}`** | GET |   |   | Returns an operation sequence given by its numerical ID |
|   | PUT |   | JSON | Updates an operation sequence given by its numerical ID |
|   | DELETE |   |   | Deletes a stored operation sequence |
| `/stored-operation/`**`{id}`**`/execute` | POST | issuekey | JSON | Executes a stored operation sequence. Body is a JSON list of asset IDs, on which the operation sequence is to be executed**issuekey** determines what issue to use for issue context specific markers. |
| `/stored-operation/`**`{id}`**`/reorder` | POST |   | JSON | Reorders the operations within the operation sequence. Body is the list of operation IDs in new order. All of the operations must be present in teh sequence. |
| `/stored-operation/`**`{id}`** | POST |   | JSON | Adds an operation to the operation sequence. Body is:`{    fieldName: "spartez.description",    valueToSet: "+update"    order: 0}`Returns the operation sequence containing the newly added operation |
| `/stored-operation/`**`{id}`**`/`**`{opId}`** | PUT |   | JSON | Updates an operation in the operation sequence.Returns the operation sequence containing the newly added operation |
| `/stored-operation/`**`{id}`**`/`**`{opId}`** | DELETE |   |   | Deletes an operation from the operation sequence.Returns the operation sequence containing the newly added operation |



