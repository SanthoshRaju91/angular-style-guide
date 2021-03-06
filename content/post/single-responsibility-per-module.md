+++
draft = false
title = "single responsibility per module"

+++

Define 1 component per file.

The following example defines the app module and its dependencies, defines a controller, and defines a factory all in the same file.

  ``` javascript

  /* avoid */
  angular
      .module('app', ['ngRoute'])
      .controller('SomeController', SomeController)
      .factory('someFactory', someFactory);

  function SomeController() { }

  function someFactory() { }

  ```
The same components are now separated into their own files.

 ```javascript

  /* recommended */

  // app.module.js
  angular
      .module('app', ['ngRoute']);

  /* recommended */

  // someController.js
  angular
      .module('app')
      .controller('SomeController', SomeController);

  function SomeController() { }

  /* recommended */
  
  // someFactory.js
  angular
      .module('app')
      .factory('someFactory', someFactory);

  function someFactory() { }

 ```
