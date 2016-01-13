Meteor Conventions
==================

Conventions used by Cell[0] on [Meteor](https://www.meteor.com/) projects.


Table of contents
-----------------

  1. [Introduction](#introduction)
  1. [Documentation](#documentation)
  1. [Folder Structure](#folder-structure)
  1. [Client / Server / Lib](#client-server-lib)
  1. [Style](#style)


Introduction
------------

This document aims to define clear conventions as much as possible.

However, Meteor is a very flexible tool. We tend to use it for projects that can be very different in nature. This is why for some important choices, there is not one approach 'to rule them all'. In these cases this document describes options and why to choose them.


Documentation
-------------

- [2.1](2.1) <a name='2.1'></a> **Top level**: `README.md` at the root of the project. Include a one-line description of the project, a how-to-run and how-to-contribute.

  > Why? Makes it easy for people to contribute. Also, it stimulates you to make contributing and building easy and automated.

- [2.2](2.2) <a name='2.2'></a> **Packages**: Postpone writing documentation as long as possible. When it is needed: write a `README.md` at root of package.

  > Why? Documentation increases the cost of refactoring.

  *Idea: add author at package.js?*


Folder structure
----------------

- [3.1](3.1) <a name='3.1'></a> **Client code**: No convention defined yet.

  There are two choices to make:

  + Package or non-package
  + One folder or distrubution [across topic folders](#3.2)

  *Package or non-package*: Placing the code into one or more packages gives you the advantage of controlling the file load order. However, having the client and non-client code in two clearly distinct places often makes the project much more clear.  

  *Write one vs distribution*: We need more experience, especially in collaborative projects.

- [3.2](3.2) <a name='3.2'></a> **Packages**: Packages-for-everything.

  > Why? Packages give you control of file loading order.

  Load only top-level packages in `.meteor/packages`.

  ```
  my-domain:apples
  my-domain:oranges
  my-domain:pears
  ```

- [3.3](3.3) <a name='3.3'></a> **Distribution**: Separated code per topic.

  > Why? Having *intent on top* makes it easy to find where things are happening, and for developers to work side-by-side on the same project simultaneously.

  ```
  packages/financial/package.js
  packages/financial/invoices/invoice.js
  packages/financial/invoices/invoiceCollection.js
  ```

- [3.4](3.4) <a name='3.4'></a> **Depth**: Avoid 'flattening' until needed.

  > Why? Exposing details is bad practice. Aim to have *intent on top*. Also, when you start getting package folder names like `apples-storage`, `apples-domain`, etc your packages folder will quickly start looking like a mess.

  ```
  # bad
  packages/invoices/package.js
  packages/invoices/invoice.js
  packages/invoices/invoiceCollection.js

  # good
  packages/financial/package.js
  packages/financial/invoices/invoice.js
  packages/financial/invoices/updateInvoice.js
  packages/financial/invoices/invoicesCollection.js
  packages/financial/transactions/updateTransaction.js
  packages/financial/transactions/transactionsCollection.js
  ```

  Of course, it is always possible to refactor specific pieces into a separate package later; when you learn that something is important enough to be *on top*.

- [3.5](3.5) <a name='3.5'></a> **External dependencies**: Load in a dedicated `external-dependencies` package.

  > Why? Figuring out repeatedly which packages you need to do X will quickly drive you crazy, especially when it comes to Meteor core packages.

  Use `api.imply` to load all external dependencies in a dedicated package. In all other project packages, depend on that package.

  ```javascript
  //packages/apples/package.js
  api.use([
    'my-domain:external-dependencies',
    'my-domain:fruit',
  ]);

  //packages/fruit/package.js
  api.use([
    'my-domain:external-dependencies',
  ]);

  //packages/external-dependencies/package.js
  api.imply([
    'accounts-password',
    'blaze-html-templates',
    'ecmascript',
    'es5-shim',
    'jquery',
    'meteor-base',
    'mobile-experience',
    'mongo',
    'reactive-dict',
    'reactive-var',
    'random',
    'standard-minifiers',
    'tracker',
  ]);

  api.imply([
    'momentjs:moment',
    'okgrow:promise',
    'useraccounts:materialize',
  ], ['client', 'server']);  
  ```

  Meteor core packages are also external dependencies.


Client / Server / Lib
---------------------

- [4.1](4.1) <a name='4.1'></a> **Definition**: Where a file is loaded is defined in [`package.js`](http://docs.meteor.com/#/full/pack_addFiles). Avoid other control mechanisms.

  > Why? `if` statements make WebStorm / PHPStorm indent your code, `client` / `server` / `lib` folders don't work for `cordova`, and comments may be wrong. The package definition is executing documentation. The Meteor documentation does not specify how the different mechanisms interact with each other if you use them together.

  Avoid using `if (Meteor.isClient)`, `client` / `server` / `lib` folders or comments on top of the file to indicate where a file runs.


Style
-----

- [5.1](5.1) <a name='5.1'></a> **Style guide**: Optionally use [AirBNB](https://github.com/airbnb/javascript).

- [5.2](5.2) <a name='5.2'></a> **Indentation**: Use this repo's [editorconfig](http://editorconfig.org/).


Contributing
------------

This document is intended for Cell[0] internal use. Forking is encouraged.
