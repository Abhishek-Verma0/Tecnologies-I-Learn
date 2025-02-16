### What is CSS BEM?
The BEM methodology is a naming convention for CSS classes in order to keep CSS more maintainable by defining namespaces to solve scoping issues. BEM stands for Block Element Modifier which is an explanation for its structure. A Block is a standalone component that is reusable across projects and acts as a "namespace" for sub components (Elements). Modifiers are used as flags when a Block or Element is in a certain state or is different in structure or style.
```
/* block component */
.block {
}

/* element */
.block__element {
}

/* modifier */
.block__element--modifier {
}
```
Here is an example with the class names on markup:
```
<nav class="navbar">
  <a href="/" class="navbar__link navbar__link--active"></a>
  <a href="/" class="navbar__link"></a>
  <a href="/" class="navbar__link"></a>
</nav>
```
In this case, navbar is the Block, navbar__link is an Element that makes no sense outside of the navbar component, and navbar__link--active is a Modifier that indicates a different state for the navbar__link Element.

Since Modifiers are verbose, many opt to use is-* flags instead as modifiers.
```
<a href="/" class="navbar__link is-active"></a>
```
These must be chained to the Element and never alone however, or there will be scope issues.
```
.navbar__link.is-active {
}
```
### What is the difference between the equality operators == and ===?

Triple equals (===) checks for strict equality, which means both the type and value must be the same. Double equals (==) on the other hand first performs type coercion so that both operands are of the same type and then applies strict comparison.

- Whenever possible, use triple equals to test equality because loose equality == can have unintuitive results.

- Type coercion means the values are converted into the same type.

- Mention of falsy values and their comparison.

### What is the difference between an element and a component in React?

An element is a plain JavaScript object that represents a DOM node or component. Elements are pure and never mutated, and are cheap to create.

A component is a function or class. Components can have state and take props as input and return an element tree as output (although they can represent generic containers or wrappers and don't necessarily have to emit DOM). Components can initiate side effects in lifecycle methods (e.g. AJAX requests, DOM mutations, interfacing with 3rd party libraries) and may be expensive to create.
```
const Component = () => "Hello"
const componentElement = <Component />
const domNodeElement = <div />
```
- Elements are immutable, plain objects that describe the DOM nodes or components you want to render.

- Components can be either classes or functions, that take props as an input and return an element tree as the output.

### Can you name the four types of @media properties?

- all, which applies to all media type devices
- print, which only applies to printers
- screen, which only applies to screens (desktops, tablets, mobile etc.)
- speech, which only applies to screenreaders

### What is the difference between the postfix i++ and prefix ++i increment operators?

Both increment the variable value by 1. The difference is what they evaluate to.

The postfix increment operator evaluates to the value before it was incremented.
```
let i = 0
i++ // 0
// i === 1
```
The prefix increment operator evaluates to the value after it was incremented.
```
let i = 0
++i // 1
// i === 1
```

### How do you write comments inside a JSX tree in React?
Hide answer
Comments must be wrapped inside curly braces {} and use the /* */ syntax.
```
const tree = (
  <div>
    {/* Comment */}
    <p>Text</p>
  </div>
)
```

### What is a stateful component in React?

A stateful component is a component whose behavior depends on its state. This means that two separate instances of the component if given the same props will not necessarily render the same output, unlike pure function components.
```
// Stateful class component
class App extends Component {
  constructor(props) {
    super(props)
    this.state = { count: 0 }
  }
  render() {
    // ...
  }
}

// Stateful function component
function App() {
  const [count, setCount] = useState(0)
  return // ...
}
```

- Stateful components have internal state that they depend on.

- Stateful components are class components or function components that use stateful Hooks.

- Stateful components have their state initialized in the constructor or with useState().

### What is a stateless component?

A stateless component is a component whose behavior does not depend on its state. Stateless components can be either functional or class components. Stateless functional components are easier to maintain and test since they are guaranteed to produce the same output given the same props. Stateless functional components should be preferred when lifecycle hooks don't need to be used.

- Stateless components are independent of their state.

- Stateless components can be either class or functional components.

- Stateless functional components avoid the this keyword altogether.

### What is the purpose of callback function as an argument of setState?

The callback function is invoked when setState has finished and the component gets rendered. Since setState is asynchronous, the callback function is used for any post action.
```
setState({ name: "sudheer" }, () => {
  console.log("The name has updated and component re-rendered")
})
```
- The callback function is invoked after setState finishes and is used for any post action.

- It is recommended to use lifecycle method rather this callback function.

### Why does React use className instead of class like in HTML?

React's philosophy in the beginning was to align with the browser DOM API rather than HTML, since that more closely represents how elements are created. Setting a class on an element meant using the className API:
```
const element = document.createElement("div")
element.className = "hello"
```
Additionally, before ES5, reserved words could not be used in objects:
```
const element = {
  attributes: {
    class: "hello"
  }
}
```
In IE8, this will throw an error.

In modern environments, destructuring will throw an error if trying to assign to a variable:
```
const { class } = this.props // Error
const { className } = this.props // All good
const { class: className } = this.props // All good, but cumbersome!
```
However, class can be used as a prop without problems, as seen in other libraries like Preact. React currently allows you to use class, but will throw a warning and convert it to className under the hood. There is currently an open thread (as of January 2019) discussing changing className to class to reduce confusion.

### How do you clone an object in JavaScript?

Using the object spread operator ..., the object's own enumerable properties can be copied into the new object. This creates a shallow clone of the object.
```
const obj = { a: 1, b: 2 }
const shallowClone = { ...obj }
```
With this technique, prototypes are ignored. In addition, nested objects are not cloned, but rather their references get copied, so nested objects still refer to the same objects as the original. Deep-cloning is much more complex in order to effectively clone any type of object (Date, RegExp, Function, Set, etc) that may be nested within the object.

Other alternatives include:

- JSON.parse(JSON.stringify(obj)) can be used to deep-clone a simple object, but it is CPU-intensive and only accepts valid JSON (therefore it strips functions and does not allow circular references).
- Object.assign({}, obj) is another alternative.
- Object.keys(obj).reduce((acc, key) => (acc[key] = obj[key], acc), {}) is another more verbose alternative that shows the concept in greater depth.

- JavaScript passes objects by reference, meaning that nested objects get their references copied, instead of their values.

- The same method can be used to merge two objects.


### What is the difference between em and rem units?

Both em and rem units are based on the font-size CSS property. The only difference is where they inherit their values from.

- em units inherit their value from the font-size of the parent element
- rem units inherit their value from the font-size of the root element (html)

In most browsers, the font-size of the root element is set to 16px by default.

### What are truthy and falsy values in JavaScript?

A value is either truthy or falsy depending on how it is evaluated in a Boolean context. Falsy means false-like and truthy means true-like. Essentially, they are values that are coerced to true or false when performing certain operations.

There are 6 falsy values in JavaScript. They are:

- false
- undefined
- null
- "" (empty string)
- NaN
- 0 (both +0 and -0)

Every other value is considered truthy.

A value's truthiness can be examined by passing it into the Boolean function.
```
Boolean("") // false
Boolean([]) // true
```
There is a shortcut for this using the logical NOT ! operator. Using ! once will convert a value to its inverse boolean equivalent (i.e. not false is true), and ! once more will convert back, thus effectively converting the value to a boolean.
```
!!"" // false
!![] // true
```
### What is the difference between the array methods map() and forEach()?

Both methods iterate through the elements of an array. map() maps each element to a new element by invoking the callback function on each element and returning a new array. On the other hand, forEach() invokes the callback function for each element but does not return a new array. forEach() is generally used when causing a side effect on each iteration, whereas map() is a common functional programming technique.


- Use forEach() if you need to iterate over an array and cause mutations to the elements without needing to return values to generate a new array.

- map() is the right choice to keep data immutable where each value of the original array is mapped to a new array.
### How does hoisting work in JavaScript?

Hoisting is a JavaScript mechanism where variable and function declarations are put into memory during the compile phase. This means that no matter where functions and variables are declared, they are moved to the top of their scope regardless of whether their scope is global or local.

However, the value is not hoisted with the declaration.

The following snippet:
```
console.log(hoist)
var hoist = "value"
```
is equivalent to:
```
var hoist
console.log(hoist)
hoist = "value"
```
Therefore logging hoist outputs undefined to the console, not "value".

Hoisting also allows you to invoke a function declaration before it appears to be declared in a program.
```
myFunction() // No error; logs "hello"
function myFunction() {
  console.log("hello")
}
```
But be wary of function expressions that are assigned to a variable:
```
myFunction() // Error: `myFunction` is not a function
var myFunction = function() {
  console.log("hello")
}
```

- Hoisting is JavaScript’s default behavior of moving declarations to the top

- Functions declarations are hoisted before variable declarations

### What are inline conditional expressions?

Since a JSX element tree is one large expression, you cannot embed statements inside. Conditional expressions act as a replacement for statements to use inside the tree.

For example, this won't work:
```
function App({ messages, isVisible }) {
  return (
    <div>
      if (messages.length > 0) {
        <h2>You have {messages.length} unread messages.</h2>
      } else {
        <h2>You have no unread messages.</h2>
      }
      if (isVisible) {
        <p>I am visible.</p>
      }
    </div>
  )
}
```
Logical AND && and the ternary ? : operator replace the if/else statements.
```
function App({ messages, isVisible }) {
  return (
    <div>
      {messages.length > 0 ? (
        <h2>You have {messages.length} unread messages.</h2>
      ) : (
        <h2>You have no unread messages.</h2>
      )}
      {isVisible && <p>I am visible.</p>}
    </div>
  )
}
```

### What are the lifecycle methods in React?

- getDerivedStateFromProps: Executed before rendering on the initial mount and all component updates. Used to update the state based on changes in props over time. Has rare use cases, like tracking component animations during the lifecycle. There are only few cases where this makes sense to use over other lifecycle methods. It expects to return an object that will be the the new state, or null to update nothing. This method does not have access to the component instance either.

- componentDidMount: Executed after first rendering and here all AJAX requests, DOM or state updates, and set up eventListeners should occur.

- shouldComponentUpdate: Determines if the component will be updated or not. By default, it returns true. If you are sure that the component doesn't need to render after state or props are updated, you can return a false value. It is a great place to improve performance as it allows you to prevent a rerender if component receives new prop.

- getSnapshotBeforeUpdate: Invoked right after a component render happens because of an update, before componentDidUpdate. Any value returned from this method will be passed to componentDidUpdate.

- componentDidUpdate: Mostly it is used to update the DOM in response to prop or state changes.

- componentWillUnmount: It will be used to cancel any outgoing network requests, or remove all event listeners associated with the component.

- componentDidCatch: Used in error boundaries, which are components that implement this method. It allows the component to catch JavaScript errors anywhere in the child component tree (below this component), log errors, and display a UI with error information.

### What are Promises?

The Promise object represents the eventual completion (or failure) of an asynchronous operation, and its resulting value. An example can be the following snippet, which after 100ms prints out the result string to the standard output. Also, note the catch, which can be used for error handling. Promises are chainable.
```
new Promise((resolve, reject) => {
  setTimeout(() => {
    resolve("result")
  }, 100)
})
  .then(console.log)
  .catch(console.error)
```

### What is a cross-site scripting attack (XSS) and how do you prevent it?
Hide answer
XSS refers to client-side code injection where the attacker injects malicious scripts into a legitimate website or web application. This is often achieved when the application does not validate user input and freely injects dynamic HTML content.

For example, a comment system will be at risk if it does not validate or escape user input. If the comment contains unescaped HTML, the comment can inject a ```<script>``` tag into the website that other users will execute against their knowledge.

- The malicious script has access to cookies which are often used to store session tokens. If an attacker can obtain a user’s session cookie, they can impersonate the user.
- The script can arbitrarily manipulate the DOM of the page the script is executing in, allowing the attacker to insert pieces of content that appear to be a real part of the website.
- The script can use AJAX to send HTTP requests with arbitrary content to arbitrary destinations.

- On the client, using textContent instead of innerHTML prevents the browser from running the string through the HTML parser which would execute scripts in it.

- On the server, escaping HTML tags will prevent the browser from parsing the user input as actual HTML and therefore won't execute the script.
### What is event-driven programming?

Event-driven programming is a paradigm that involves building applications that send and receive events. When the program emits events, the program responds by running any callback functions that are registered to that event and context, passing in associated data to the function. With this pattern, events can be emitted into the wild without throwing errors even if no functions are subscribed to it.

A common example of this is the pattern of elements listening to DOM events such as click and mouseenter, where a callback function is run when the event occurs.
```
document.addEventListener("click", function(event) {
  // This callback function is run when the user
  // clicks on the document.
})
```
Without the context of the DOM, the pattern may look like this:
```
const hub = createEventHub()
hub.on("message", function(data) {
  console.log(`${data.username} said ${data.text}`)
})
hub.emit("message", {
  username: "John",
  text: "Hello?"
})
```
With this implementation, on is the way to subscribe to an event, while emit is the way to publish the event.
### What is the only value not equal to itself in JavaScript?

NaN (Not-a-Number) is the only value not equal to itself when comparing with any of the comparison operators. NaN is often the result of meaningless math computations, so two NaN values make no sense to be considered equal.


The difference between isNaN() and Number.isNaN()

const isNaN = x => x !== 

### **_What is an error-first callback?_**

The pattern used across all the asynchronous methods in Node.js is called _Error-first Callback_. Here is an example:

```javascript
fs.readFile("file.json", function (err, data) {
  if (err) {
    console.error(err)
  }
  console.log(data)
})
```

Any asynchronous method expects one of the arguments to be a callback. The full callback argument list depends on the caller method, but the first argument is always an error object or null. When we go for the asynchronous method, an exception thrown during function execution cannot be detected in a try/catch statement. The event happens after the JavaScript engine leaves the try block.

In the preceding example, if any exception is thrown during the reading of the file, it lands on the callback function as the first and mandatory parameter.

### Why express js is required when I have node.js

So you don't have to repeat same code over and over again. Node.js is a low-level I/O mechanism which has an HTTP module. If you just use an HTTP module, a lot of work like parsing the payload, cookies, storing sessions (in memory or in Redis), selecting the right route pattern based on regular expressions will have to be re-implemented. With Express.js it there for you to use.

#### Middleware functions allow you to take action on any incoming request and modify it before sending back a response. Each piece of middleware is just another request handler.

The difference between node.js and express.js is in the level of abstraction:

Node.js is a platform for building server-side event-driven i/o application using javascript.

Express.js is a framework based on node.js for building web-application using principles and approaches of node.js
### Cookie-Based Authentication

Cookie-based authentication has been the default, tried-and-true method for handling user authentication for a long time.

#### Cookie-based authentication is **stateful**. This means that an authentication record or session must be kept both server and client-side. The server needs to keep track of active sessions in a database, while on the front-end a cookie is created that holds a session identifier, thus the name cookie based authentication. Let's look at the flow of traditional cookie-based authentication:

User enters their login credentials.
Server verifies the credentials are correct and creates a session which is then stored in a database.
A cookie with the session ID is placed in the users browser.
On subsequent requests, the session ID is verified against the database and if valid the request processed.
Once a user logs out of the app, the session is destroyed both client-side and server-side.

###Token-Based Authentication

Token-based authentication has gained prevalence over the last few years due to the rise of single page applications, web APIs, and the Internet of Things (IoT). When we talk about authentication with tokens, we generally talk about authentication with JSON Web Tokens (JWTs). While there are different ways to implement tokens, JWTs have become the de-facto standard. With this context in mind, the rest of the article will use tokens and JWTs interchangeably.

#### Token-based authentication is **stateless**. The server does not keep a record of which users are logged in or which JWTs have been issued. Instead, every request to the server is accompanied by a token which the server uses to verify the authenticity of the request. The token is generally sent as an addition Authorization header in the form of Bearer {JWT}, but can additionally be sent in the body of a POST request or even as a query parameter. Let's see how this flow works:

- User enters their login credentials.
- Server verifies the credentials are correct and generates and returns a signed token.
- This token is stored client-side, most commonly in local storage - but can be stored in session storage or a cookie as well.
- Subsequent requests to the server include this token as an additional Authorization header or through one of the other methods mentioned above.
- The server decodes the JWT and if the token is valid processes the request.
- Once a user logs out, the token is destroyed client-side, no interaction with the server is necessary.

### Advantages of Token-Based Authentication

Understanding how something works is only half the battle. Next, we'll cover the reasons why token authentication is preferable over the traditional cookie-based approach.

### Stateless, Scalable, and Decoupled

Perhaps the biggest advantage to using tokens over cookies is the fact that token authentication is stateless. The back-end does not need to keep a record of tokens. Each token is self-contained, containing all the data required to check it's validity as well as convey user information through claims.

The server's only job, then, becomes to sign tokens on a successful login request and verify that incoming tokens are valid. In fact, the server does not even need to sign tokens. Third party services such as Auth0 can handle the issuing of tokens and then the server only needs to verify the validity of the token.

### Cross Domain and CORS

Cookies work well with singular domains and sub-domains, but when it comes to managing cookies across different domains, it can get hairy. In contrast, a token-based approach with CORS enabled makes it trivial to expose APIs to different services and domains. Since the JWT is required and checked with each and every call to the back-end, as long as there is a valid token, requests can be processed. There are a few caveats to this and we'll address those in the Common Questions and Concerns section below.

### Store Data in the JWT

With a cookie based approach, you simply store the session id in a cookie. JWT's, on the other hand, allow you to store any type of metadata, as long as it's valid JSON. The JWT spec specifies different types of claims that can be included such as reserved, public and private. You can learn more about the specifics and the differences between the types of claims on the jwt.io website.

In practice, what this means is that a JWT can contain any type of data. Depending on your use case you may choose to make the minimal amount of claims such as the user id and expiration of the token, or you may decide to include additional claims such as the user's email address, who issued the token, scopes or permissions for the user, and more.

### Performance

When using the cookie-based authentication, the back-end has to do a lookup, whether that be a traditional SQL database or a NoSQL alternative, and the round trip is likely to take longer compared to decoding a token. Additionally, since you can store additional data inside the JWT, such as the user's permission level, you can save yourself additional lookup calls to get and process the requested data.

For example, say you had an API resource /api/orders that retrieves the latest orders placed via your app, but only users with the role of admin have access to view this data. In a cookie based approach, once the request is made, you'd have one call to the database to verify that the session is valid, another to get the user data and verify that the user has the role of admin, and finally a third call to get the data. On the other hand, with a JWT approach, you can store the user role in the JWT, so once the request is made and the JWT verified, you can make a single call to the database to retrieve the orders.

### JWT Size

The biggest disadvantage of token authentication is the size of JWTs. A session cookie is relatively tiny compared to even the smallest JWT. Depending on your use case, the size of the token could become problematic if you add many claims to it. Remember, each request to the server must include the JWT along with it.

### Where to Store Tokens?

With token-based auth, you are given the choice of where to store the JWT. Commonly, the JWT is placed in the browser's local storage and this works well for most use cases. There are some issues with storing JWTs in local storage to be aware of. Unlike cookies, local storage is sandboxed to a specific domain and its data cannot be accessed by any other domain including sub-domains. **Because localStorage works on same-origin policy. So, data stored will only be available on the same origin.**

You can store the token in a cookie instead, but the max size of a cookie is only 4kb so that may be problematic if you have many claims attached to the token. Additionally, you can store the token in session storage which is similar to local storage but is cleared as soon as the user closes the browser.

### XSS and XSRF Protection

Protecting your users and servers is always a top priority. One of the most common concerns developers have when deciding on whether to use token-based authentication is the security implications. Two of the most common attack vectors facing websites are Cross Site Scripting (XSS) and Cross-Site Request Forgery (XSRF or CSRF).

Cross Site Scripting) attacks occur when an outside entity is able to execute code within your website or app. The most common attack vector here is if your website allows inputs that are not properly sanitized. If an attacker can execute code on your domain, your JWT tokens are vulnerable.

XSS attacks are much easier to deal with compared to XSRF attacks because they are generally better understood. Many frameworks, including Angular, automatically sanitize inputs and prevent arbitrary code execution. If you are not using a framework that sanitizes input/output out-of-the-box, you can look at plugins like caja developed by Google to assist. Sanitizing inputs is a solved issue in many frameworks and languages and I would recommend using a framework or plugin vs building your own.

#### Cross Site Request Forgery attacks are not an issue if you are using JWT with local storage.

On the other hand, if your use case requires you to store the JWT in a cookie, you will need to protect against XSRF. XSRF are not as easily understood as XSS attacks. Luckily, preventing XSRF attacks is a fairly simple matter. To over-simplify, protecting against an XSRF attack, your server, upon establishing a session with a client will generate a unique token (note this is not a JWT). Then, anytime data is submitted to your server, a hidden input field will contain this token and the server will check to make sure the tokens match. Again, as our recommendation is to store the JWT in local storage, you probably will not have to worry about XSRF attacks.

#### Luckily, preventing XSRF attacks is a fairly simple matter. To over-simplify, protecting against an XSRF attack, your server, upon establishing a session with a client will generate a unique token (note this is not a JWT). Then, anytime data is submitted to your server, a hidden input field will contain this token and the server will check to make sure the tokens match. Again, as our recommendation is to store the JWT in local storage, you probably will not have to worry about XSRF attacks.

### Ways to protect token

1> One of the best ways to protect your users and servers is to have a short expiration time for tokens. That way, even if a token is compromised, it will quickly become useless.

2> Additionally, you may maintain a blacklist of compromised tokens and not allow those tokens access to the system.

3> Finally, the nuclear approach would be to change the signing algorithm, which would invalidate all active tokens and require all of your users to log in again. This approach is not easily recommended, but is available in the event of a severe breach.

### Tokens Are Signed, Not Encrypted

A JSON Web Token is comprised of three parts: the header, payload, and signature. The format of a JWT is header.payload.signature. If we were to sign a JWT with the HMACSHA256 algorithm, the secret 'shhhh' and the payload of:

```
{
"sub": "1234567890",
"name": "Ado Kukic",
"admin": true
}
```

The JWT generated would be:

eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkFkbyBLdWtpYyIsImFkbWluIjp0cnVlLCJpYXQiOjE0NjQyOTc4ODV9.Y47kJvnHzU9qeJIN48_bVna6O0EDFiMiQ9LpNVDFymM

#### The very important thing to note here is that this token is signed by the HMACSHA256 algorithm, and the header and payload are Base64URL encoded, it is not encrypted. If I go to jwt.io, paste this token and select the HMACSHA256 algorithm, I could decode the token and read its contents. Therefore, it should go without saying that sensitive data, such as passwords, should never be stored in the payload.

#### If you must store sensitive data in the payload or your use case calls for the JWT to be obscured, you can use JSON Web Encryption (JWE). JWE allows you to encrypt the contents of a JWT so that it is not readable by anyone but the server. JOSE provides a great framework and different options for JWE and has SDKs for many popular frameworks including NodeJS and Java.

