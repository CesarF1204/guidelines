Session/POST Management

#### Avoid Storing Sensitive Information in Sessions
Ensure that no sensitive data is stored in session variables. If an attacker gains access to someone else's session data in Hacker Hero, they should not be able to exploit it. Do not store sensitive details such as credit card information, passwords, or any other personal data in the session—even if encrypted.

#### Prevent Session Hijacking
- Always encrypt session data using a unique encryption key for each user.
- Ensure the site operates over HTTPS to protect session integrity.
- While the following link provides methods to enhance security against session hijacking, it does not completely eliminate the risk: [Session Hijacking and How to Prevent It](https://www.freecodecamp.org/news/session-hijacking-and-how-to-stop-it-711e3683d1ac/).

#### Enhance Security for Form/POST Data
- Do not blindly trust incoming data from forms or POST requests. Attackers can manipulate this data using browser developer tools or browser extensions.
- Before passing data from the controller to the model, the controller should filter and validate inputs, allowing only the necessary parameters required by the model. This helps minimize security vulnerabilities.
<br>
<br>

#### We can use express-validator package (https://www.npmjs.com/package/express-validator)
Read more: https://express-validator.github.io/docs
#### Installation
```
npm install express-validator
```
Basic Usage:
#### 1. Import express-validator and create validation rules
*path: `/utils/validationRules.js`*
```javascript
import { check } from "express-validator";

/**
* DOCU: This is set of rules for validating input fields for account sign-in <br>
* This is being called when user wants to sign in. <br>
* Last Updated Date: February 08, 2025 <br>
* @function
* @author Cesar
*/
const signInValidationRules = [
    /* Validate fields */
    check('email')
        .isEmail().withMessage('Invalid email address'),
    check('password')
        .isLength({ min: 6 }).withMessage('Password should be at least 6 characters long')
];

export { signInValidationRules };
```

#### 2. Add signInValidationRules as a middleware in routes.
```javascript
import express from 'express';
import { signIn } from '../controllers/userController.js';
import { signInValidationRules } from '../utils/validationRules.js';

/* Route for user's login */
router.post('/sign_in', signInValidationRules, signIn);

export default router;
```

#### 3. Use validationResult from express-validator in controller.
```javascript
import User from '../models/User.js';
import { validationResult } from "express-validator";

/**
* DOCU: This function is used to handle the user's login. <br>
* This is being called when user is logging in. <br>
* Last Updated Date: February 08, 2025 <br>
* @function
* @param {object} req - request
* @param {object} res - response
* @author Cesar
*/
const signIn = async (req, res) => {
    try {
        /* Handle validation errors */
        const errors = validationResult(req);
        if (!errors.isEmpty()) {
            return res.status(400).json({ message: errors.array().map(error => error.msg) });
        }
...
```
<br>

Using express-validator helps ensure user-submitted data is correct, secure, and meets predefined rules before processing. By using built-in and custom validation methods, developers can easily check for required fields, enforce formats (e.g., email, numbers), and sanitize inputs to prevent security risks like SQL injection and XSS. With express-validator, you can streamline validation logic, improve code maintainability, and enhance the overall security of your application.
