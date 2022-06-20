# **[GET]** /api/packages
List all packages.

Auth: `FALSE`
Parameters:
---
* page _(optional)_ `[integer]` | Location: `query` | Defaults: `1` 
  - Indicate the page number to return.


---
* sort _(optional)_ `[string]` | Location: `query` | Defaults: `downloads` | Valid: `[downloads, created_at, updated_at, stars]`
  - The method to sort the returned pacakges by.


---
* direction _(optional)_ `[string]`  | Defaults: `desc` | Valid: `[desc, asc]`
  - Which direction to list the results. If sorting by stars, can only be sorted by desc.


---
Responses:
---
**HTTP Status Code:** `200 OK`

**Type:** `[application/json]`

Returns a list of all packages. Paginated 30 at a time. Links to the next and last pages are in the 'Link' Header.


---
# **[POST]** /api/packages
Publishes a new Package.

Todo: With auth not setup, nor atombot setup, this is non-functional.

Auth: `true`
Parameters:
---
* repository _(required)_ `[string]` | Location: `query`  
  - The repository containing the plugin, in the form 'owner/repo'.


---
* Authentication _(required)_ `[string]` | Location: `header`  
  - A valid Atom.io token, in the 'Authorization' Header.


---
Responses:
---
**HTTP Status Code:** `201 `

**Type:** `[application/json]`

Successfully created, return created package.


---
**HTTP Status Code:** `400 Bad Request`

**Type:** `[application/json]`

Repository is inaccessible, nonexistant, not an atom package. Could be different errors returned.

```json
{ "message": "That repo does not exist, ins't an atom package, or atombot does not have access." }, { "message": "The packagge.json at owner/repo isn't valid." }
```


---
**HTTP Status Code:** `409 Conflict`

**Type:** `[application/json]`

A package by that name already exists.


---
# **[GET]** /api/packages/search
Searches all Packages.

Auth: `FALSE`
Parameters:
---
* q _(required)_ `[string]` | Location: `query`  
  - Search query.


---
* page _(optional)_ `[integer]` | Location: `query`  
  - The page of search results to return.


---
* sort _(optional)_ `[string]` | Location: `query` | Defaults: `relevance` | Valid: `[downloads, created_at, updated_at, stars]`
  - Method to sort the results.


---
* direction _(optional)_ `[string]` | Location: `query` | Defaults: `desc` | Valid: `[asc, desc]`
  - Direction to list search results.


---
Responses:
---
**HTTP Status Code:** `200 OK`

**Type:** `[application/json]`

Same format as listing packages.


---
# **[GET]** /api/packages/:packageName
Show package details.

Auth: `FALSE`
Parameters:
---
* packageName _(required)_ `[string]` | Location: `path`  
  - The name of the package to return details for. URL escaped.


---
* engine _(optional)_ `[string]` | Location: `query`  
  - Only show packages compatible with this Atom version. Must be valid SemVer.


---
Responses:
---
**HTTP Status Code:** `200 OK`

**Type:** `[application/json]`

Returns package details and versions for a single package.


---
# **[DELETE]** /api/packages/:packageName
Delete a package.

Auth: `true`
Parameters:
---
* packageName _(required)_ `[string]` | Location: `path`  
  - The name of the package to delete.


---
* Authorization _(required)_ `[string]` | Location: `header`  
  - A valid Atom.io token, in the 'Authorization' Header.


---
Responses:
---
**HTTP Status Code:** `204 No Content`

**Type:** `[application/json]`

Successfully deleted package.

```json
{ "message": "Success" }
```


---
**HTTP Status Code:** `400 Bad Request`

**Type:** `[application/json]`

Repository is inaccessible.

```json
{ "message": "Respository is inaccessible." }
```


---
**HTTP Status Code:** `401 Unauthorized`

**Type:** `[application/json]`

Unauthorized.


---