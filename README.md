# apidoc-swagger

Note: The original package would not work with @apiSchema (apidoc-plugin-schema) and it seems to be no longer maintained.

Apidoc and Swagger are two nice projects which are focusing on documentation of APIs. 
This project is a middle tier which tries to bring them together in a sense that:
> It uses apidoc to convert inline documentation comments into json schema and later convert it to swagger json schmea.


## HOW IT WORKS

### OPTION 1:

***(uses [apidoc-core](https://github.com/apidoc/apidoc-core) library)***

APIDOC_INLINE_COMMENTS_IN_CODE -> APIDOC (json) -> SWAGGER (json)

Note: if your inline comments contain `@apiSchema` then this option won't work (use option 2). This is due to apidoc-core not supporting `apidoc-plugin-schema` at the time of writing.

By putting inline comments in the source code like this in javascript, you will get `swagger.json` file which can be served to [swagger-ui](https://github.com/swagger-api/swagger-ui) to generate html overview of documentation.

`/api/foo.js`:
```js
/**
 * @api {get} /user/id Request User information
 * @apiName GetUser
 * @apiGroup User
 *
 * @apiParam {Number} id Users unique ID.
 *
 * @apiSuccess {String} firstname Firstname of the User.
 * @apiSuccess {String} lastname  Lastname of the User.
 */
```

### EXAMPLE

`apidoc-swagger --input path_to_api_project/ --output ./nginx/www/swagger/`

### OPTION 2: 
APIDOC -> SWAGGER

For this option to work, you need to convert APIDOC_INLINE_COMMENTS_IN_CODE to APIDOC(json) yourself, for example using [apidoc.js](https://www.npmjs.com/package/apidoc)

### EXAMPLE

`apidoc-swagger --useApidocJson --input ./api_project.json --apidocDataInput ./api_data.json --output ./nginx/www/swagger/`


## Installation

`npm install @nlevo/apidoc-swagger -g`


Have a look at [apidoc](https://github.com/apidoc/apidoc) for full functionality overview and capabilities of apidoc.

To read more about how swagger works refer to [swagger-ui](https://github.com/swagger-api/swagger-ui) and [swagger-spec](https://github.com/swagger-api/swagger-spec) for details of `swagger.json`.

