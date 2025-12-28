# Oracle JET MVVM Architecture Style Guide

Oracle JET supports the Model-View-ViewModel (MVVM) architectural design pattern.

In MVVM, the Model represents the app data, and the View is the presentation of the data. The ViewModel exposes data from the Model to the view and maintains the app's state.

To support the MVVM design, Oracle JET is built upon a modular framework that includes a collection of third-party libraries and Oracle-provided files, scripts, and libraries.

To implement the View layer, Oracle JET provides a collection of UI components implemented as HTML5 custom elements, ranging from basic buttons to advanced data visualization components such as charts and data grids.

Knockout.js implements the ViewModel and provides two-way data binding between the view and model layers.

Oracle JET features include:

- Messaging and event services for both Model and View layers
- Validation framework that provides UI element and component validation and data converters
- Caching services at the Model layer for performance optimization of pagination and virtual scrolling
- Filtering and sorting services provided at the Model layer
- Connection to data sources through Web services, such as Representational State Transfer (REST) or WebSocket
- Management of URL and browser history using Oracle JET `CoreRouter` and `oj-module` components
- Integrated authorization through OAuth 2.0 for data models retrieved from REST Services
- Resource management provided by RequireJS
- A `RESTDataProvider` API to represent data from JSON-based REST services
- JavaScript logging
- Popup UI handling

## Project Setup

This section assume that you setup the JET project for MVVM JET application developing with JavaScript only.

### Setting Up a MVVM Project

To start a new Oracle JET MVVM project, use the Oracle JET Command-Line Interface (CLI). The following command scaffolds a basic web app:

```bash
ojet create my-web-app --template=basic
```
This sets up a project with a pre-configured structure, including essential files and directories for web app development. After scaffolding, navigate to the app directory and run:

```bash
cd my-web-app
ojet build
ojet serve
```
This builds and serves the app locally for development and testing.

### Directory Structure

The typical directory structure for a JET web app includes:

- `src/`: Source files for the application, including index.html file and a main.js RequireJS bootstrap file.
- `src/js/`: contains templates and scripts for the app's views and viewModels
- `src/css/`: CSS files for styling.
- `node_modules/`: Dependencies installed via npm, including Oracle JET libraries.

Understanding this structure is crucial for organizing your codebase effectively.

The index.html, assuming for JET version 18.1.0, also includes meta links to the following dependencies from Oracle CDN:

- redwood CSS: `https://static.oracle.com/cdn/jet/18.1.0/default/css/redwood/oj-redwood-min.css`
- 3rd-party requireJS: `https://static.oracle.com/cdn/jet/18.1.0/3rdparty/require/require.js`

## Use RequireJS in Oracle JET App

To use RequireJS in an Oracle JET app:

1. In the bootstrap file or your app scripts, in the require() definition, add additional Oracle JET modules as needed.
2. Add any scripts that your app uses to the require() definition and update the function(ko) definition to include the script.
3. Add any app startup code to the callback function.
4. If your app includes resource bundles, enter the path to the bundle in the merge section.

Here's an example of the steps in order.
Your app uses the Oracle JET Common Model integrated with Knockout and includes an oj-dialog. Add the highlighted modules to your bootstrap file or app script.

```js
require(['knockout', 'ojs/ojdialog'],
  function(ko) // obtaining a reference to the oj namespace
  {
  }
);
```

Then, to use a script named myapp.js, add the 'myapp' code to your require() definition, as shown below.

```js
require(['myapp', 'knockout', 'ojs/ojdialog'],
  function(myapp, ko) // obtaining a reference to the oj namespace
  {
  }
);
```

## Oracle JET User Interface Components

Oracle JET currently has two sets of UI components. The first set with components that use the oj- namespace are packaged in @oracle/oraclejet and date back to the initial releases of Oracle JET. The newer Core Pack components, introduced in January 2023 with release 14.0.0 of Oracle JET, use the oj-c- namespace and are packaged in @oracle/oraclejet-core-pack.

Core Pack components represent the future of JET. The JET team are rewriting all the existing JET UI components from scratch using Preact, a modern virtual DOM rendering library that uses React design and composition principles. 

JET's existing set of UI components, now referred to as legacy components, has served the JET community and its app developers well for the last 10 years. The legacy components, using the oj- namespace, will run side-by-side with the newer Core Pack components, using the oj-c- namespace in the same JET apps.

To use core pack components, require() should use the prefix `oj-c/` for referencing the core-pack elements, e.g. in the above example code, to reference the core-pack JET dialog component:

```js
require(['myapp', 'knockout', 'oj-c/dialog'],
  function(myapp, ko) // obtaining a reference to the oj namespace
  {
  }
);
```
