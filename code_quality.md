
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
<br>
<br>

# Better Comments Plugin
- A powerful tool that enhances your code commenting experience by enabling different styles and formats to enhance productivity by making comments more meaningful and noticeable.

### Features
- Categorize comments with different colors for better readability.
- Supports highlighting TODOs, questions, warnings, and other custom tags.

### Installation
1. Open VS Code.
2. Go to Extensions Marketplace (Ctrl+Shift+X).
3. Search for Better Comments.
4. Click Install.
5. Restart VS Code (if needed).

### Usage
The plugin categorizes comments based on specific symbols:
| Symbol | Purpose        | Example |
|--------|--------------|---------|
| `*`    | Important    | `/* * This is an important comment */` |
| `!`    | Warning      | `/* ! This is a warning` */ |
| `?`    | Question     | `/* ? This is a question` */ |
| `TODO` | Task Reminder | `/* TODO: Fix this bug` */ |
| `@`    | Highlight    | `/* @ This is a highlighted note` */ |


### Example Usage in JavaScript
```javascript
/* * This is an important comment */
/* ! This is a warning */
/* ? This is a question that needs an answer */
/* TODO: Refactor this function */
/* @ Highlight this section for review */
function example() {
    console.log("Better Comments Plugin in action!");
}
```

### Customizing Better Comments
To modify the colors and styles, follow these steps:

1. Open **Settings** (`Ctrl + ,`).
2. Search for `Better Comments`.
3. Adjust colors and comment styles as needed.

### Benefits of Using Better Comments
- Improves code readability.
- Helps in organizing tasks and warnings.
- Makes code reviews more efficient.
<br>
<br>


# Using Prettier in VS Code
**Prettier** is a code formatter that ensures consistent code style across your projects. It helps maintain clean and consistent code, improving collaboration and readability.

## Installation
To install Prettier in VS Code, follow these steps:

1. Open **VS Code**.
2. Go to the **Extensions Marketplace** (`Ctrl + Shift + X`).
3. Search for **Prettier - Code formatter**.
4. Click **Install**.
5. Reload or restart VS Code if necessary.

### Configuring Prettier as the Default Formatter
To set Prettier as your default formatter:

1. Open **Settings** (`Ctrl + ,`).
2. Search for `editor.defaultFormatter`.
3. Select **Prettier - Code formatter**.
4. Enable format on save by searching for `editor.formatOnSave` and checking the box.

### Basic Usage
Prettier can format code manually or automatically:

- **Format on Save:** Enable `editor.formatOnSave` in settings.
- **Manual Formatting:** Press `Shift + Alt + F`.
- **Format a Selection:** Highlight code and press `Ctrl + K Ctrl + F`.

### Customizing Prettier
Prettier can be customized using a `.prettierrc` file in your project root. Example:

```json
{
  "singleQuote": true,
  "trailingComma": "es5",
  "tabWidth": 2,
  "semi": false
}
```

You can also configure settings in `settings.json` inside VS Code.

### Ignoring Files
To ignore specific files, create a `.prettierignore` file:

```
node_modules/
build/
dist/
*.min.js
```

### Benefits of Using Prettier
- Ensures **consistent code formatting**.
- Supports multiple programming **languages and frameworks**.
- Integrates with **ESLint** for additional linting.
- Saves time by **automating formatting**.
<br>
<br>

# DRY (Don't Repeat Yourself) Principle in Software Development
The DRY (Don't Repeat Yourself) principle is a fundamental concept in software development that encourages reducing code duplication to improve maintainability, scalability, and readability. It promotes reusability by using functions, modules, or libraries to handle repetitive tasks.

## Why Follow DRY?
- Reduces redundancy
- Simplifies maintenance
- Enhances code readability
- Improves scalability
- Reduces the chances of errors

## Implementing DRY in MERN (MongoDB, Express, React, Node.js)

### Example 1: Using Helper Functions in Express (Node.js)
Instead of writing the same logic multiple times, we can create a helper function.

#### ❌ Without DRY:
```javascript
app.get("/users", async (req, res) => {
    const users = await User.find();
    res.json(users);
});

app.get("/posts", async (req, res) => {
    const posts = await Post.find();
    res.json(posts);
});
```

#### ✅ With DRY (Using a Helper Function):
```javascript
const fetchData = async (Model, res) => {
    try {
        const data = await Model.find();
        res.json(data);
    } catch (error) {
        res.status(500).json({ error: error.message });
    }
};

app.get("/users", (req, res) => fetchData(User, res));
app.get("/posts", (req, res) => fetchData(Post, res));
```

### Example 2: Reusable React Components
Instead of writing similar UI components multiple times, create a reusable component.

#### ❌ Without DRY:
```jsx
const PrimaryButton = () => (
    <button style={{ backgroundColor: "blue", color: "white", padding: "10px" }}>Click Me</button>
);

const SecondaryButton = () => (
    <button style={{ backgroundColor: "gray", color: "black", padding: "10px" }}>Click Me</button>
);
```

#### ✅ With DRY (Using a Reusable Component):
```jsx
const Button = ({ label, bgColor, textColor }) => (
    <button style={{ backgroundColor: bgColor, color: textColor, padding: "10px" }}>
        {label}
    </button>
);

<Button label="Primary" bgColor="blue" textColor="white" />
<Button label="Secondary" bgColor="gray" textColor="black" />
```

### Example 3: Using Middleware in Express
Middleware can be used to avoid repeating authentication logic in multiple routes.

#### ❌ Without DRY:
```javascript
app.get("/dashboard", async (req, res) => {
    const token = req.headers.authorization;
    if (!token) return res.status(401).json({ message: "Unauthorized" });
    // Token validation logic here...
    res.json({ message: "Welcome to Dashboard" });
});

app.get("/profile", async (req, res) => {
    const token = req.headers.authorization;
    if (!token) return res.status(401).json({ message: "Unauthorized" });
    // Token validation logic here...
    res.json({ message: "Welcome to Profile" });
});
```

#### ✅ With DRY (Using Middleware):
```javascript
const authenticate = (req, res, next) => {
    const token = req.headers.authorization;
    if (!token) return res.status(401).json({ message: "Unauthorized" });
    // Token validation logic here...
    next();
};

app.get("/dashboard", authenticate, (req, res) => {
    res.json({ message: "Welcome to Dashboard" });
});

app.get("/profile", authenticate, (req, res) => {
    res.json({ message: "Welcome to Profile" });
});
```

Applying the DRY principle makes your code more maintainable, reduces errors, and improves efficiency. By using helper functions, reusable components, and middleware, you can significantly enhance the quality of your MERN applications.
