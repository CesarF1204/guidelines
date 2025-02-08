# JavaScript Coding Guidelines 

We should follow Airbnb JavaScript coding guidelines, not entirely but a lot of it. If a link to a section in Airbnb coding guideline is provided it means the whole section must be followed. 

Read more: https://github.com/airbnb/javascript

## Spaces/Tabs/Indention
Always set your code editor to use 4 spaces for tabs.

```javascript
//bad
if (isHidden === true) {
	// do something
} else if(isHidden === false && isDeleted === true) {
	// do something
} else {
	// do something
}

//good 
if(isHidden === true){
	// do something
} 
else if(isHidden === false && isDeleted === true){
	// do something
}
else{
	// do something
}

//bad
const getUserData = function getUserData ( user_id, api_key ) {
	return //result of do something; 
}

//good
const getUserData = function getUserData(user_id, api_key){
	return //result of do something; 
}
```
</br>
</br>

## Variables and Constants 

###  Declaring Constants
When declaring constants, make sure to group them by category into objects instead of declaring them by separate variables. 

```javascript
//bad
/* USER LEVEL CODES */
    Constants.SUPER_ADMIN = 0;
    Constants.AGENCY = 1;
    Constants.EMPLOYEE = 2;

//good 
const USER_LEVELS = {
    super_admin: 0, 
    agency: 1,
    employee: 2,
};
```

Use Constants to avoid confusing codes with direct values and make the code more readable. 

```javascript
//bad
if(result.value === 1){
	// some code
}

//good
if(result.value === CONSTANTS.USER_LEVELS.super_admin){
	// some code
}
```
Read and follow: https://github.com/airbnb/javascript#references
</br>
</br>

### Declaring Variables 
Read and follow: https://github.com/airbnb/javascript#variables.

Avoid declaring a variable and eventually putting a value on it with a different Data Type. 
In the bad code example below, noticed how **correct_answer_count** which initially stores an integer value eventually contained an object. 
Yes, this will work, but it's a pain for other devs who will eventually read and work on top of your code. Do not do this. 

```javascript
let correct_answer = 10;                        

if(correct_answer_count === undefined){					            
    correct_answer = { total_score: 0, question: {} };
} 
```
#### PBR Trap

Be careful of pass by reference behaviour of JavaScript Objects.
When you declare an object variable (OBJ1) and passed that as a value of another variable (OBJ2).
The value of OBJ2 is the value of OBJ1. However, when you change the value of OBJ2 or update a property of it, the changes are also reflected in OBJ1.  

This is critical because, when overlooked, this results in unnecessary passing of values and could also lead to memory leaks. 
We will use JS spread operator to solve this. Read more at https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_syntax. 

```javascript
//pass by referenced example
let employee = {name: "Cesar Francisco"};
let person = employee;
person.name = "Luan Akio";
console.log(person.name); //value is Luan Akio
console.log(employee.name); //value is Luan Akio as well, not Cesar Francisco

//how to avoid passed by reference behaviour 
let employee = {name: "Cesar Francisco"};
let person = {...employee};
person.name = "Luan Akio";
console.log(person.name); //value is Luan Akio
console.log(employee.name); //value is still Cesar Francisco
```

### Cases
When to use CamelCase or snake_case? 

Class names for controllers, models, and imported/required modules uses camelcase with Uppercase first letter. 
Methods/functions inside a Class uses camelcase with lowercase first letter.

```javascript
import DatabaseModel from "./database-query-model/lib/database.model";

class AgencyController {

    constructor(){
    }
    

   /** 
    * DOCU: This function is to fetch agency data. 
    * This is being called on employees.controller.js <br>
    * Last Updated Date: February 08, 2025 <br>
    * @function
    * @param {integer} agency_id - id of the agency
    * @author Cesar, Updated by: Kath
    */
    fetchAgencies = async (agency_id) => {
        let response_data = { status: false, result: [], error: null };

        try{
```
> Additional rule here, in loading dependencies, load third party first, then load configs/helpers, then lastly models. 

Normal variables use snake case all in lowercase
> Note also to add space after opening curly-brace `{` and before closing curly-brace `}`

```javascript
const response_data = { status: false, result: {}, error: null };
const has_transaction_started = false;
```
</br>
</br>

## Arrays
```javascript
const items = []; /* declaration of new array */
items.push('item1'); /* inserting a new value */
```
Read and follow: https://github.com/airbnb/javascript#arrays
</br>
</br>

## Objects
Read more: https://github.com/airbnb/javascript#objects

Use the literal syntax for object creation

```javascript
// bad
const item = new Object();

// good
const item = {};
```

## Destructuring
```javascript
const users = [user1, user2, user3];

// bad
const user1 = users_result[0];
const user2 = users_result[1];
const user3 = users_result[2];

// good
const [user1, user2, user3] = users;
```
```javascript
// bad
function getFullName(user) {
  const firstName = user.firstName;
  const lastName = user.lastName;

  return `${firstName} ${lastName}`;
}

// good
function getFullName(user) {
  const { firstName, lastName } = user;
  return `${firstName} ${lastName}`;
}

// best
function getFullName({ firstName, lastName }) {
  return `${firstName} ${lastName}`;
}
```

Read and follow: https://github.com/airbnb/javascript#destructuring
</br>
</br>

## Strings 
Read more: https://github.com/airbnb/javascript#strings

Use single quotes '' for strings.
```javascript
// bad
const name = "Capt. Janeway";

// bad - template literals should contain interpolation or newlines
const name = `Capt. Janeway`;

// good
const name = 'Capt. Janeway';
```


Strings that cause the line to go over 100 characters should not be written across multiple lines using string concatenation.
```javascript
// bad
const errorMessage = 'This is a super long error that was thrown because \
of Batman. When you stop to think about how Batman had anything to do \
with this, you would get nowhere \
fast.';

// bad
const errorMessage = 'This is a super long error that was thrown because ' +
  'of Batman. When you stop to think about how Batman had anything to do ' +
  'with this, you would get nowhere fast.';

// good
const errorMessage = 'This is a super long error that was thrown because of Batman. When you stop to think about how Batman had anything to do with this, you would get nowhere fast.';
```

When programmatically building up strings, use template strings instead of concatenation.
```javascript
// bad
function sayHi(name) {
  return 'How are you, ' + name + '?';
}

// bad
function sayHi(name) {
  return ['How are you, ', name, '?'].join();
}

// bad
function sayHi(name) {
  return `How are you, ${ name }?`;
}

// good
function sayHi(name) {
  return `How are you, ${name}?`;
}
```

</br>
</br>

## Iterators 
```javascript
// bad
// forEach is much slower than for-loop, for-in, for-of
let total_rating = 0;
ratings_response.forEach((rating_response) => {
	total_rating += rating_response.rating;
});
```

```javascript
// good
let total_rating = 0;
for(let i=0; i<ratings_response.length; i++){
	total_rating += ratings_response[i].rating;
}
```

```javascript
// best
let total_rating = 0;
for(let index in ratings_response){
	let rating_response = ratings_response[index];

	total_rating += rating_response.rating;
	...
}
```
</br>
</br>

## Conditions and Comparison Operators 
If/else statements
```javascript
if(result.status === true){
	...
}
else{
	...
}
```
Read and follow: 
https://github.com/airbnb/javascript#control-statements /
https://github.com/airbnb/javascript#comparison-operators--equality

### Ternary
#### Nullish Coalescing Operator  
Simplified way of checking if variable is not undefined or not null. 
Read more https://javascript.info/nullish-coalescing-operator. 

```javascript
//normal approach 
const b = (a !== null && a !== undefined) ? a : c;

//better approch 
const b = a ?? c; 
```

We can also use a sequence of ?? to select the first value from a list that isn’t null/undefined.

```javascript
const a = null;
const b = undefined; 
const c = 20; 
const d = 0;
const x = a ?? b ?? c ?? d; //the value of x will be 20 
const y = a ?? b ?? d ?? c; //the value of y will be 0; 
```

Read also about || operator for ternary. https://javascript.info/nullish-coalescing-operator#comparison-with. 
The important difference between them is that: || returns the first truthy value. ?? returns the first defined value.

So in the example above, if we replace ?? with ||
```javascript
const y = a || b || d || c; //the value of y will be 20 since 'd' has value of 0 which is evaluated as false; 
```

#### Optional Chaining 
Simplifying long ternary for checking possible non-existing/undefined property of an object. 
Read more https://javascript.info/optional-chaining. 

```javascript
// normal approach
const street_address =  (user.address != undefined && user.address.street != undefined) ? user.address.street : undefined;

// better approach using Optional chaining '?.'
const street_address = user?.address?.street; 
```
</br>
</br>


## Functions 
Read more on https://github.com/airbnb/javascript#functions. 
Read and understand all sections related to functions, do not skip. 
 
If you are passing Objects as parameters, you should be very careful in re-assinging values of the object. Read more on Deep vs Shallow Copy of an object. 
https://www.javascripttutorial.net/object/3-ways-to-copy-objects-in-javascript/

## Classes & Constructors
Read and follow: https://github.com/airbnb/javascript#classes--constructors

### Modules
Read and follow: https://github.com/airbnb/javascript#modules

### Accessors
Read and follow: https://github.com/airbnb/javascript#accessors

### Properties
Read and follow: https://github.com/airbnb/javascript#properties
</br>
</br>


## Code Standards for Models and Controllers 

### File Naming

1. Always name files base on their purpose (e.g. based on page for controllers, tables for models, goal to accomplish for scripts). 

2. For scripts, DO NOT call any model function from the main code base, instead just create a copy of the function directly in the script. In short, make the main code base be totally separate from scripts as we don't want to be tied up in maintaining all scripts as the main code base also progresses. 
</br>

### Declaraing Classes 
Declare models and controllers as classes and always add constructor. 
```javascript
class SampleController {
    constructor(){
        ...
    }

    getRecordById = async function(req, res = undefined){
        ...
    }
}

export default (function sample_controller(){
    return new SampleController();
})();
```
</br>

### Importing Constants and Helpers

For importing constants to a controller or model, just put or import the required constants in controller or model. Same too with the helpers, only import the needed helper functions. Moving forward, we should avoid using 'require', use import instead. 

```javascript
//constants
import { 
    USER_LEVELS 
} from "../config/constants";

//helpers
import { timeDifference } from "../helpers";
```
</br>

### Use async/await and try/catch
Avoid having nested callbacks because it's not easy to read or maintain.  Read the following articles:
  * Callback hell: http://callbackhell.com/
  * Making asynchronous programming easier with [async and await](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Asynchronous/Async_await)

Your **controller methods** would need to look like this when using async and await. On as needed basis, try/catch can also be used in controller methods but it's more utilized in the models.

```javascript
import User from "../models/User";

const getUsers = async (req, res) => {
  try {
    const users = await User.find();
    res.status(200).json(users);
  } catch (error) {
    res.status(500).json({ message: "Error fetching users", error });
  }
};

export { getUsers };
```
</br>

## Comment Guidelines

### Document your code, add meaningful comments

Aside from readable codes, detailed comments on every function and complex codes are required to be added. Pull Request with poor documentation or comments will not be approved. 

For each function, write a brief description that would help other developrs as well as yourself. For complex parts of the code within functions, add explanation on how the code works, provide details that other devs should know. 

### Comment Types
- DOCU - discuss how the code works. 
- BUG – a known bug that should be corrected.
- FIXME – should be corrected, problematic or misguiding code.
- TEMP_FIX – a workaround or temporary fix.
- TODO – something to be done.

### Comment Format

Use /* instead of // for comments to avoid issues on code precompile. 

##### A good or acceptable DOCU comment would include the ff: 
1. Concise and clear explanation of the purpose of the function.
2. What feature/page/function triggers or call the funtion. 
3. What are the required parameters for the function to work. 
4. Owner of the function and who updated it recently. 

**Good documentation of a function**
> There should be comments in every function. And also using the appropriate way. This is the first step for us to practice in preparation for us to use the JSDoc later on.
    
```javascript
/**
* DOCU: This function is used to fetch all group employee list. <br>
* This is being called on /accounts/group-employee route. <br>
* Last Updated Date: January 27, 2025 <br>
* @function
* @param {object} req - request
* @param {object} res - response
* @author Cesar
*/
const groupEmpList = asyncHandler(async (req, res) => {
  try {
```

**Good documentation of codes within function**
> For one liner within the function comments, no need to add the label DOCU. 
```javascript
    const user = req.user;
    /* Check if user is present */
    if (!user) throw new Error("Unauthorized");

    /* Get needed data from request query */
    const { groupId, page, search } = req.query;

    /* Check if groupId is present */
    if (!groupId) throw new Error("Group Id is required.");
    
    /* Call getGroupEmployee function to get employees data */
    const employees = await getGroupEmployee(groupId, page, search);
```

**More examples on other comment types** 
```javascript
/* TODO: Revise implementation, upload a single file instead of uploading multiple files. */
uploadFile = async (post_data, is_submit = false) => {
```

```javascript
/* TEMP_FIX: Temporary solution while waiting for Feature X,Y,Z to be implemented. */
employeeExamFiles = async (post_data, is_submit = false) => {
```