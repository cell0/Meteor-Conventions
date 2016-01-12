Meteor Conventions
==================

Conventions used by Cell[0] on Meteor projects


Table of contents
-----------------

  1. [Introduction](#introduction)
  1. [Folder Structure](#folder-structure)
  1. [Client / Server / Lib](#client-server-lib)
  1. [Style](#style)


Introduction
------------

This document aims to define clear conventions as much as possible.

However, Meteor is a very flexible tool. We tend to use it for projects that can be very different in nature. This is why for many important choices, there is not one approach 'to rule them all'. In these cases this document describes options and why to choose them.


Folder structure
----------------

- [2.1](#2.1) <a name='2.1'></a> **Client code**: No convention defined yet.

  There are two choices to make:

  + Package or non-package
  + One folder or distrubution [across topic folders](#2.2)

  Placing the code into one or more packages gives you the advantage of controlling the file load order. However, the client and non-client code in two clearly distinct places often makes the project much more clear.  

  *Todo: Write one vs distribution*

- [2.2](#2.2) <a name='2.2'></a> **Packages**: Packages-for-everything, separated per topic.

  > Why? Packages give you control of file loading order.



- [2.3](#2.3) <a name='2.3'></a> **Distribution**: Separated code per topic.

  > Why? Having *intent on top* makes it easy to find where things are happening, and for developers to work side-by-side on the same project simultaneously.

  ```
  packages/financial/package.js
  packages/financial/invoices/invoice.js
  packages/financial/invoices/invoiceCollection.js
  ```

Depending on 

This convention has not yet been established for client code (which includes web clients and mobile clients).



As a rule of thumb, apply **intent on top**.



To quote the Meteor docs:

> **Method 3: Packages**
> 
> This is the ultimate in code separation, modularity, and reusability. If you put the code for each feature in a separate package, the code for one feature won't be able to access the code for the other feature except through exports, making every dependency explicit. This also allows for the easiest independent testing of features. You can also publish the packages and use them in multiple apps with `meteor add`.
> 
> ```
> packages/apples/package.js     # files, dependencies, exports for apple feature
> packages/apples/<anything>.js  # file loading is controlled by package.js
> 
> packages/oranges/package.js    # files, dependencies, exports for orange feature
> packages/oranges/<anything>.js # file loading is controlled by package.js
> ```


Client / Server / Lib
---------------------

Where a file is loaded is defined in [`package.js`](http://docs.meteor.com/#/full/pack_addFiles).

Don't use `if (Meteor.isClient)`, `client` / `server` / `lib` folders or comments on top of the file to indicate where a file runs. *If statements make your code ugly, the folders don't work for `cordova`, and comments may be wrong. The package definition is executing documentation.*


Style
-----

- [4.1](#4.1) <a name='4.1'></a> **Style guide**: Optional AirBNB.

- [4.2](#4.2) <a name='4.2'></a> **Indentation**: Use this repo's editorconfig.
