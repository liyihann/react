# React - A JavaScript library for building user interfaces

<div align="center"><img src="https://ws1.sinaimg.cn/large/006tNbRwly1fwzmderuurj318g0exjtc.jpg" alt="react" width="70%" /></div>

By [Li Yihan](https://github.com/liyihann), [Cao Zixuan](https://github.com/caozixuan), [Zhang Dake](https://github.com/RickyZhang1998) and [Cai Hongyang](https://github.com/LuvMeReal)

Wuhan University, 2018

## Abstract
React is a declarative, efficient, and flexible JavaScript library for building user interfaces which allow developers compose complex UIs from components. It was initially created for the development of Facebook. Lately, it was found easy and convenient to use so that it had its first initial public release. And in this document, we will take a look at React from the shallower to the deeper. At first, we show the stakeholders to React. Then we analyze its architecture more vividly from several perspectives including context view, development view, deployment view, functional view, and performance & scalability perspective. Also, we use tools to evaluate technical debt of React. At last, the whole process of React evolution is indicated in the last part of the article.
## Table of Contents

- [1. Introduction](#1)
- [2. Stakeholders](#2)
  - [2.1 Stakeholder Roles](#2.1)
  - [2.2 Power Interest Grid](#2.2)
- [3. Context View](#3)
  - [3.1 System Scope and Responsibilities](#3.1)
  - [3.2 External Entities](#3.2)
- [4. Development View](#4)
  - [4.1 Design Principle](#4.1)
  - [4.2 Code Organization](#4.2)
  - [4.3 Module Organization](#4.3)
- [5. Deployment View](#5)
  - [5.1 Third-party Software Requirements](#5.1)
  - [5.2 Specialist Knowledge](#5.2)
- [6. Functional View](#6)
  - [6.1 Functionalities](#6.1)
  - [6.2 Extensibility](#6.2)
- [7. Performance Perspective](#7)
- [8. Technical Debt](#8)
  - [8.1 Static Analysis](#8.1)
  - [8.2 Testing Debt](#8.2)
- [9. Evolution Perspective](#9)
- [10. Conclusion](#10)
- [11. References](#11)

<h2 id="1">1. Introduction</h2>

Raised in F8 by Facebook in 2014, React is an open-source JavaScript library for building user interfaces in Web Programming. React is commonly used in the development of UI, which focuses on the View part in the traditional MVC Model. It is narrow in scope and tightly focused. It's known for three features: declarative, component-based and applicable in a wide range of fields.

React provides a method of declarative programming. Simplified grammar can still generate efficient and interactive UIs. React efficiently handles DOM manipulations through a Virtual DOM using an algorithm which determines the optimal set of manipulations based upon the changes needed.

Components developed using React can be highly encapsulated and reusable. You are recommended to break down a larger component into many small components which can be reused.

A new XML-like syntax named JSX is introduced in order to make modification on React components much more straightforward. Furthermore, React is flexible and provides hooks that enable users to interface with other libraries and frameworks.

Nowadays, React is widely used in business. The users include Zhihu, Instagram and so on. What's more, this project on GitHub has over 1,200 contributors and nearly 100 releases. There is an increasing number of web developers who are willing to use this library and help promote the development of React.

<h2 id="2">2. Stakeholders</h2>

To start with an analysis of its architecture, we talk about stakeholders to React as an open source and widely used project. Nick Rozanski and Eoin Woods gave an definition for stakeholder as follows:<a href="#ref_sta1">[1]</a>

> A stakeholder in a software architecture is a person, group, or entity with an interest in or concerns about the realization of the architecture.

Different types of stakeholders have different requirements and influences on the project. As an open source project, the category boundaries of React's stakeholders may not be very clear. Actually, our team member sent an e-mail to the manager of ReactJS core team, [@Sophie Alpert](https://github.com/sophiebits), expecting some extra information, which got such reply as follows:

> We don't typically have a formal division of responsibilities between the different stakeholder classes you have listed. For example, everyone on the team acts as a communicator, developer, maintainer, support, and tester from time to time. People have the chance to choose what to work on based on whatever is pressing and what they find interesting.  
>
> React as a project is not wholly owned by Facebook, but the most active contributors (what we think of as the "core team") are all employed by Facebook and paid full time to work on React using Facebook's funds.

However, in order to more fully understand the roles of stakeholders to React, we will still classify and analyze the various roles according to the classification method of Rozanski and Woods below.

<h3 id="2.1">2.1 Stakeholder Roles</h3>

Rozanski and Woods classified stakeholders as ten roles according to their roles and concerns: ``Acquirers``, `` Assessors``, ``Communicators``, ``Developers``, ``Maintainers``, ``Suppliers``, ``Support staff``, ``System administrators``, ``Testers`` and ``Users``. Here, we analyze each of these stakeholder groups based on the actual situation of this project. 

Although there are a large number of brilliant and passionate developers that contributed to React, in order to specify stakeholder roles of React more clearly and more intuitively, we will mainly discuss the core team members here. They are:

[@Andrew Clark](https://github.com/acdlite), [@Dan Abranmov](https://github.com/gaearon), [@Brian Vaughn](https://github.com/bvaughn), [@Dominic Gannaway](https://github.com/trueadm), [@Brandon Dail](https://github.com/aweary) and [@Flarnie Marchan](https://github.com/flarnie)

<div align="center"><img src="https://ws1.sinaimg.cn/large/006tNbRwgy1fx2yjutsm0j315u0p07pr.jpg" alt="stakeholders" width="100%" /><i><b>Figure1</b>  Stakeholders of React</i></div>

#### Acquirers

Acquirers oversee the procurement of the system or product.

React was started by [@Jordan Walke](https://github.com/jordwalke), a Facebook software engineer, in 2011. However, this project is not wholly owned by Facebook. This project relies on Facebook's funds and other sources. [@Sophie Alpert](https://github.com/sophiebits) is the first open source contributor to React, and now the manager of ReactJS at Facebook, who manages fundings for the product. She can represent the commercial interests of users in negotiating with third-party suppliers and can also be investor representation in this group if a specific external investment is required to fund the project. 

#### Assessors

Assessors oversee the system’s conformance to standards and legal regulation.

The members of the core team are responsible for checking whether the pull-requests meet the standards of the Code of Conduct adopted by Facebook. In this case, assessors come from React’s Core Team instead of external legal entities.

#### Communicators

Communicators explain the system to other stakeholders via its documentation and training materials.

Communicators usually explain the rationale behind and details of the architecture to technical and ordinary users. In this case, the whole project is put on GitHub, where people can view codes freely. Every time when there is a new version released, the README file will be updated simultaneously so that we can learn about the new features of this version. What’s more, other stakeholders can follow the official React blog [@reactjs]( https://twitter.com/reactjs) on Twitter for the latest news about React.

#### Developers

Developers are those people who construct and deploy the system from specifications. 

From this point of view, all the contributors of React code hub can be considered as developers. When we talk about the developers of React, we first should know the development of React. 

Back in 2011, the developers at Facebook started to face some issues with code maintenance. When Facebook needed to come up with a good solution for it,  Jordan Walke worked on the prototype and created React. Later, some employees of Facebook keep building the React. 

In 2013, Jordan Walke introduced React. Its expansion was quick, and more and more developers from big companies such as Netflix and Twitter joined.

In summary, React's initial developer is Jordan Walke along with his colleagues. With the popularity of React developing, more and more community developers join.

#### Maintainers

Maintainers manage the evolution of the system once operational. 

In React, the React core teams work as maintainers. They discuss the development direction of React and they accept and review pull-requests. From GitHub contributors, we view the main contributors and find those programmers who work for React core team. 

Here are the major maintainers:[@Andrew Clark](https://github.com/acdlite), [@Dan Abranmov](https://github.com/gaearon), [@Brian Vaughn](https://github.com/bvaughn), [@Dominic Gannaway](https://github.com/trueadm), [@Brandon Dail](https://github.com/aweary) and [@Flarnie Marchan](https://github.com/flarnie).

#### Suppliers

Suppliers build or supply the hardware, software or infrastructure on which the system will run. The build of React relies on many other dependencies. We just list the most important ones.<a href="#ref_sup1">
</a>

**Node.js**: It is an open-source, cross-platform JavaScript run-time environment that executes JavaScript code outside of a browser. This project is governed by the Node.js Foundation and is facilitated by the Linux Foundations' Collaborative Projects program.

**Art**: It is a retained mode vector drawing API designed for multiple output modes. This open-source project is also built by Facebook.

**Babel**: It is a tool that helps programmers write code in the latest version of JavaScript.

**Webpack**: It is an open-source JavaScript module bundler. Its main purpose is to bundle JavaScript files for usage in a browser, yet it is also capable of transforming, bundling, or packaging just about any resource or asset.

**http-server**: It is a simple, zero-configuration command-line HTTP server. It is powerful enough for production usage, but it's simple and hackable enough to be used for testing, local development, and learning.

**dagre**: Dagre is a JavaScript library that makes it easy to lay out directed graphs on the client-side.

#### Support staff

Support staff is those who provide support to users for the product or system when it is running. 

As we have mentioned above, React is an open source project on [Github](https://github.com/facebook/react). Every member of the core team acts as a technical support. If users have any bug to report or question to ask, they can feel free to open an issue on the [issue page](https://github.com/facebook/react/issues) of the project on Github as long as they follow the contributing guidelines. After that, the developers of the core team will notice it and give their suggestions.

#### System administrators

System administrators run the system once it has been deployed.

React is an open source Javascript framework which can be downloaded and used by everyone on their website or other projects. After the system has been deployed, it is users themselves that are in charge of the administration of the whole project. For individual users, that is, web developers themselves are very likely to administrate the system. For team users or corporate users, it is more likely to have a specified person to act as the system administrator. They will focus on a wide range of concerns, such as system monitoring and management, business continuity, disaster recovery, availability, resilience, and scalability. 

#### Testers

Since React is an open-source library and has been posted on the Github, a huge number of programmers have the access to test it. Therefore it is tested by the staff of React and the contributors on the Github. When bugs are found, they can send emails or issue them on the Github for the staff to solve.

#### Users

As we know, React is a JavaScript Library for building users interfaces. Thus, every student or programmer who is a front-end engineer may find it convenient and easy to build an interface.

<h3 id="2.2"> 2.2 Power Interest Grid</h3>

The following figure shows the power versus interest relation of the stakeholders of the React:

<div align="center"><img src="https://ws1.sinaimg.cn/large/006tNbRwgy1fx2ykc16esj30ye0mg464.jpg" alt="Power Interest Grid" width="100%" /><i><b>Figure2</b>  Power interest grid of React</i></div>

- **Low power, low interest**: GitHub and npm are stakeholders that have no control over the management of  React, nor do they directly benefit from it.
- **Low power, high interest**: Users, community developers and competitors to React are stakeholders that are greatly affected by the changes in React, but they have no power to influence the system. Also, Facebook provides funds for this project and is also an interest-related party.
- **High power, low interest**: Dependencies and suppliers provide React with necessary library and tools to develop and install. React will not affect their interests to a certain degree, but on the contrary, their changes will directly affect the development of React.
- **High power, high interest**: Core team and acquirers of the project are stakeholders that have significant interest and power in the development of React.

<h2 id="3">3. Context View</h2>

Now we will take a look into the details of React. This section shows the relations, platforms, dependencies and external entities that React uses. By reading the analysis graph you can get a clear view of the interactions of React.

### 3.1 System Scope and Responsibilities

According to the creation and development of React that has been written in its official [website,](https://reactjs.org/) we can learn that React was initially created to make it more efficient and easier for web developers to re-render applications.

> React is a library for building composable user interfaces. It encourages the creation of reusable UI components which present data that changes over time. 

It is commonly used in user interfaces developing, focusing on the View part in the traditional MVC Model. However, React is not just an MVC framework. The author([@Pete Hunt](https://twitter.com/floydophone)) described the features of React on the [blog](https://reactjs.org/blog/2013/06/05/why-react.html) as follows:

> - React isn't an MVC framework.
> - React doesn't use templates.
> - Reactive updates are dead simple.
> - HTML is just the beginning.

React functions concentratedly in the UI scope and its usage is clear and efficient. It has the following three aspects of responsibilities in general:<a href="#ref_con1">[3]</a>

- **Declarative**: Enabling users to create interactive UIs in a painless and efficient way. 
- **Component-Based**: Enabling users to build encapsulated components that manage their own state, then compose them to make complex UIs.
- **Learn Once, Write Anywhere**: Enabling users to develop new features in React without rewriting existing code.

These responsibilities of React provides users a more predictable and easier way to code and debug. It is widely used by a large number of independent developers and organizations in various fields. 

### 3.2 External Entities

The following figure shows the external entities surrounding React's environment and their relationships.

<div align="center"><img src="https://ws3.sinaimg.cn/large/006tNbRwgy1fx2yl9bt9wj31980o0tjk.jpg" alt="external entities" width="100%" /><i><b>Figure3</b>  External entities of React</i></div>

With this figure, we can clearly see external entities of React.

React is...

- programmed in: JavaScript
- [developed with](https://reactjs.org/community/debugging-tools.html)：[React Developer Tools](https://github.com/facebook/react-devtools)...
- continuous integration and coverage testing with：[CircleCI](https://circleci.com/gh/facebook/react), [Coveralls](https://coveralls.io/github/facebook/react?branch=master)
- developed by：core team & community developers（GitHub）
- versioning&issue tracking：git、[GitHub](https://github.com/facebook/react)、[npm](https://www.npmjs.com/package/react)
- runs on：Windows，OS X， Linux（cross-platform）
- supported by：browsers(chrome、ie、Firefox...)Node.js
- [dependencies](https://github.com/liyihann/react/network/dependencies)：loose-envify, object-assign, prop-types, schedule
- communicated via：[StackOverflow](https://stackoverflow.com/questions/tagged/reactjs)、[DEV’s React community](https://dev.to/t/react)、[Hashnode’s React community](https://hashnode.com/n/reactjs)、[React Discuss](https://discuss.reactjs.org/)、[Reactflux online chat](https://discord.gg/0ZcbPKXt5bZjGY5n)、[Reddit’s React community](https://www.reddit.com/r/reactjs/)、[Spectrum’s React community](https://spectrum.chat/react)
- licensed by：[MIT](https://github.com/facebook/react/blob/master/LICENSE)
- [used by](https://github.com/facebook/react/wiki/Sites-Using-React)：Facebook, Instagram, Twitter, Wordpress....
- competed against：Vue, Angular...
- funded by: Facebook

<h2 id="4">4. Development View</h2>

This section describes the architecture that supports React development process. First, we will describe principles and guidelines that govern the development of React. This will be followed by React code and module organizaton.

### 4.1 Design Principle

Since React is an open-source JavaScript library, everybody is free to contribute to the repository on GitHub. In order to maintain the reliability and technical cohesion of the system, core developers wrote several design principles of React itself (not React components or applications) so that contributors can have a better idea of how they decide what React does and what React doesn’t do.<a href="#ref_dev1">[4]</a>

#### Composition

The key feature of React is the composition of components which include rendering, lifecycle, and state. Components written by different people should work well together. It is important to add functionality to a component without causing rippling changes throughout the codebase.

#### Stability

API stability is highly valued. Many companies, including Facebook, Twitter, and Airbnb, are heavy users of React. Therefore, it's better not to change public APIs or behavior. However, stability doesn't mean “nothing changes”. Instead, it is interpreted in the sense of “It is heavily used in production, and when something changes, there is a clear (and preferably automated) migration path”.

#### Interoperability

It is important to React that any product team can start using React for a small feature rather than rewrite their code to bet on it. This is why React provides escape hatches to work with mutable models and tries to work well together with other UI libraries. Users can wrap an existing imperative UI into a declarative component, and vice versa. This is crucial for gradual adoption.

#### Scheduling

React is a library for building user interfaces instead of a generic data processing library. If something is offscreen, we can delay any logic related to it. If data is arriving faster than the frame rate, we can coalesce and batch updates. We can prioritize work coming from user interactions (such as an animation caused by a button click) over less important background work (such as rendering new content just loaded from the network) to avoid dropping frames.
Even when your components are described as functions, when you use React you don’t call them directly but let React call it. It means React has the power to delay calling it if necessary. This is a subtle distinction but a powerful one. 

#### Developer Experience

Providing a good developer experience is important to React. For example, React maintains React DevTools which let users inspect the React component tree in Chrome and Firefox. 

#### Debugging

If users see something wrong on the screen, they can open React DevTools, find the component responsible for rendering, and then see if the props and state are correct. This ability to trace any UI to the data that produced it in the form of current props and state is very important to React. It is an explicit design goal that state is not “trapped” in closures and combinators, and is available to React directly.

#### Implementation

React is looking for an implementation that is correct, performant and affords a good developer experience. Elegance is secondary. Verbose code that is easy to move around, change and remove is preferred to elegant code that is prematurely abstracted and hard to change.

#### Optimized for Tooling

In order to make the points of interaction with the library highly visible, some commonly used APIs have verbose names, such as `componentDidMount()` instead of `didMount()` or `onMount()`. Since in a massive codebase like Facebook, being able to search for uses of specific APIs is very important. Distinct verbose names are highly valued, especially for the features that should be used sparingly. 

#### Dogfooding

Dogfooding means that React's vision stays sharp and has a focused direction going forward. Actually, picking a small audience and focusing on making them happy brings a positive net effect. Solving the problems encountered by Facebook product teams first allows React to develop much more efficiently. 

### 4.2 Code Organization

The following figure shows the organization of React's code in four sections.

<div align="center"><img src="https://ws3.sinaimg.cn/large/006tNbRwgy1fx2ylr55d1j314s0min0n.jpg" alt="codeline" width="100%" /><i><b>Figure4</b>  Code organization of React</i></div>

#### Functionality

The functionality part contains the components that are responsible for functions of the project. Generally, `packages` contains the main and fundamental part of the codes. The `react` directory inside `packages` is the core components of all the codes. It has the essential functions and works together with `react-dom` and `react-native`. And  `react-art`  is a JavaScript library used for creating vector graph. The package `react-dom`  serves as the entry point to the DOM and server renderers for React. It is intended to be paired with the generic React package, which is shipped as `react` to ``npm``. What's more, the `scripts` directory contains files that provide additional functions to React.

#### Development and Deployment

The development and deployment section contains code that is used in the complement and development of React. They are mainly used in developing React rather than affecting the functionality of React. The directory `fixtures`  includes the test examples of React. The `art` directory contains the test examples of vector controls. The `attribute-behavior` tests every property that the controls may bring. The rest of the directories have various testing functions.

#### Documentation

The documentation section contains codes used to demonstrate and generate the documentation of React.  They are often written in Markdown. For example, `README.md`  contains the usage and instructions of using React and `CHANGELOG.md`  contains the development progress of React.

#### Miscellaneous

The miscellaneous section contains the rest of the code that doesn't belong to any directory. There are several script documents are there.

### 4.3 Module Organization

React has some relatively independent modules. These modules can be used out of React to build a web page, but their main purpose is working together to build a React web page.

React's module organization is showed below. 

<div align="center"><img src="https://i.imgur.com/DOGWbWr.png" alt="module" width="100%" /><i><b>Figure5</b> Module organization of React</i></div>

**react-dom**: This module serves as the entry point to the DOM. This is the fundamental part of React. All the elements of React are organized by react-dom which makes the updating of pages more efficient.

**react**: This module contains the functionality necessary to define React elements, instances, and components. It is the core part of React and interacts with other modules to finally form a web page.

**events**: This module contains how React handle with events which happen on the web page.

**tool-kit**: It is a set of useful tools that React develops for us to build a web page.**create-subscription ** is a utility for subscribing to external data sources inside React components. **react-art** is a module for drawing vector graphics using React. **react-is** allows you to test arbitrary values and see if they're a particular React element type. **schedule** is a module for cooperative scheduling in a browser environment.

**react-rendered**: When using React to build applications, we always have a step to render the build or virtual DOM elements to the real DOM, to hand the task to the browser, and then to lay out and paint.

**react-reconciler**: It is an experimental module for creating custom React renderers.


<h2 id="5">5. Deployment View</h2>

According to Rozanski and Woods<a href="#ref_sta1">[1]</a>, the deployment view describes the environment where the system will be deployed.

In this case, React actually runs on the server side. It depends on several third-party software to realize its functions to render the web page on the client side. For the client side, customers can choose any web browser as long as it supports the corresponding version of JavaScript and HTML that React uses. While on the server side, React is a cross-platform product since it runs on Node.js, which is a cross-platform runtime environment in JavaScript for developing web applications on the server side. 

<div align="center"><img src="https://i.imgur.com/03HfA17.jpg" alt="Deployment View" width="100%" /><i><b>Figure6</b>  Deployment environment and dependencies of React</i></div>

### 5.1 Third-party Software Requirements

**Node.js**: Node.js is an open-source, cross-platform JavaScript run-time environment that executes JavaScript code outside of a browser. It is similar to JVM for Java.

**npm**:npm is a package manager for the JavaScript programming language. It is the default package manager for the JavaScript runtime environment Node.js.

**loose-envify**: loose-envify is a JavaScript package which is used to selectively replace Node-style environment variables with plain strings.

**object-assign**:object-assign is a JavaScript package which is used to merge JavaScript objects. 

**prop-types**:prop-types is a JavaScript package which is used to examine the type of JavaScript variables.

**schedule**: schedule  is a JavaScript package which is used for cooperative scheduling in a browser environment.

What's more, here are some recommended web browsers, Chrome, Firefox, Safari, and IE10 including later versions. And Facebook has also offered us some useful tools to develop using React. For example, we can use "create-react-app" to build a development environment for React automatically without complex configuration.

### 5.2 Specialist Knowledge

- Basic knowledge of programming in JavaScript
- Familiar with web programming:HTML, CSS, Web Model, etc.

If you have basic knowledge in both fields, you are good to go in the realm of React.

<h2 id="6">6. Functional View</h2>

In this section, we will discuss the most important and unique functionalities of React. This will involve the main roles, functions features, internal implementations, and usage for developers of these functionalities, which are closely related to the architecture of the entire project. We will also analyze extensibility of React related to these functionalities.

### 6.1 Functionalities
#### JSX

**JSX** is a syntax extension to **JavaScript**. JSX is recommended to be used with React in order to describe what the UI is like. JSX produces React "elements". It is more like a template language, but it has the full power of JavaScript.<a href="#ref_func0">[5]</a>

> JSX gets compiled to `React.createElement()` calls which return plain JavaScript objects called "React elements". To get a basic introduction to JSX, see the docs here and find a more in-depth tutorial on JSX here.
>
> React DOM uses camelCase property naming convention instead of HTML attribute names. For example, `tabindex` becomes `tabIndex` in JSX. The attribute `class` is also written as `className` since `class` is a reserved word in JavaScript:

We can use JSX in the following way:

```jsx
const name = 'Clementine';
ReactDOM.render(
<h1 className="hello">My name is {name}!</h1>,
               document.getElementById('root')
);
```

React separates concerns with units called "components" that contain both markup and logic without separating technologies.

> React embraces the fact that rendering logic is inherently coupled with other UI logic: how events are handled, how the state changes over time, and how the data is prepared for display. (Introducing JSX)

On the above, we can see the reason that we use JSX is that it can better render logics with other UI logic. And "components" can well manage the relationship among the logic.

##### Have a closer look at JSX

**Embedding Expressions in JSX:** We can see that a variable is declared and called name. Then it is used inside JSX by wrapping it in curly braces. And you can put any valid JavaScript expression inside the curly braces.

**JSX is an Expression Too:** JSX expressions turn into regular JavaScript function calls and evaluate to JavaScript objects.

**Specifying Attributes with JSX:** Use quotes to specify string literals as attributes. Use curly braces to embed a JavaScript expression in an attribute.

**Specifying Children with JSX:** JSX tags may contain children.

**JSX Prevents Injection Attacks:** React DOM avoids embedding any values in JSX before rendering them, so it ensures that you can never inject anything that's not explicitly written in your application.

**JSX Represents Objects:** React ``elements`` are like descriptions of what you want to see on the screen. React reads them and use them to construct DOM.

#### DOM

##### Virtual DOM

Traditional workflow of browser engines

1. HTML Parser will analyze elements in HTML files to build a **DOM Tree**.

2. CSS Parser will analyze CSS files and inline styles defined in them and generate a **Style Table** of the page.

3. **Attachment** will link DOM Tree and Style Table above and create a **Render Tree**. Actually, each DOM node in the DOM Tree has a method named "attach" which get the style information and return an object of render. These objects of render will make up a Render Tree.

4. Given the Render Tree, the browser will start to set the layout. Every node in the Render Tree will be allocated a precise coordinate on the screen.

5. The method named "paint" of each node will be called to show the node.

   <div align="center"><img src="https://i.loli.net/2018/10/22/5bcd8c4defcb5.jpg" alt="Workflow of Browser Engines" width="100%" /><i><b>Figure7</b>  Implementation of DOM in React</i></div>

Previously, when the DOM is modified, the browser will run the workflow above through, which can cost a lot of time. When there are ten modifications to the DOM, the browser will run the procedure ten times. However, as we all know, we can run the procedure to set ten modifications only in one time, while the computer cannot do that. 

Virtual DOM is designed to solve this bottleneck. It can save the ten modifications in one local instance of JavaScript to avoid unnecessary cost of repeated updating of DOM Tree.

##### Diff Algorithm 

We have learned that Virtual DOM normally resides in memory and begins with a copy of current DOM Tree. There comes a question, how can we make changes on the current DOM appear on the Virtual DOM Tree? Diff Algorithm works well in this case.

Algorithms comparing two trees have a time complexity of O(n^3^). However, the time complexity of Diff algorithm is O(n), which compares trees layer by layer. Since in web programming DOM elements won't be moved from layer to layer, this simplified algorithm works best. 

<div align="center"><img src="https://i.loli.net/2018/10/22/5bcd8c8f7cccb.png" alt="Examples of Different Cases of Diff Algorithm" width="100%" /><i><b>Figure8</b>  Process of Diff Algorithm in React</i></div>

There are four cases in our concern.

**Case 1: REPLACE** When a node is changed, the old node will be replaced by the new one along its children. This method might have low efficiency especially when the children nodes remain the same.

**Case 2: PROPS** When attributes of a node are changed, the node will be updated instead of being replaced. See the code below for an example.

```jsx
renderA: <ul>
renderB: <ul class: 'marginLeft10'>
=> [addAttribute class "marginLeft10"]
```

**Case 3: TEXT** When the text within a node is changed, just modify the text of that node.

**Case 4: REORDER** This case involves moving, adding and deleting children nodes. Let's have a look at this example.

<div align="center"><img src="https://i.loli.net/2018/10/22/5bcd8cc46e4ee.png" alt="Example: Add a Node" width="40%" /></div>

<div align="center"><i><b>Figure9</b>  Example: Add a Node</i></div>

There are several ways to solve this problem.

<div align="center"><img src="https://i.loli.net/2018/10/22/5bcd8cc49d173.png" alt="One Simple Way to Add a Node" width="40%" /></div>

<div align="center"><i><b>Figure10</b>  Example: One Simple Way to Add a Node</i></div>

The simplest way: delete C, add F, delete D, add C, delete E, add D, add E.
However, when we are writing codes in JSX, React reminds us that we should define keys for arrays and enumerations. 

<div align="center"><img src="https://i.loli.net/2018/10/22/5bcd8cc4c5c65.png" alt="A Better Way to Add a Node" width="40%" /></div>

<div align="center"><i><b>Figure11</b>  Example: A Better Way to Add a Node</i></div>

In this way, React can use keys to locate the position and add node much more efficiently.<a href="#ref_func1">[6]</a><a href="#ref_func2">[7]</a>

####  Component 

One of the most important functions of React is ``Component``. React components are small, reusable pieces of code that return a React element to be rendered to the page. Components allow developers to split the UI into independent, reusable pieces and think about each piece in isolation, which leads to a more efficient and simple way to develop beautiful and interactive web pages.<a href="#ref_func3">[8]</a>

> Conceptually, components are like JavaScript functions. They accept arbitrary inputs (called “props”) and return React elements describing what should appear on the screen.

Components can be broken down into distinct pieces of functionality and used within other components. They accept passes JSX attributes as a single object, which is called ``props``(which stands for properties), as inputs and return React elements such as other components, arrays, strings, and numbers. 

##### Function and Class Components

The way React defines components can be divided into two types: functions and classes. Although they are equivalent from React’s point of view, function definitions can be seen as a simple form of class definition.

Function components are literally JavaScript functions that accept single ``props`` object arguments with data and returns React elements. However, classes have some additional features like local state, which is exactly a feature available only to classes.

##### Composing and Extracting Components

Components can refer to other components in their output. This lets us use the same component abstraction for any level of detail. A button, a form, a dialog, a screen: in React apps, all those are commonly expressed as components.

Moreover, a component can be split into smaller components. When a component is too complex (for example, there are a lot of nestings) for its users to change it and reuse individual parts of it, they can consider extracting a few smaller and simpler components from it. Extracting is like the reverse process of composing components.

##### Inputs and Outputs of Components

Although React is pretty flexible, it has a single strict rule:

> All React components must act like pure functions with respect to their props.

It means whether the form of a React component is(no matter a function or a class), it must never modify its own props. React components must act like pure functions that do not attempt to change their inputs and always return the same result for the same inputs.

However, as dynamic data changes over time, React components are allowed by ``state`` to change their output over time in response to user actions, network responses, and anything else, without violating this rule.

#### State and Props

- In any application, data is necessary. React's data flow from top to bottom, that is from parent component to child component and data is stored in **props** and **state**.

  ##### props

  - The core idea of React is the idea of componentization, where pages are cut into separate, reusable components.
  - A component is conceptually a function that accepts a parameter as an input value, which is props, so props can be understood as data that is passed from outside into the component. Because React is a one-way data stream, props are basically the data passed from the parent component to the child component.
  - Suppose that we need to implement a list. According to React's core idea, we can regard list as a component. So we have two components: ``ItemList`` and ``Item``.

```jsx
   export default class ItemList extends React.Component{
   	const itemList = data.map(item => <Item item=item />);
   	render(){
   		return (
   	 	 {itemList}
   		)
   	}
   }
```

```jsx
   export default class Item extends React.Component{
     render(){
       return (
         <li>{this.props.item}</li>
       )
     }
   }
```

- Read-Only: ``Props`` are often used as rendering components and initialization states, and when a component is instantiated, its ``props`` are read-only and immutable. If ``props`` can be changed during the rendering process, the appearance of this component becomes unpredictable. The new ``props`` can be imported into the component only through the way of re-rendering the parent component.

##### state

-  ``State`` is similar to ``props``, but it is private and fully controlled by the component.
-  setState: The difference between ``state`` and ``props`` is that ``state`` can be changed. However, you can't modify the state directly by this. state = but you need to modify the state by this.setState() method.

#### Life Cycle

The following figure shows a complete life cycle of React components:

   <div align="center"><img src="https://ws4.sinaimg.cn/large/006tNbRwly1fwzaz94mx2j30kk0p0dhq.jpg" alt="lifecycle" width="100%" /><i><b>Figure12</b>  Life cycle of React components</i></div>

There are 3 states of a life cycle of React components<a href="#ref_life">[9]</a>:

1. **Initialization**: The first stage is the first drawing stage of components. In the dotted frame above, the loading and initialization of components are completed here.
2. **Update**: The second stage is component in the operation and interaction phase, as shown in the lower left corner dotted line frame, this stage component can handle user interaction, or receive event update interface.
3. **Destruction**: The third stage is the stage of component uninstallation and extinction, as shown in the dotted line frame in the lower right corner, here do some component cleaning work.

<h3 id="6.2"> 6.2 Extensibility</h3>

React using virtual DOM and JSX enables to compose components like functions while keeping the expressiveness of HTML which provides a highly scalable environment to web development. That is to say, the extensibility of React framework depends on its several very important features: ``Component``, ``JSX`` and ``Virtual DOM``. 

React components encourage a unidirectional data flow and make state explicit and data can only be entered into JSX elements through descriptive properties. Because of this mechanism, developers must consider its interface when creating new components so that they can communicate with other different components. Inside the component, you usually access the properties. The attributes provide a descriptive API and as long as they don’t change there is no regression if the component is changed. This is very similar to functional programming: new modules can be continually created, which increases the extensiblity of React projects.

As an extension of JavaScript, JSX is not only fully compatible with JS, but also embeds html code in JS, which means users can quickly learn to use it. In addition, for a non-React project, due to the characteristics of JSX, developers can easily convert it to a React project.

The mechanism of virtual DOM is similar to that of JVM. Instead of directly passing the DOM to the browser for processing and generating the DOM tree, virtual DOM process it firstly by itself, and then processed and then hand it to the browser. This makes React projects adaptable to different versions of the browser.

What's more, since React is written in pure JavaScript, we can rely on traditional ways to organize code to make it robust and scalable. React perfectly encapsulates the underlying functionality, so in this way, a big number of developers can working behind one component without being affected.<a href="#ref_ext">[10]</a>

<h2 id="7"> 7. Performance Perspective</h2>

In this section, we discuss performance of React as an important factor which provide a more detailed view of its architecture concerning how React enables highly scalable web development. Performance of a big project, especially it is related to web application development, usually refers to its ability to satisfy users' requests simultaneously. 

According to React's official document, it uses some strategies to efficiently improve its performance, which, for example, reduces latency or response time.

> Internally, React uses several clever techniques to minimize the number of costly DOM operations required to update the UI. For many applications, using React will lead to a fast user interface without doing much work to specifically optimize for performance. 

We used a JavaScript web frameworks benchmark<a href="#ref_perf1">[11]</a> to compare the performance of various versions of several of the most famous modern JS framework such as React, Angular, Vue and so on. This test used duration and memory usage as two indicators. The results are as follows:

<div align="center"><img src="https://ws3.sinaimg.cn/large/006tNbRwly1fwzrr5sqhoj30ue11w12o.jpg" alt="duration" width="80%" /></div>
<div align="center"><i><b>Figure13</b>  Duration(milliseconds)  of React and other JS web frameworks</i></div>

<div align="center"><img src="https://ws2.sinaimg.cn/large/006tNbRwly1fwzrtaepizj30u809kac4.jpg" alt="memory usage" width="80%" /></div>
<div align="center"><i><b>Figure14</b>  Memory allocation(MBs) of React and other JS web frameworks</i></div>

What's more, we used another benchmark which is focused on the performance of server-side rendered React on ``Node.js``.<a href="#ref_perf2">[12]</a> The benchmark used a simple Node.js [application](https://github.com/janit/node-templating-benchmark) that renders a HTML table of 100 rows of employee data from a JSON file to evaluate different templating methods such as ``React(DOMServer), v16.1.0``, ``Pug, v2.0.0-rc4``, ``Nunjucks, v3.0.1`` and ``ES6 template literals, native Node v9.2.0`` by comparing their  throughput (requests / second) and the average response time (in Milliseconds of waiting for response) with concurrencies of 1, 5, 50, 100 and 250 . The results are as follows:

 *In the test,  average values of the three runs were used and results are from Node prod mode, except for React got results for both dev and prod settings.*

<div align="center"><img src="https://ws4.sinaimg.cn/large/006tNbRwly1fwzs72sdrwj30s80hgt96.jpg" alt="throughput" width="100%" /></div>
<div align="center"><i><b>Figure15</b>  Throughput of React(DOMServer) and other templating methods</i></div>

<div align="center"><img src="https://ws4.sinaimg.cn/large/006tNbRwly1fwzsbj9vrvj30s80hgt92.jpg" alt="response time" width="100%" /></div>
<div align="center"><i><b>Figure16</b>  Response time of React(DOMServer) and other templating methods</i></div>

Through the above analysis, we can see:

- Compared with other two similar JS network frameworks, React starts slower than Vue yet faster than Angular.  Also, React's memory usage is smaller than Angular but bigger than Vue.

- The startup time row highlights the benefits of smaller frameworks. The cost of adding frameworks can be clearly seen for react. ``mobx`` or ``redux`` increase startup cost about 30% in comparison to react.

- As for server-side rendered React on ``Node.js``, React has a noticeably lower average throughput and a significantly longer response time than other templating methods. However, with production optimizations in place, React rises significantly and manages to be equal in performance compared to the Nunjucks engine, which is an impressive feat. It shows that while the throughput of React in development mode will be enough for many low to medium traffic web services.

In general, as a front-end JavaScript framework for web development, React's overall performance in browsers is relatively good, while server-side rendered React on Node.js has quite poor performance.

<h2 id="8"> 8. Technical Debt</h2>

After the analysis about React, we now can have a closer and deeper look into the source code. There have been some changes happened to the system. Thus we have to do something to identify functionality that is added to it. Technical is exactly the concept that reflects the extra development work that arises from wrong implementations. When code which is easy to implement in a short period is used in the place of an overall solution, long-run adjustments need to be made. Here are two ways of doing it, static code analysis and manual code inspection. And this section is not only related to the code but also associated with the documentation or the low testing coverage.

### 8.1 Static Analysis

Static code analyzing is one of the methodologies in technical debt analysis which often involves the evaluation of code styles, complexity, duplications, security and so on. We chose [CODEBEAT](https://codebeat.co/projects/github-com-liyihann-react-master) and [CodeFactor](https://www.codefactor.io/repository/github/liyihann/react) as static code analysis tools for identifying technical debt. These two tools can inspect codes separately in order to rate them from A to F. They conclude the outcome of code complexity, code issues, and code duplication. These examples of metrics are taken into consideration. What's more, the two tools are free to be accessed.

#### Analysis Results

##### CODEBEAT

For the analysis of React code, CODEBEAT gave an overall score of 3.44 points (4 points total).

The results show that there are 2209 complexity issues, 466 duplications, and 6037 style issues in the total of 73,060 lines of code.

<div align="center"><img src="https://ws4.sinaimg.cn/large/006tNbRwly1fwvvqzcnu8j30ro08sjsa.jpg" width="60%" /></div>

<div align="center"><i><b>Figure17</b>  Overall result of CODEBEAT in static analysis of React</i></div>

CODEBEAT listed all the files associated with the above issues and gives a rating from A to F, where F is the worst case. The figure below shows part of the list of files containing problematic code.

<div align="center"><img src="https://ws2.sinaimg.cn/large/006tNbRwly1fwvvx5ueytj31kw0ubgtu.jpg" width="100%" /></div>

<div align="center"><i><b>Figure18</b>  List of files of React involving problems shown by CODEBEAT</i></div>

##### CodeFactor

Unlike CODEBEAT, CodeFactor not only calculates the code lines of the React project itself but also counts its external reference code.

It counted about 121,145 lines of code lines of React in the past two weeks, which contains 23,144 issue lines, and gave an overall score of 83.3 (100 points total).

<div align="center"><img src="https://ws1.sinaimg.cn/large/006tNbRwly1fwvw5pj5gej31ig0f8ach.jpg" width="90%" /></div>

<div align="center"><i><b>Figure19</b>  Overall result of CodeFactor in static analysis of React</i></div>

CodeFactor rated the code issues to varying degrees and gave some suggestions based on them. The following figure(left) shows several hotspots, which are the most significant ones that can be improved for code promotion based on CodeFactor recommendations.

Meanwhile, CodeFactor analyzed and rated 141 external libraries referenced by React. The following figure(right) is the analysis result of several of the most important libraries for React.

<div align="center"><img src="https://ws2.sinaimg.cn/large/006tNbRwly1fwvwi2sz4ej30ge0fw404.jpg" width="40%" /><img src="https://ws1.sinaimg.cn/large/006tNbRwly1fwvwe4wo46j30gg0fgwfh.jpg" width="40%" /></div>

<div align="center"><i><b>Figure20</b>  Hotspots and library ratings of React shown by CodeFactor</i></div>

#### Discussions of Technical Debt

After a comprehensive evaluation of the results of static code analysis tools (such as CODEBEAT and CodeFactor), we can summarize the following points:

- React project code has quite a lot of duplications. Of the 532 duplications discovered by CodeFactor, 7 were rated as critical issues, 485 as major issues and 40 as minor issues. According to CODEBEAT's [documentation](https://hub.codebeat.co/docs/software-quality-metrics#lines-of-code),  duplications are considered as one of the most serious issues due to their harm to the maintainability of the project.
- React project code has some complexity issues. For example, there are some complex methods with a large number of rows or a large number of nested layers, which is not very readable.
- React project code has some other code style issues, such as unnecessary escape characters, malformed whitespace, etc.

React's code can be found some problems in static analysis, but the overall situation is relatively good. However, it should be pointed out that there are some relatively serious problems in the project. If these problems can be modified, the quality of the entire project will be greatly improved. 

Static analysis tools such as CODEBEAT and CodeFactor can only analyze the code line by line from the surface layer, and cannot uncover the relationships between files and even modules. Nevertheless, they do help find errors and discover trends at the code level.

### 8.2 Testing Debt

Testing debt is another type of technical debt. Software testing is a crucial step in the development cycle and it needs to be thorough. The longer you put off testing, the more potential your project has to accumulate technical debt. In an Agile development process, individual units of the end product are designed, developed and tested before moving onto the next functional unit of the software. This helps to avoid leaving errors in the source code of programs or otherwise overlooking problems that will only worsen as more code is written around faulty components.<a href="#ref_tec1">[13]</a>

Testing new features and functions only are natural. However, regression testing is equally important. A typical testing cycle will focus on different levels of the software at different times. For example, Unit Testing is the process of testing individual units of the software to see if they are coded properly. And Integration Testing, on the other hand, is testing to see if the interactions between different units are happening like they’re supposed to.<a href="#ref_tec6">[14]</a>

#### Coverage Testing Tools

React uses automated testing tools like ``COVERALLS`` and ``CircleCI`` to minimize the cost for software testing. Code coverage determines how many lines of code is being tested.

#### Analysis Results

In this case, we will inspect the amount of code covered by unit tests in React based on reports generated by coverage.

<div align="center"><img src="https://ws3.sinaimg.cn/large/006tNbRwgy1fwwe81jn80j31kw0seu0x.jpg" width="100%" /></div>

<div align="center"><i><b>Figure21</b>  Result of COVERALLS in coverage testing of React</i></div>

This report shows an overall high code coverage all the time to the current nearly 90%, which means React does well in the field of testing. 

<div align="center"><img src="https://ws4.sinaimg.cn/large/006tNbRwgy1fwweol3lhgj30rg13wk90.jpg" alt="Details of Coverage on Facebook/React"  width=40%></div>

<div align="center"><i><b>Figure22</b>  Overall high code coverage of React all the time shown by COVERALLS</i></div>

And more information about coverages of different folders is shown in this figure. Since React Native is a relatively new component, no wonder that folder has a low coverage. And there are some files in those low-coverage folders without corresponding test files. In fact, 100% code coverage is generally not necessary and not practical. Although React remains high code coverage which is definitely an advantage, there is still room for improvement in relatively new components. 

<h2 id="9"> 9. Evolution Perspective</h2>

This section summarizes and analyzes feature evolution of React by comparing its changes among different releases, which helps us understand its core design and architecture.

With the inspiration of XHP, an HTML component framework for PHP being used at Facebook, React was developed from FaxJS which was an innovation of  Facebook before 2013, in order to make it more efficient and easier to re-render the application. <a href="#ref_evo1">[15]</a>

> “One of the things we strived for when we were building our component framework, is that we want to minimize the number of developer-facing mutations that the developer is exposed to.” (Jordan Walke)

React's initial public open-sourced version was released on May 29, 2013, during the JS ConfUS as v0.3.0. And after that, it varies greatly between different releases. The latest version(v16.5.2) of React was released on Sep 18, 2018, and there are still changes that have landed in master but are not yet released.  The following figure shows the timeline of React version releases based on its [changelog](https://github.com/facebook/react/blob/master/CHANGELOG.md) and [version release posts](https://reactjs.netlify.com/blog/all.html). 

<div align="center"><img src="https://ws3.sinaimg.cn/large/006tNbRwgy1fx2ymfzrwlj311u0mgn4a.jpg"  width=100%></div>

<div align="center"><i><b>Figure23</b>  Feature evolution of React </i></div>

React uses semantic versioning to mark its major releases, minor releases, and bug fix patches. Here, we will mainly discuss the changes between its major versions.

`v0.3(0.3.0-0.3.3)`Initial public release(v0.3.0). Allow reusing the same DOM node to render different components.s

`v0.4(0.4.0-0.4.1)`Prop validation and default values. Auto-bind by default. Support for more DOM elements and attributes. Support for the key prop. Improved synthetic event system. Some other minor changes and bug fixes.

`v0.5(0.5.0-0.5.2)`Memory usage improvements. Performance improvements. Standardized prop. Support for Selection events, Composition events, additional DOM properties, and additional SVG properties. Some other minor changes and bug fixes.

`v0.8(0.8.0)`Added support for more attributes. Improved error messages. New events support. Some other minor changes and bug fixes.

`v0.9(0.9.0)`Better support for normalizing event properties. Improvements to error system. New add-ons build utilities for writing unit tests for React components. Some other minor changes and bug fixes.

`v0.10(0.10.0)`Added warnings to help migrate towards descriptors. Made it possible to server render without React-related markup. Added support for more attributes. Some other minor changes and bug fixes.

`v0.11(0.11.0-0.11.2)`Rendering to null. More properties for keyboard events. New normalized event. A new API for counting the number of children. Some other minor changes and bug fixes.

`v0.12(0.12.0-0.12.2)`BSD license with accompanying Patents grant. Moved default prop resolution to Element creation time instead of mount time. Added support for more HTML attributes. Corrected many top-level APIs to align with the terminology. Some other minor changes and bug fixes.

`v0.13(0.13.0-0.13.3)`Deprecated patterns that warned in `v0.12` no longer work. Support for using ES6 classes to build React components. Added new top-level APIs. New ref style, allowing a callback to be used in place of a name. Support for iterators and immutable-js sequences as children. Some other minor changes and bug fixes.

`v0.14(0.14.0-0.14.8) `Split the main `react` package into two: `react` and `react-dom`. DOM node refs. A new, simpler syntax for components. Deprecation of react-tools. Support for two compiler optimizations. Some other minor changes and bug fixes.

`v15.0` Initial render now uses `document.createElement` instead of generating HTML. `data-reactid` is no longer on every node. No more extra `<span>`s. Rendering `null` now uses comment nodes. Functional components can now return `null`. Improved SVG support. Some other minor changes and bug fixes.

`v15.4.0` React package and browser build no longer "secretly" includes React DOM. Required PropTypes now fail with specific messages for null and undefined. Improved development performance by freezing children instead of copying. Some other minor changes and bug fixes.

`v15.5.0` Added a deprecation warning for `React.PropTypes` . Points users to prop-types instead. Fixed an issue when using `ReactDOM` together with `ReactDOMServer`. Added component stack info to invalid element type warning. Some other minor changes and bug fixes.

`v15.6.0` Downgrade deprecation warnings to use `console.warn` instead of `console.error`. Add a deprecation warning for `React.createClass` , deprecation warnings and separate module for `React.DOM` factory helpers. Warn for deprecation of `React.createMixin` helper. Some other minor changes and bug fixes.

`v16.0` Components can now return arrays and string from `render`. Improved error handling with intrduction of "error boundaries". First-class support for declaratively rendering a subtree into another DOM node with `ReactDOM.createPortal()` .Streaming mode for server side rendering is enabled with `ReactDOMServer.renderToNodeStream()` and `ReactDOMServer.renderToStaticNodeStream()`. Some other minor changes and bug fixes.

`v16.5.0` Add a warning if `React.forwardRef` render function doesn't take exactly two arguments. Improved the error message when passing an element to `createElement` by mistake. Don't call profiler `onRender` until after mutations. Some other minor changes and bug fixes.

<h2 id="10"> 10. Conclusion</h2>

From several software architecture perspectives, we summarised the React to help readers understand, use and be able to contribute to the project. A conclusion has been drawn that React is an extensible, simple and fully functional JavaScript library.

First of all, in the **Stakeholder Analysis**, we discussed various roles of stakeholders involved in React. Core members take on numerous responsibilities of different roles. They maintain and promote React along with community contributors. 

Secondly, the **Context View** showed the responsibilities and external entities that React uses. Therefore, readers could get a clear view of the interactions within the environment of React.

Thirdly, in the **Development View**, design principles, code organization and model organization of React were discussed in details. Based on React's clear principle, React provides a elegant  way to write UI code succinct and efficient. Although React's code organization is a little confusing due to its fast development, it's core function module is simple to understand. At the same time, React provides many tools for users to build their websites freely. 

Next, the **Deployment View** gave a description of the environment where React would be deployed. Various third-party software requirements were introduced in details to help programmers to set up the developing environment.

What's more, in the **Functional View**, we showed several key features of React including ``JSX``, ``Virtual DOM``,  ``Component`` and ``State&Props``, which were vital and unique. These functionalities effectively increase the extensibility of the React projects.

In addition to these four views, we also studied React from other perspectives. From the **Performance Perspective**, a more detailed view of its architecture was displayed. Performance of React is relatively good in comparison with its competitors. Key features of React guarantee the robustness and scalability of web development for programmers. 

In the **Technical Debt** section, we used tools to analyze technical debts within React such as code duplication, testing debt and so on. There were still minor errors in static code analysis. Meanwhile, React performed beyond expectation in the code coverage analysis.

From the **Evolution Perspective**, we summarized and analyzed feature evolution of React by comparing its changes among different releases, which helps us understand its core design and architecture.

Raised in 2014, React is still thriving in the field of web page development. It is the architectural integrity, open source and users first policy that makes React prevalent among web programming. Virtues of React are attracting contributors on Github and users around the world, who facilitate the growing of React in return. We are convinced that React will be prosperous all through in the future. Now, core members of React are paying attention to React Native which may bring a revolutionary change to the application development on mobile devices. 

Thanks to this valuable opportunity, we can concentrate on the architecture analysis of React in twelve weeks. During this procedure, we gradually learned React through multiple meetings and iterative revisions of this document. In addition, we sincerely hope that this document will benefit users, developers and those who have interests in React. 

<h2 id="11"> 11. References</h2>

<a name="ref_sta1">[1]</a>  Nick Rozanski and Eoin Woods. Software System Architecture: Working With Stakeholders Using Viewpoints and Perspectives. Addison-Wesley, 2012. 

<a name="ref_sup1">[2]</a> [React - Network Dependencies](https://github.com/facebook/react/network/dependencies)

<a name="ref_con1">[3]</a> [React - A JavaScript library for building user interfaces](https://reactjs.org/)

<a name="ref_dev1">[4]</a>  [Design Principles of React](https://reactjs.org/docs/design-principles.html#composition)

<a name="ref_func0">[5]</a>[Introducing JSX – React](https://reactjs.org/docs/introducing-jsx.html)

<a name="ref_func1">[6]</a>  [从零开始实现一个React（一）：JSX和虚拟DOM](https://github.com/hujiulong/blog/issues/4)

<a name="ref_func2">[7]</a>  [虚拟DOM介绍](https://www.jianshu.com/p/616999666920)

<a name="ref_func3">[8]</a> [Components and Props – React](https://reactjs.org/docs/components-and-props.html)

<a name="ref_life">[9]</a> [React生命周期](https://www.cnblogs.com/qiaojie/p/6135180.html)

<a name="ref_ext">[10]</a>  [How React Makes Web Development Scalable](https://blog.codecentric.de/en/2016/05/how-react-makes-web-development-scalable/)

<a name="ref_perf1">[11]</a>  [Results for js web frameworks benchmark – round 6](https://www.stefankrause.net/js-frameworks-benchmark6/webdriver-ts-results/table.html)

<a name="ref_perf2">[12]</a>  [The Performance Cost of Server Side Rendered React on Node.js](https://malloc.fi/performance-cost-of-server-side-rendered-react-node-js)

<a name="ref_tec1">[13]</a>[Technical debt - Wikipedia](https://en.wikipedia.org/wiki/Technical_debt)

<a name="ref_tec6">[14]</a>  [Avoiding Technical Debt: An Intro to Software Testing](https://www.skillgigs.com/blog/avoiding-technical-debt-an-intro-to-software-testing/)

<a name="ref_evo1">[15]</a>  [The Evolution Of React — DashBouquet](https://dashbouquet.com/blog/frontend-development/the-evolution-of-react)
