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





## General Coding Workflow

### Git
- repo naming: ??? PROJECT-some_module ???
- master, staging, feature branches, pull requests, don't squash

### Semver 
- in development, 0.1.0 ... once it has dependencies 1.0.0
- every project must have a maintainer who keeps the readme and changelog/versioning up to date 

### Readme.md 
- every project must have a readme that details any gotchas that might not be apparent within the readable code, especially important how to get the codebase setup and running properly

### Changelog
- details changes that are x.x.0, especially new features and obviously breaking changes 


## Language/Framework Specific Standards

### Javascript/TypeScript

We follow the Airbnb Javascript StyleGuide and have based our own linting on their style guide
https://github.com/airbnb/javascript ??? should we fork these ???

**Some DON'Ts**
- Don't sacrifice READABILITY for "magic" or ease of implementation unless it's a known, documented pattern and then make it known in the README or someplace else for the next developer
- Don't leave console.log statements in code (and better still, use a debugger)

Development Tools

??? Chrome sourcemaps and "workspaces", live editing and debugging within Chrome

??? CSS ???

??? JEST ???

#### Node.js


#### React

Again, we build on the Airbnb guidelines:
https://github.com/airbnb/javascript/tree/master/react



New react projects need to be created using ???create-cactus-react-app, which is based on create-react-app but has additional dependencies and configurations that are specific to Cactus.

All React projects MUST use Redux, ImmutableJS, redux-sagas and related "redux compatible" modules including 'connected-react-router/immutable', 'redux-saga-requests', 'redux-immutable' (for an Immutable compatible combineReducers at the root level...entire state tree should be IMMUTABLE)

Development Tools

React DevTools
https://github.com/facebook/react-devtools

Redux DevTools
https://github.com/reduxjs/redux-devtools

ImmutableJS Formatter
https://chrome.google.com/webstore/detail/immutablejs-object-format/hgldghadipiblonfkkicmgcbbijnpeog?hl=en

??? TBD ???
CSS/JSS https://github.com/airbnb/javascript/tree/master/css-in-javascript


### CSS
https://github.com/airbnb/css

### Python



### Ruby
https://github.com/airbnb/ruby

#### Ruby on Rails







How to create a new applicaton (create-cactus-app) includes core Cactus dependencies, layouts, examples and .gitignore and linting setups, built ontop of create-react-app
Testing framework JEST
Logging and events

Every codebase needs to be reviewed WEEKLY for code updates, so we don’t have code erosion (npm outdated, other tools to update/test packages)

Grading code
NO long switch statements, functionality should be broken out into functions within a module
ALL exports should happen at the end of the file, so it’s clear what is exported and what isn’t
Include documentation as a module, so we know what version it was written with?
Semver for every cactus module
We use BABEL, for full es6 compatibility 
Based on create-react-app
Redux-loop, redux-thunk, redux-saga
prettier/beautify https://css-tricks.com/prettier-beautify/ … code MUST be beautiful and READABLE


Files with JSX should have .jsx extension, same with .ts for TypeScript
.editorconfig vs vscode settings vs prettier eslint and beautify
No generic import and export to group things (root/actions.js)...need to be explicit
Known file entry points and flow
Separate routes file
Don’t combine middleware and sagas...pure sagas only
TypeScript?
Order of imports (modules first, then local code in order of most local at bottom)
	


Highlights

NO console.log debugging (learn to use breakpoints or other debug mechanisms, eventing loggin)
TODO/FIX comments
Creating documentation
Listing dependencies and what they do
Airbnb coding standards and linting
Maximum nesting levels?
FSA compatible actions?

React
JSS? Where to locate assets?
Props must be declared/defined (prop-types)

Redux
File layout
Naming actions and action creators
No * importing, must explicitly import action creators for readability
Following logic/logging for Redux (replayability also)
What belongs in action creators, sagas, middleware??, action creators
Using reselect/selectors (memoization and understanding what gets rendered or rerendered)
Immutable-JS
Understanding where state is changing and causing rerenders
Namespacing actions 
https://kickstarter.engineering/namespacing-actions-for-redux-d9b55a88b1b1
Use es6 style functions that auto bind instead (or if needing to bind, do it in the constructor...don’t use autoBind from react-extras or do we?? Discuss prototype vs instance and memory situations
Use controlled components almost ALWAYS (vs uncontrolled with ref=)

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




Other

Separation of components/containers and writing portable code that can be converted to a separate NPM at any time (nesting component code under containers??)
Components should be dumb/unaware of redux, immutableJS  etc?
MUST use redux compatible modules (router, api, etc)
Every project should have some standard things setup for VPN, logging, authentication, deployment, builds, staging, docker containers, database seed data


Use appropriate dev tools in Chrome (react and redux both have them)

Use VS Code and the shared Cactus configs (2 spaces, formatters, debuggers)

Branching and merging, master deply build, dev/staging branches deploying and building and automated tests linting and grading
Pull requests


Project checklist