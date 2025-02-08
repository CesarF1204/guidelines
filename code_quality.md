
# JSDoc 
> What is JSDoc?
JSDoc is a documentation generator that is used for the Javascript language, we can compare it with Javadoc (JAVA) or PHPDocumentor (PHP) among others, JSDoc what it does is analyze all the Javascript code and AUTOMATICALLY 🤯 generates a static page (HTML) with All the documentation. JSDoc is easy to integrate with any IDE or Code Editor.

## How to install JSDoc

1. Run `npm install --save jsdoc`
2. In the root folder, on the same file level of Package.json, create and save jsdoc configs on a new JSON file. *On this example, I named the file as jsdoc_conf.json.*

```javascript
{
    "plugins": [],
    "recurseDepth": 10,
    "source": {
        "exclude": ["node_modules"],
        "includePattern": ".+\\.js(doc|x)?$",
        "excludePattern": "(^|\\/|\\\\)_"
    },
    "sourceType": "module",
    "tags": {
        "allowUnknownTags": true,
        "dictionaries": ["jsdoc","closure"]
    },
    "templates": {
        "cleverLinks": false,
        "monospaceLinks": false,
        "sort": false
    }
}
```

3. In **package.json**, add the code below to scripts. Pattern will be `/jsdoc -d <folder where to save generated API documents> --configure jsdoc_conf.json -r {your project folder}`
    *Example:*
    `"doc": "./node_modules/.bin/jsdoc -d docs --configure jsdoc_conf.json -r ../011-skillura-backend"`

4. Run `npm install` to apply the newly added script for generating JavaScript API Documentation.
5. Run `npm run doc` to generate the JavaScript API Documentation.
> Note that you need to run this when there is a change in the comments.

##### Sample codes
*Module*
```javascript
/**
 * @module UserModel
 */
```

*Classes*
```javascript
/** 
 * @class 
 * Class representing User Controller
 */
class EmployeeController {
    
    constructor(){
        ...
    }
}
```

*Methods*
> Documentation must be enclosed by `/**` and `*/`, then new lines should be started by `*`

```javascript
/** 
* DOCU: This function is used to fetch employees <br>
* This is being called on employees.controller.js <br>
* Last Updated Date: February 08, 2025 <br>
* @function
* @param {integer} employee_id - id of the employee
* @param {object} agency - agency data { agency_id, agency_name }
* @author Raymund, Updated by: Cesar
*/
```

Indicate the default value of parameter by adding `=value` after the parameter.
> @param {integer} page - page=1

If you want a code that should never appear in the documentation use the **@ignore** tag

> If you use the @ignore tag with the @class or @module tag, the entire class or module will be omitted from the documentation

> If you use the @ignore tag with the @namespace tag, you must also add the @ignore tag to any child classes and namespaces. Otherwise, your documentation will show the child classes and namespaces, but with incomplete names.

There is also way to add a ToDo for any function/method/class using the **@todo** tag.
```javascript
@todo Add more documentation
```

**Links**
- https://alligator.io/js/jsdoc/https://alligator.io/js/jsdoc/
- https://medium.com/@imanol_suarez/jsdoc-what-is-that-1d2aa10d9635
- https://github.com/SAP/openui5/blob/master/docs/guidelines/jsdoc.md (Additional JSDoc Guidelines)