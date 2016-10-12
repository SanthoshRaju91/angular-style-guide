+++
date = "2016-10-12T02:16:19-04:00"
draft = false
title = "Services & Factories"

+++

There are 3 ways to instantiate a service in angular JS

   * Service
   * Factory
   * Provider

Services in Angular JS are singletons, Services are instantiated with the new keyword, use this for public methods and variables.

<b>Example</b>

```javascript

angular
    .module('app')
    .service('logger', logger);

function logger() {
  this.logError = function(msg) {
    /* */
  };
}


```

Factories are singletons and return an object that contains the members of the service.

<b>Example</b>

```javascript
angular
    .module('app')
    .factory('logger', logger);

function logger() {
    return {
        logError: function(msg) {
          /* */
        }
   };
}
```
For choosing between Service and Factory refer

[Service V/s Factory one and for all](http://blog.thoughtram.io/angular/2015/07/07/service-vs-factory-once-and-for-all.html)

[Angular Factory V/s Service](https://tylermcginnis.com/angularjs-factory-vs-service-vs-provider-5f426cfe6b8c#.ivkojy8de)

Expose the callable members of the service (its interface) at the top, using a technique derived from the Revealing Module Pattern.

<b>Reason</b>

   * Placing the callable members at the top makes it easy to read and helps you instantly identify which members of the service can be called and must be unit tested (and/or mocked).
   * This is especially helpful when the file gets longer as it helps avoid the need to scroll to see what is exposed.
   * Setting functions as you go can be easy, but when those functions are more than 1 line of code they can reduce the readability and cause more scrolling. Defining the callable interface via the returned service moves the implementation details down, keeps the callable interface up top, and makes it easier to read.

```javascript

/* avoid */
function dataService() {
  var someValue = '';
  function save() {
    /* */
  };
  function validate() {
    /* */
  };

  return {
      save: save,
      someValue: someValue,
      validate: validate
  };
}
/* recommended */
function dataService() {
    var someValue = '';
    var service = {
        save: save,
        validate: validate
    };
    return service;

    ////////////

    function save() {
        /* */
    };

    function validate() {
        /* */
    };
}


```

<b>Separate Data Calls</b>

Refactor logic for making data operations and interacting with data to a factory. Make data services responsible for XHR calls, local storage, stashing in memory, or any other data operations.

<b>Reason</b>

The controller's responsibility is for the presentation and gathering of information for the view. It should not care how it gets the data, just that it knows who to ask for it. Separating the data services moves the logic on how to get it to the data service, and lets the controller be simpler and more focused on the view.

<b>Example</b>

```javascript

angular
    .module('app.core')
    .factory('dataservice', dataservice);

dataservice.$inject = ['$http', 'logger'];

function dataservice($http, logger) {
    return {
        getAvengers: getAvengers
    };

    function getAvengers() {
        return $http.get('/api/maa')
            .then(getAvengersComplete)
            .catch(getAvengersFailed);

        function getAvengersComplete(response) {
            return response.data.results;
        }

        function getAvengersFailed(error) {
            logger.error('XHR Failed for getAvengers.' + error.data);
        }
    }
}


```
