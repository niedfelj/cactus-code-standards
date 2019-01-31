# Cactus Code Standards and Style Guide

## Welcome to the Cactus way of coding

Version 0.1.0

We are heavily opinionated because we believe in beautiful, modern, READABLE code that leverages the inherent power in each language that we use. Opinionated code means that anyone on the team can look at what you've been doing and understand the techniques, file structure, and related modules/gems/extensions that are being used. Keep code simple and when it becomes a jumbled mess, take the time to REFACTOR so that it makes sense and is READABLE by someone else.

## About This Document

This document and this repository is a living (and versioned) guide to coding at Cactus. Every project should include this project as a dependency (module, gem, etc) so that we know what version of this document was relevant when the codebase was created or last refactored. This repository is also the home of any automated coding tool configurations and dependencies including ??? eslint, tslint, prettier, beautify, etc ???

## Core Principles

* Class, Object and Variable Names Matter - make them relevant and REFACTOR when they aren't
* Use a Debugger - don't rely on console.log and definitely don't leave logger debug output in code
* Spend Time Architecting/Designing - always look at ways of doing something better or using existing codebases/projects
* If you find yourself 6 layers deep and 50 lines down in switch statement, break it out into sub functions so the core logic remains READABLE 

## Your Workspace

### Visual Studio Code

We require the use of VS Code by all developers because we've configured our "template" projects with the correct settings and also have designed scripts and techniques that work specifically with VS Code.

Prettier
https://prettier.io

Beautify (needs settings.json so doesn't conflict with Prettier)

Chrome Debugger

???TBD What else???

### Chrome

We use Chrome to develop, partially because it's become the defacto standard browser, but mostly because it has the most extensions for development.

Extensions that we use are listed in each language/framework specific section.

### Docker

### VPN

Every project has a separate VPN that ties together devices and the cloud and the office. We use a SSO solution to manage access and deployments along with monitoring. ??? TBD ???  There is a list of standard setup procedures for each new client project that involves creating a new VPN, setting up cloud infrastructure, setting up DevOps infrastructure, creating build servers and webhooks to respond to 


## General Coding Workflow

### Git
- repo naming: ??? PROJECT-some_module ???
- master, staging, feature branches, pull requests, don't squash
- auto linting, auto code grading
- every project should have a master repo that contains build scripts and lists the dependencies for each sub-project so that a build server can access shared constants and cross dependencies and auto deploy each different component whether it's a device, a node server, or some other system. This project should also have the core Docker Compose setup for each sub project that has it's own Docker file

### Semver 
- in development, 0.1.0 ... once it has dependencies 1.0.0
- every project must have a maintainer who keeps the readme and changelog/versioning up to date 

### Readme.md 
- every project must have a readme that details any gotchas that might not be apparent within the readable code, especially important how to get the codebase setup and running properly
- core external dependencies should be enumerated in the Readme as to why they are needed and how/what they do if it's not clear, ie redux-saga-requests

### Changelog
- details changes that are x.x.0, especially new features and obviously breaking changes 

### Maintenance
- every project should be reviewed WEEKLY in an attempt to keep modules/gems up to date to prevent code erosion. This means running npm outdated or bundle outdated etc, reviewing updates, attempting to apply updates and testing them along with updating versioning, CHANGELOGS and applying any other maintenance tasks required

### Core Libraries
- every project must use standard Cactus coding libraries and abstractions for gathering telemetry, logging, event monitoring and other features ??? 

### Autogen Documentation/TODOs
??? format for TODOs/comments/inline documentation ???

### Development and Test Seed Data
??? TBD, need this for every project along with "migrations" ???

## Language/Framework Specific Standards

### Javascript/TypeScript

We follow the Airbnb Javascript StyleGuide and have based our own linting on their style guide
https://github.com/airbnb/javascript ??? should we fork these ???

We use Babel for everything, so please use ES6 syntax. We also have some specific rules that we follow (and prettier will clean up for you), but they include 2 spaces as an indent, and NO semicolons

??? .editorconfig vs vscode settings vs prettier eslint and beautify ???

Files with JSX should have .jsx extension, same with .ts for TypeScript


**Some DON'Ts**
- Don't sacrifice READABILITY for "magic" or ease of implementation unless it's a known, documented pattern and then make it known in the README or someplace else for the next developer. eg, Don't combine all action-creators into one file and then bind them all in every view using *
- Don't leave console.log statements in code (and better still, use a debugger)

**Some DOs**
- Do export at the end of the file/module so it's clear what the "api" is
- Do import in the order of external modules, local files with the MOST local (meaning same dir) last
- Only import what's needed and make it declarative (no wildcards) so it's easy to see where code is coming from

Development Tools

??? Chrome sourcemaps and "workspaces", live editing and debugging within Chrome

??? CSS ???

??? JEST ???

#### Node.js


#### React

Again, we build on the Airbnb guidelines:
https://github.com/airbnb/javascript/tree/master/react


New react projects need to be created using ???create-cactus-react-app, which is based on create-react-app but has additional dependencies and configurations that are specific to Cactus (.gitignore, linting rules, other rules, scripts, default file layouts, sample components/containers)

All React projects MUST use Redux, ImmutableJS, redux-sagas and related "redux compatible" modules including 'connected-react-router/immutable', 'redux-saga-requests', 'redux-immutable' (for an Immutable compatible combineReducers at the root level...entire state tree should be IMMUTABLE)

Don't combine or use other middlewares, you should be able to do EVERYTHING using redux-saga (don't use redux-thunk or redux-loop)

??? TBD Main entry points for react and default file layouts for root, containers, components ... see INGH_AdminTool when it's updated to debate ???

??? Routes should always be in a separate file ???

??? FSA compatible actions, eg redux-saga-requests can use a simpler form or be FSA compatible, I chose the simpler form but maybe that's a mistake in the long run ???

Props must be declared/defined using prop-types.

??? Naming actions and action creators ???

Action creators do not need to map 1:1 with actions and should be named in a way that makes sense when called in the component. Action creators should also be very THIN and contain a minimum of business logic. Action creators should also EXPLICITY declare their argument list instead of using generics like payload or meta.

```
export const getCode = phoneNumber => ({
 type: 'SUBMIT_PHONE_FOR_CODE',
 request: {
   url: '/auth/phone',
   method: 'post',
   data: {
     number: phoneNumber
   }
 }
})
```



Reducers should contain the core logic for shaping state, but they should also be aware of not shaping it too much so that it's constantly changing (leave it as raw as possible and allow selectors to shape it further for ingestion by the container)

Sagas should handle any side effects (anything that is too complicated/asynchronous to handle in an action creator or reducer)

When using ImmutableJS, toJS should never be called in mapStateToProps as it ALWAYS generates a new object, is very heavy and will cause a rerender EVEN if the Immutable object didn't change

??? Reselect/selectors should be used to build a components state from the basic raw state, so that data can be memoized and renders happen efficiently ???

Containers are components that are "smart" enough to be connected to dispatch and state. They should contain "dumb" components that ONLY receive props and are not redux or Immutable aware. Their "api" should be clearly defined using prop-types. If they aren't GLOBAL components, they should be nested within the containers folder.

??? Namespacing actions ??? I hate the global namespace for actions, I tried some ideas with AdminTool but need more input on this one. Kickstarter had some posts on it, but it felt like overkill. I'm more looking for a solution to know where an action came from, so it's easy to track down the core package and trace code.  https://kickstarter.engineering/namespacing-actions-for-redux-d9b55a88b1b1

Use es6 style functions/class fields since they are always bound to the correc this. Declare initial state using a class field like state = {something: false} and avoid using constructors unless necessary. Never use autoBind. Only gotcha with this methodology is that every INSTANCE gets their own version of these class fields, so for components that are instantiated in large numbers it might be problem. ??? discuss ???

Use controlled components almost ALWAYS (vs uncontrolled with ref=). https://reactjs.org/docs/uncontrolled-components.html

Containers and components should always be thought of first and foremost as INDEPENDENT entities, attempting to make them portable and non-reliant on other parts of the state tree or knowledge of other containers or components. When there is a necessity to interconnect them, try to do it in a way that you could still easy extract parts of the codebase because they have a known way of interacting with each other vs directly interacting with state. 

Development Tools

React DevTools
https://github.com/facebook/react-devtools

Redux DevTools
https://github.com/reduxjs/redux-devtools

ImmutableJS Formatter
https://chrome.google.com/webstore/detail/immutablejs-object-format/hgldghadipiblonfkkicmgcbbijnpeog?hl=en

??? TBD ???
CSS/JSS https://github.com/airbnb/javascript/tree/master/css-in-javascript
??? Where to locate assets ???

### CSS
https://github.com/airbnb/css

### Python



### Ruby
https://github.com/airbnb/ruby

#### Ruby on Rails

