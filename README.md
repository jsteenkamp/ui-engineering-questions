# UI Engineering Questions

Questions for UI engineers and Front-End developers.

## Table of Contents

1. [HTML](#html)
2. [CSS](#css)
3. [JavaScript](#javascript)
4. [Libraries](#libraries)
5. [Frameworks](#frameworks)
6. [APIs](#apis)
7. [Tools](#tools)
8. [Testing](#testing)
9. [Applications](#applications)
10. [Build and Deploy](#build-and-deploy)
11. [Process](#process)
12. [Design](#design)
13. [Person](#person)
14. [Questions](#questions)
15. [Contributing](#contributing)


## HTML

- What is HTML5?
  > New version of the language HTML, with new elements, attributes, and behaviors, and a larger set of technologies that allows more diverse and powerful Web sites and applications.

- What is your top pick, favorite feature, in HTML5?
- What are Web Components?
  > Web Components consists of several separate technologies. Web Components consists of four technologies: Custom Elements, HTML Templates, Shadow DOM, HTML Imports. Custom elements: an API for registering your own implementations for HTML elements. HTML Templates: enable you to store HTML data inside an HTML document. The content of a `<template>` element is parsed without interpreting it (no loading of images etc.). Shadow DOM: Encapsulates and hides the innards of a custom element inside a nested document. The most important part of Web Components and hardest to polyfill. HTML Imports: let you import other HTML documents into the current one. That way, HTML documents become bundles of HTML, CSS and JavaScript. You need such bundles to distribute custom elements and all of their dependencies.

- What are your thoughts on JSX?
  > JSX is a XML-like syntax extension to ECMAScript without any defined semantics. It's NOT intended to be implemented by engines or browsers. JSX is intended to be used by various preprocessors (transpilers) to transform these tokens into standard ECMAScript. JSX is an inline markup that looks like HTML and gets transformed to JavaScript. Though it looks like it, JSX isn’t a template in the sense that Handlebars and EJS are templates. It’s actually a declarative syntax that’s used to express the virtual DOM. JSX gets interpreted and converted to virtual DOM, which gets diffed against the real DOM. JSX is not limited to HTML. You can use it to create arbitrary object trees. Netflix uses that capability to mirror their web app architecture on a wide variety of devices using their own custom object model for TV rendering. React Native uses it to render device-native UI elements. In this sense, JSX is actually a lot more flexible and versatile than a template.

- ARIA / a11y?
  > WAI-ARIA, the Accessible Rich Internet Applications Suite, defines a way to make Web content and Web applications more accessible to people with disabilities.

- Icon font vs SVG?
  > Scalable Vector Graphics let you describe images as sets of vectors (lines) and shapes in order to allow them to scale smoothly regardless of the size at which they're drawn. There are big advantages to vector icons: resizable up and down without losing quality, extra sharp on retina displays, and small file size among them. Other considerations including CSS control (size, color...), positioning, weird failures, semantics, accessibility, and ease-of-use SVG wins. Fonts only win on legacy browser support (below IE8, Android 2.3).

- What is WebP?
  > WebP is a lossless and lossy compression image format developed by Google. The format was first announced in 2010 as a new open standard for lossily compressed true-color graphics on the web, producing smaller files of comparable image quality to the older JPEG scheme. WebP also supports animation, ICC profile, XMP metadata and tiling (compositing very large images from maximum 16384×16384 tiles). Google has proposed using WebP for animated images as an alternative to the popular GIF format, citing the advantages of 24-bit color with transparency, combining frames with lossy and lossless compression in the same animation, and as well as support for seeking to specific frames. Google reports a 64% reduction in file size for images converted from animated GIFs to lossy WebP, and a 19% reduction when converted to lossless WebP.

- What is WHATWG?
  > The WHATWG (Web Hypertext Application Technology Working Group) is an organization that maintains and develops HTML and APIs for Web applications. Former employees of Apple, Mozilla, and Opera established WHATWG in 2004.

- What is the DOM?
  > The Document Object Model (DOM) is a programming interface for HTML, XML and SVG documents. It provides a structured tree representation of the document and it defines a way that the structure can be accessed from programs to change the document structure, style and content. The DOM provides a representation of the document as a structured group of nodes and objects that have properties and methods. Nodes can have event handlers attached to them, and once that event is triggered the event handlers get executed. Essentially, it connects web pages to scripts or programming languages.

- What is a returned by `document.querySelectorAll('div')`?
  > Returns a NodeList object which is a collection of nodes. NodeList are used very much like arrays and it's tempting to invoke Array.prototype methods on them, however NodeList objects don't have any of the familiar Array methods. The only method NodeLists have is `item(idx)`. A NodeList prototype chain is myNodeList --> NodeList.prototype --> Object.prototype --> null, whereas the array prototype chain is myArray --> Array.prototype --> Object.prototype --> null

- How can you use array methods on a NodeList?
  > NodeLists are array-like but don't feature many of the methods provided by the Array, like `forEach`, `map`, `filter`... JavaScript provides a very simple way to convert NodeLists to Arrays.

  ```javascript
  // we use slice with no arguments to return the entire NodeList
  var nodesArray = Array.prototype.slice.call(document.querySelectorAll('div'));
  // shorter method to access array prototype
  var nodesArray = [].slice.call(document.querySelectorAll('div'));
  ```

- The DOM was designed for documents, we are building applications. Discuss.
- Discuss `console.dir(document.createElement('div'))`.
  > Creates unattached DOM element and lists its properties. Stark example of the complexity resulting from legacy standard support.

- What is `<canvas>` and WebGL?
  > The HTML `<canvas>` element can be used to draw graphics via scripting (usually JavaScript). For example, it can be used to draw graphs, make photo compositions or even perform animations. You can provide alternate content inside the `<canvas>` block that will be rendered on older browsers lacking `canvas` support and browsers with JavaScript disabled. WebGL brings 3D graphics to the Web by introducing an API that closely conforms to OpenGL ES 2.0, and which can be used in HTML `<canvas>` elements.


## CSS

- What is good about CSS? What is bad about CSS?
  > Separate visual design from markup. Browser support (no such a problem with newer evergreen web browsers), globals, managing style bleed-through...

- What are the hard problems in CSS?
  > Global namespace, dependencies, dead code elimination, minification, sharing constants, non-deterministic resolution, isolation

- What is the benefit of using `calc( … )`?
  > Allows mixing units like `%` and `px`, for example `calc(100% - 60px)`

- Specificity - discuss.
  > Selectors in descending order of specificity: inline style, id (a), class (b), attribute (b), pseudo-class(b), type (c), universal. Calculate specificity as (abc). Examples: `#sid.red:not(FOO)` = 111, `ul ol li.red` = 13

- Positioning - 4 types, discuss.
  > static, absolute, relative, fixed

- How would you keep a header bar fixed at the top of a scrolling panel?
  > Position fixed is relative to the browser window so will not work

- What is deterministic matching?
  > Applied CSS differs based on the navigation and UI interactions

- Are conventions like BEM, Atomic, SMACSS good?
  > They are not good in the sense that they rely on naming conventions. They can clutter markup with verbose class names and shift style "code" into markup. However they are the best solution that does not require additional code or tooling for solving the style encapsulation problem.

- How would you go about modularizing your CSS?
  > Container specific selectors to constrain style bleed-through, this leads to naming conventions like BEM. Other approaches are using CSS pre-processor placeholders and mixins to keep you markup generic whilst creating more specific CSS selectors. Innovative approach is using CSS Modules or some way to apply in-line styles.

- Why use a CSS pre-processor?
  > A preprocessor allows additional leverage over CSS by providing additional syntax that delivers the following advantages: Nested syntax, Ability to define variables, Ability to define mixins, Mathematical functions, Operational functions (such as “lighten” and “darken”), Joining of multiple files.

- What does `autoprefixer` do?
  > Parse CSS and add vendor prefixes to rules.

- When would you use mixins and placeholders?
  > A mixin lets you make groups of CSS declarations that you want to reuse. `@mixin border-radius($radius)` ---> `@include border-radius(10px)`. The `%placeholder` selector is used with the `@extend` directive that allows one selector to inherit the styles of another selector. `%column{ ... }` ---> `@extend %column`

- When would you use `@media`?
  > The `@media` rule is used to define different style rules for different media types/devices. In CSS2 this was called media types, while in CSS3 it is called media queries. Media queries look at the capability of the device, and can be used to check many things, such as width and height of the browser window, width and height of the device, orientation (is the tablet/phone in landscape or portrait mode?), resolution etc.

- How would you go about implementing the Holy Grail layout?
  > Use flexbox, css-tables, positioning, tables are options in descending order of preference (for modern browsers). An alternative question is what are the problems you encounter when trying to implement HG layout? These are keeping the footer positioned correctly -fixed at the bottom of the browser window if the content does not push it down, pushed down when content length exceeds browser winder height. The other common problem is displaying background color for full length of columns.

- Would you use tables for layout?
- What can a browser animate efficently?
  > Modern browsers can animate four things really cheaply: `position`, `scale`, `rotation` and `opacity`. If you animate anything else, it’s at your own risk, and the chances are you’re not going to hit a silky smooth 60fps.

- Should you use CSS or JavaScript for animation?
  > Developers often have to decide if they will animate with JavaScript (imperative) or CSS (declarative). Pro of imperative animations is also its main con: it’s running in JavaScript on the browser’s main thread. The main thread is already busy with other JavaScript, style calculations, layout and painting. Often there is thread contention. This substantially increases the chance of missing animation frames, which is the very last thing you want. Animating in JavaScript does give you a lot of control: starting, pausing, reversing, interrupting and canceling are trivial. Some effects, like parallax scrolling, can only be achieved in JavaScript. The alternative approach is to write your transitions and animations in CSS. The primary advantage is that the browser can optimize the animation. It can create layers if necessary, and run some operations off the main thread which, as you have seen, is a good thing. The major con of CSS animations for many is that they lack the expressive power of JavaScript animations. It is very difficult to combine animations in a meaningful way, which means authoring animations gets complex and error-prone.

- What are the advantages/disadvantages of using a CSS framework?
  > Some advantages are speed to build something, tested across browsers, responsive design, implement popular/accepted UI design patterns. Disadvantages are all deigns look the same, performance and size (more features than you need), lack of control performance impacting features like animation, integration may depend on additional libraries like jQuery.

- How would you select the 3rd element in a list?
  > `li:nth-child(3)`

- What are pseudo selectors?
  > A CSS pseudo-class is a keyword added to selectors that specifies a special state of the element to be selected. Examples include `:link :visited :hover :active :focus :target :enabled :disabled :first-child :last-child :nth-child()`


## JavaScript

- Why is JavaScript important? Why is it so popular/unpopular?
- What are your favorite features of the language?
- List the JavaScript primitives (5 or 6?)
  > A primitive (primitive value, primitive data type) is data that is not an object and has no methods. In JavaScript, there are 6 primitive data types: `string`, `number`, `boolean`, `null`, `undefined`, `symbol` (new in ECMAScript 2015). All primitives are immutable (cannot be changed).

- What is hoisting? What is logged to the console by this code?
  > Declaration hoisting can cause lots of debugging pains. Because variable declarations (and declarations in general) are processed before any code is executed, declaring a variable anywhere in the code is equivalent to declaring it at the top. If you reference a variable before the `var` is declared the result is `undefined`. In ES6, `let` does not hoist the variable to the top of the block. If you reference a variable in a block before the `let` declaration for that variable is encountered, this results in a `ReferenceError`, because the variable is in a "temporal dead zone" from the start of the block until the declaration is processed.

  ```javascript
  // why is myVar undefined? How would you
  var myVar = 'foo';

  (function(){
      var myVar;
      console.log(myVar); // logs undefined
      myVar = 'bar';
  })();
  ```

- What is `this`?
  > In most cases, the value of `this` is determined by how a function is called. It can't be set by assignment during execution, and it may be different each time the function is called. ES5 introduced the `bind` method to set the value of a function's `this` regardless of how it's called.

- When would you use `call(...)`, `apply(...)`, `bind(...)`?
  > The `call()` method calls a function with a given `this` value and arguments provided individually. The `apply()` method calls a function with a given `this` value and arguments provided as an array (or an array-like object). The `bind()` method creates a new function that, when called, has its `this` keyword set to the provided value, with a given sequence of arguments preceding any provided when the new function is called.

- What are closures?
  > A closure is a function that closes over the environment in which it was defined. This means it can access variables not in it's parameter list. Closures and lambdas are entirely different, although related, concepts. A lambda is simply an anonymous function.

- Why do we need Callbacks and Promises?
  > To work with asynchronous processes, typically remote requests. If you have a number of dependent (cascading) processes/requests then callbacks result in the "Pyramid of Doom" describing the indentation of nested callback functions. Promises are easier to chain together and popular implementations provide methods for collating/combining responses.  

- What is Event bubbling and event capturing?
  > Event bubbling and capturing are ways of event propagation in the DOM API. The difference is the order of the execution of the event handlers. With bubbling, the event handler on the innermost element fires first and then propagates to outer elements. With capturing, the event is first captured by the outermost element and propagated to the inner elements.

- How would you detect an Array vs an Object?
  > The key to to understand JavaScript prototype chains. For an array the prototype chain is: a ---> Array.prototype ---> Object.prototype ---> null. To detect an array vs object your code could use `instanceof` but should test for `Array` before checking for `Object`.

- How would to add and remove an item from an Array?
  > `push` adds items and `pop` removes an item from the end of an array, `unshift` adds items and `shift` remove an item from the start of an array. Adding items returns the new length of the array. Removing an item returns the item.

- What does the `map()` method do?
  > The map() method creates a new array with the results of calling a provided function on every element in this array.

  ```javascript
  var numbers = [1, 4, 9];
  var roots = numbers.map(Math.sqrt);
  // roots is now [1, 2, 3], numbers is still [1, 4, 9]
  ```

- Babel, Traceur or TypeScript?
- What is an AST?
  > An abstract syntax tree (AST) is a tree representation of the abstract syntactic structure of source code written in a programming language. Made available as a JavaScript API makes it easier to write tools in JavaScript that manipulate JavaScript source programs, such as syntax highlighters, static analyses, translators, compilers, obfuscators, etc.

- What does the `use strict` directive do?
  > Strict mode makes several changes to normal JavaScript semantics. First, strict mode eliminates some JavaScript silent errors by changing them to throw errors. Second, strict mode fixes mistakes that make it difficult for JavaScript engines to perform optimizations: strict mode code can sometimes be made to run faster than identical code that's not strict mode. Third, strict mode prohibits some syntax likely to be defined in future versions of ECMAScript.

- What is the prototype chain for an object, array, function?
  > When it comes to inheritance, JavaScript only has one construct: objects. Each object has an internal link to another object called its prototype. That prototype object has a prototype of its own, and so on until an object is reached with null as its prototype. null, by definition, has no prototype, and acts as the final link in this prototype chain. When trying to access a property of an object, the property will not only be sought on the object but on the prototype of the object, the prototype of the prototype, and so on until either a property with a matching name is found or the end of the prototype chain is reached.

  ```javascript
  var o = {a: 1};

  // The newly created object o has Object.prototype as its [[Prototype]]
  // o has no own property named 'hasOwnProperty'
  // hasOwnProperty is an own property of Object.prototype.
  // So o inherits hasOwnProperty from Object.prototype
  // Object.prototype has null as its prototype.
  // o ---> Object.prototype ---> null

  var a = ['yo', 'whadup', '?'];

  // Arrays inherit from Array.prototype
  // (which has methods like indexOf, forEach, etc.)
  // The prototype chain looks like:
  // a ---> Array.prototype ---> Object.prototype ---> null

  function f(){
    return 2;
  }

  // Functions inherit from Function.prototype
  // (which has methods like call, bind, etc.)
  // f ---> Function.prototype ---> Object.prototype ---> null
  ```

- What is Prototypal Inheritance?
  > Each object has an internal link to another object called its prototype. That prototype object has a prototype of its own, and so on until an object is reached with null as its prototype. While this is often considered to be a weaknesses, the JavaScript prototypal inheritance model is in fact more powerful than the classic model.

  ```javascript
  // How would we set up the inheritance chain, such that Bar inherits from Foo?
  function Foo() {
    console.log(‘Initializing…’);
    this.init();
  }

  Foo.prototype.init = function() {
    console.log(‘Initialized!’);
  };

  function Bar() {}

  var bar = new Bar();
  // should log ‘Initializing…’ and ‘Initialized!’
  // bonus points add an initialization property to Foo
  ```

- Which ES6/ESNext features have you used?
  > Favorite new JS features: compact object literals, destructuring, rest, spread `(x) => x*2;`

- What do you think about classes in ES6?
  > Gang of Four advice: Favor object composition over class inheritance. Large class hierarchies are brittle and become arthritic. Prototypal inheritance is simpler and more powerful. Browsers do provide some performance optimizations for class.  

- Composition vs inheritance. Discuss?
  > Composition is a type of inheritance. Classical and prototypal inheritance are fundamentally and semantically distinct. In class inheritance, instances inherit from a blueprint (the class), and create sub-class relationships. In prototypal inheritance, instances inherit from other instances. A class is a blueprint. A prototype is an object instance. Classes are not the right way to create objects in JavaScript.

- Two-way data binding is cool. Or is it?
- What is JSON? `isp`
  > JSON (JavaScript Object Notation) is a lightweight data-interchange format. It is easy for humans to read and write. It is easy for machines to parse and generate. It is based on a subset of the JavaScript Programming Language.

- What is JSONP?
  > JSONP (JSON with padding) is a communication technique used in JavaScript programs running in web browsers to request data from a server in a different domain, something prohibited by typical web browsers because of the same-origin policy. JSONP takes advantage of the fact that browsers do not enforce the same-origin policy on `<script>` tags. Since it works through `<script>` tags, JSONP supports only the `GET` request method. There are significant security implications and risks associated to using JSONP; unless you have no choice, CORS is usually the better choice.

- What do you think about Type checking and TypeScript?
- Why use `function*` when declaring a function?
  > The `function*` declaration (function keyword followed by an asterisk) defines a generator function, which returns a Generator object. Generators are functions which can be exited and later re-entered. Their context (variable bindings) will be saved across re-entrances. The `yield` keyword is used to pause and resume a generator function (`function*` or legacy generator function). The `yield*` expression is used to delegate to another generator or iterable object.

- How would you change change an HTML attribute using JavaScript?
  > First you need to find the element using `var el = document.querySelector(".myclass");` then you can set the attribute using `el.setAttribute('tabindex', 3);` Note that `querySelector()` returns the first matching element, `querySelectorAll()` returns a non-live list of elements that match the group of selectors.

- What is a `NodeList`?
  > `NodeList` objects are collections of nodes such as those returned by `Node.childNodes` and the `document.querySelectorAll` method. In some cases, the `NodeList` is a live collection, which means that changes in the DOM are reflected in the collection. For example, `Node.childNodes` is live. In other cases, the `NodeList` is a static collection, meaning any subsequent change in the DOM does not affect the content of the collection. `document.querySelectorAll` returns a static `NodeList`.

- 60fps - discuss.
  > This is about understanding the browser rendering engine and render pipeline. JavaScript -> Style -> Layout -> Paint -> Composite. Avoid CSS properties that affect Layout. Properties that affect geometry (height, width, border, margin, padding) affect Layout, Paint and Composite and are least performant. CSS in render blocking, JavaScript is parser blocking.

- Infinite scroll - discuss.
  > Memory usage is a concern. Object pooling and memory reuse is essential.

- Immutable data - discuss.
- Universal (Isomorphic) JavaScript - discuss.
- What are monomorphic calls?
  > Operations are monomorphic if the hidden classes of inputs are always the same - otherwise they are polymorphic, meaning some of the arguments can change type across different calls to the operation. JavaScript compliers can inline monomorphic functions and constructors for performance.

- Event driven, non-blocking I/O - discuss.
  > Having asynchronous I/O is good, because I/O is more expensive than most code and we should be doing something better than just waiting for I/O. The event loop handles and processes external events and converts them into callback invocations. So I/O calls are the points at which Node.js can switch from one request to another. At an I/O call, your code saves the callback and returns control to the node.js runtime environment. The callback will be called later when the data actually is available. There is no way of making code run in parallel within a single request. However, all I/O is evented and asynchronous.

- What is the _main thread_?
  > JavaScript historically suffers from an important limitation: all its execution process remains inside a unique thread. This JavaScript limitation implies that a long-running process will freeze the main window. We often say that we’re blocking the “UI Thread”. This is the main thread in charge of handling all the visual elements and associated tasks: drawing, refreshing, animating, user inputs events, etc.

- What is the _event loop_?
  > JavaScript has a concurrency model based on an "event loop". This model is quite different than the model in other languages like C or Java. JavaScript runtimes contain a message queue which stores a list of messages to be processed and their associated callback functions. These messages are queued in response to external events (such as a mouse being clicked or receiving the response to an HTTP request) given a callback function has been provided. If, for example a user were to click a button and no callback function was provided then no message would have been enqueued. In a loop, the queue is polled for the next message (each poll referred to as a “tick”) and when a message is encountered, the callback for that message is executed.

- Discuss asynchronous processing `callbacks, promises, generators/yield, async/await)`?

- What does this code do? It does not work correctly can you fix it?
  > The code creates and unordered list with 5 items and binds a `click` event to each item. Clicking an item should log the corresponding item number to the console however it always logs 5. Possible solutions include using ES6 block scope, using a closure, or using event delegation.

  ```javascript
  var list = document.createElement('UL');

  for (var i = 1; i <= 5; i++) {
    var item = document.createElement('LI');
    item.appendChild(document.createTextNode('Item ' + i));

    var j = i;
    item.onclick = function (ev) {
      console.log('Item ' + j + ' is clicked.');
    };
    list.appendChild(item);
  }

  document.querySelector('body').appendChild(list);
  ```
  
  [Gist with alternative solutions](https://gist.github.com/jsteenkamp/938ca16bc4cd2969a5c5)

## Libraries

- What is the difference between a Library and a Framework?
  > You call a library, a framework calls you. Library is utilitarian, framework is prescriptive and typically all-in (lock-in). Libraries more flexible but you have to choose, match and manage, framework less flexibility but provides a more complete solution.

- Which are your favorite libraries? (lodash, moment...)
- RxJS, Bacon, Ramda - important?
- D3 or other graphing libraries... _questions required._


## Frameworks

- Which frameworks have you used?
- We are currently using Angular. Thoughts?
- Frameworks vs micro-Frameworks vs Libraries?
- Core things you look for in a framework?
- MVC vs MVVM vs MV* - discuss.
- i18n/g11n.
- What is DI (Dependency Injection)?
  > In software engineering, dependency injection is a software design pattern that implements inversion of control for resolving dependencies. Dependency injection means giving an object its instance variables. Dependency injection separates the creation of a client's dependencies from the client's behavior, which allows program designs to be loosely coupled and to follow the dependency inversion and single responsibility principles.

- Describe your application folder structure.
- What is “scope soup” (Angular)?
- When would you use `$apply` and `$destroy` (Angular)?
- Why use directives? (Angular) Link function vs Controller? Isolate scope?
- Why do companies like Google, Facebook, Netflix release their technology as OSS?


## APIs

- REST - discuss.
  > Representational State Transfer (REST) is a software architecture style for building scalable web services. RESTful systems typically communicate over the Hypertext Transfer Protocol with the same HTTP verbs (`GET`, `POST`, `PUT`, `DELETE`, etc.) which web browsers use to retrieve web pages and to send data to remote servers. REST interfaces usually involve collections of resources with identifiers, for example `/people/joe`, which can be operated upon using standard verbs, such as `DELETE /people/joe`.

- What is the n + 1 request problem?
  >  When a request to load one item turns into n+1 requests since the item has n associated items.

- Real-time options, websockets, other?
- RAML, OData, json:api … _questions required._
- Why use jsonp? Significant limitation of jsonp?
- Postman, mocking data (Faker)
- What are your thoughts on microservices?
- Online/Offline - discuss.

## Tools

- Which IDE or editor do you use?
- Why is automation important?
  > Productivity and build integrity, both are enablers for continuous deployment/delivery. This in in turn is an enabler for iterative testing (A/B) based product development.

- Node, npm, jspm, bower ... ?
- Grunt vs Gulp vs WebPack vs jspm ... ?
  > Gulp only has 4 API commands `.src`, `.dst`, `.task`, `.watch`

- Chrome DevTools - pick a panel and discuss: Elements, Network, Sources, Timeline, Profiles, Audit, Console?
- Favorite Chrome developer plug-ins/extensions?
- Postman, Charles ...
- What are source maps?
  > JavaScript (and CSS) sources are often combined and minified to make delivering them from the server more efficient. Increasingly, too, JavaScript running in a page is machine-generated when transpiled from ES6 to ES5. By using source maps, the debugger can map the code being executed to the original source files, making debugging much, much easier.

- JSHint, ESLint, JSDoc, ESDoc
- Documentation generation
- Version control, Git
- Wiki (Confluence), Jira
- What is your favorite terminal command?
- What is the `scripts` object in `package.json` for?

## Testing

- Do you test? Why?
- Unit testing, E2E testing?
- Jasmine, Mocha, Chai, Sinon, Tape (TAP) … ?
- Karma, Protractor
- Coverage (Istanbul)
- TDD (Test Driven Development) vs WBT (Write Behind Tests)?

## Applications

- How do you build large front-end applications?
  > A good answer is you never build large applications! Looking for insights into modularity and componentization. An alternative/related question is _"how would you go about rebuilding a large legacy application using a modern web stack?"_.

- Have you adopted Style Guides?
  > Ideally you have applied style guides like Air BnB JavaScript, John Papa Angular, and CSS style guides.

- Is it important to support legacy browsers?
  > Looking for pragmatism, "if required by our target market, and weight cost of supporting old browsers against development complexity, lost opportunity to use new features...", and innovation, "ideally I would like to leverage new features where possible across current web browsers".

- How would you implement login?
  > Most developers are familiar with cookie and session based solutions. Ideally we want to hear about JSON Web Tokens (JWT) and authorization headers. Bonus point in Angular context for mention of `$http` response interceptors.

- JWT?
  > JSON Web Token (JWT) is a JSON-based open standard (RFC 7519) for passing claims between parties in web application environment. The tokens are designed to be compact, URL-safe and usable especially in web browser single sign-on (SSO) context.

- CORS?
  > Cross-site HTTP requests are HTTP requests for resources from a different domain than the domain of the resource making the request.

- CSP?
  > Content Security Policy (CSP) is an added layer of security that helps to detect and mitigate certain types of attacks, including Cross-Site Scripting (XSS) and data injection attacks. These attacks are used for everything from data theft to site defacement or distribution of malware.

- Service Worker will change front-end development. Discuss.
  > Service workers essentially act as proxy servers that sit between web applications, and the browser and network (when available.) They are intended to (amongst other things) enable the creation of effective offline experiences, intercepting network requests and taking appropriate action based on whether the network is available and updated assets reside on the server. They will also allow access to push notifications and background sync APIs.

- Have you used any NoSQL databases?
- Have you used any cloud APIs / services?
- What do you think will future applications look like?
  > Discussion. Looking for insights. Would they still use HTML, CSS and JavaScript? Would they still use the DOM, if not have we been down that road before with Flex/Flash and Silverlight plugins?

- Should a component retrieve its own data?
  > If a component is completely independent then the trade-off is the number of requests and efficient caching vs sharing a common service/API layer to marshal requests.

- OWASP top 10?
  > The OWASP Top Ten is a list of the 10 most dangerous current Web application security flaws, along with effective methods of dealing with those flaws. OWASP (Open Web Application Security Project) is an organization that provides unbiased and practical, cost-effective information about computer and Internet applications.

## Build and Deploy

- Describe your front-end application build process.
- Release trains and feature toggles - discuss.
- Versioning and semver.
  > Given a version number MAJOR.MINOR.PATCH, increment the: MAJOR version when you make incompatible API changes, MINOR version when you add functionality in a backwards-compatible manner, and PATCH version when you make backwards-compatible bug fixes. Additional labels for pre-release and build metadata are available as extensions to the MAJOR.MINOR.PATCH format.

- CI (Jenkins, Bamboo) ...?
- Docker ...

## Process

- Have you read the Agile Manifesto?
  >  Individuals and interactions over processes and tools. Working software over comprehensive documentation. Customer collaboration over contract negotiation.  Responding to change over following a plan.

- Agile / Scrum - experience, what works, what does not.
- Describe a Code Review process
- What makes an effective meeting?

## Design

- How do you contribute as part of the design process?
- Continuous design - thoughts?
- What is Responsive Design?
- What trade-offs would you make to deliver a complex UI on a small screen?

## Person

- What do you do well?
- What do you want to do?
- Any professional/career regrets?
- Why front-end / UI / JavaScript?
- How would you describe the purpose (job) of a UI Engineer?
- How do you keep up-to-date?
- Which are your favorite blogs, sites, resources, heros?
- Describe how you have worked with customers and 3rd parties.
- You have developed a good technical solution however it is rejected by your team. What do you do?
- Community involvement, projects?
- OSX, Windows, Linux?
- What motivates you?
- What is your plan? What career path?
- What questions should we have asked?


## Questions

Questions you should ask:

- What is a typical day like?
- What will I have done in 6 months from now to be successful in this job?
- What kind of person succeeds in this job and why? Are there specific personality traits you can think of?
- What kind of person fails in this job and why?
- What do you consider the most important day-to-day responsibilities of this job?
- What will be the first projects I tackle?
- What are the biggest challenges the department faces this year? What will my role as a team member be in addressing them?
- What are the challenges you are facing right now?

An astute candidate will seek immediate feedback:

- Are there any weaknesses in my candidacy that I can address right now?


## Contributing

- To contribute questions, answers and rankings issue a [Pull Request](https://help.github.com/articles/using-pull-requests/).
- Questions may include resources such as images and links. Images should not be wider than 730px for README.
- Succinct answers, ideally a couple of lines are preferable. This can be followed by a detailed explanation and links for further reading as appropriate.
