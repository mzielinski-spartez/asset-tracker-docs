# Search query syntax

### Search modes {#Searchquerysyntax-Searchmodes}

**Asset Tracker **supports two search modes:

* **Simple mode.** Just type any text into search box, and Asset Tracker will find all assets containing given phrase in any of their text fields \(actualy, it is equivalent to a "similarity" search on all text fields - see below\). 
* **Advanced mode. ** You can enter complex queries using built-in query language. This page documents syntax of such queries.
* [**Functional search**](functional-searches.md)**.** You can use search functions to find assets that fulfil a given criteria.

### Advanced search query syntax {#Searchquerysyntax-Advancedsearchquerysyntax}

Every query consists of at least one question, which should include `Field`, `Operator` and optionally `Value` \(in that order\). Questions can be linked together using `Conjunctions` and parentheses and ordered by selected field.

* **Field** - field name, as defined in _Administration -&gt; Field types _section \(e.g. `system.title`\). There are also following special field types defined:
  * `text` - references all text fields. Simple search actually uses this internally.
  * folder - references folder name
  * `type` - references asset type name
* **Operator** - one of the two types
  * **Binary operator** - defines relation between field and value. It can be one of the following: `=, ~, <, >, <=, >=, !=`. For multiple selection fields `=` \(equals\) operator means that field should have at least one of the typed values. Operator `~` means "fuzzy search" which is approximate text search \(words can have typos etc.\).
  * **Unary operator** - an operator that isn't followed by any value. There are three available unary operators: 
    * `IS EMPTY` and `IS NOT EMPTY `- they can be used to query assets that have given field empty \(no value is set\) or not empty \(some value is set\). 
* **Value \(optional\)** - value that is searched for, used only with binary operator. Multi-word text should be provided in apostrophes. 
  * Date format is:
    * `YYYY-MM-DD` for absolute dates \(e.g. `2014-03-27`\) 
    * `+/-XmYwZd` for relative dates \(e.g. `-2m3w2d` or `3m2d`, where "m" is months, "w" is weeks and "d" is days\)
* **Conjunction** \(optional\) - used for joining queries. Two conjunctions are available: `AND` & `OR`\(where `AND` has higher precedence\). Operator precedence can be overriden using parentheses: `(` and `)`.
* **Order by **\(optional\) - field name which values should be user for results ordering. If `ORDER BY` is not specified, results are order by last update time \(most recently updated first\) by default. 

### Advanced search query examples {#Searchquerysyntax-Advancedsearchqueryexamples}

Find assets with title containing word _chair:_

| `system.title = chair` |
| --- |


Find assets with title containing exact phrase_ jingle bells:_

| `system.title = "jingle bells"` |
| --- |


Find assets with `some.field` value _automobile_ or similar \(e.g. with typos, such as: _atomobile_, _autombile_, etc.\). Simple search uses this type of matching internally:

| `some.field ~ automobile` |
| --- |


Find assets of _Computer_ type with `computer.model` field value set to _X123:_

| `type = Computer AND computer.model = X123` |
| --- |


List all laptops \(assets where `computer.type` field is set to _Laptop_\) ordered by memory size \(biggest values first\):

| `type = Computer AND computer.type = Laptop ORDER BY computer.memory.size DESC` |
| --- |


List all books that have no owner assigned; order results by title:

| `type = Book AND book.owner IS EMPTY ORDER BY book.title` |
| --- |


