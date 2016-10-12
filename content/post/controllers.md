+++
date = "2016-10-12T02:16:26-04:00"
draft = true
title = "Controllers"

+++

The controller in AngularJS is a function that adds additional functionality to the scope of the view. We use it to set up an initial state and to add custom behavior to the scope object.

## Standard rules for the Controller
   * It is a best practice to keep our controllers as slim as possible. It’s bad practice to allow any DOM interaction or data manipulation inside the controller.
   * Controllers should hold zero logic Controllers should bind references to Models only (and call methods returned from promises).
   * Try to avoid injecting $scope into Controllers, such as avoiding $scope.$watch().

## Do not use Controller for

   * Manipulate DOM — Controllers should contain only business logic. Putting any presentation logic into Controllers significantly affects its testability. Angular has databinding for most cases and directives to encapsulate manual DOM manipulation.
   * Format input — Use angular form controls instead.
   * Filter output — Use angular filters instead.
   * Share code or state across controllers — Use angular services instead.
   * Manage the life-cycle of other components (for example, to create service instances).


## controllerAs View Syntax

Use the controllerAs syntax over the classic controller with $scope syntax.

```html
<!-- avoid -->
<div ng-controller="myController">
    {{ name }}
</div>

```

```html
<!-- recommended -->
<div ng-controller="myController as ctrl">
    {{ ctrl.name }}
</div>

```

## Reason

   * It promotes the use of binding to a "dotted" object in the View (e.g. customer.name instead of name), which is more contextual, easier to read, and avoids any reference issues that may occur without "dotting".
   * Helps avoid using $parent calls in Views with nested controllers.
   * The controllerAs syntax uses this inside controllers which gets bound to $scope.\
   * Helps avoid the temptation of using $scope methods inside a controller when it may otherwise be better to avoid them or move the method to a factory, and reference them from the controller.


   ```javascript
   /* avoid */
    function CustomerController($scope) {
        $scope.name = {};
        $scope.sendMessage = function() { };
    }

```

```javascript
  /* better */
  function CustomerController() {
      this.name = {};
      this.sendMessage = function() { };
  }

```

Use a variable for this when using the controllerAs syntax

```javascript
  /* recommended  */
  function CustomerController() {
      var self = this;
      self.name = {};
      self.sendMessage = function() { };
  }

```

<b>More Examples</b>

```html
<!-- Avoid -->
<div ng-controller="BaseCtrl">
  {{ name }}
  <div ng-controller="SectionCtrl">
    {{ name }}
    <div ng-controller="FinalCtrl">
      {{ name }}
    </div>
  </div>
</div>
```

In case of nested controllers we can see that each controller is accessing the name property, but the question is: which one? That code looks very confusing.

Using the controllerAs syntax

```html
<!-- Recommended -->
<div ng-controller="BaseCtrl as base">
  Base scope: {{ base.name }}
  <div ng-controller="SectionCtrl as section">
    Section scope: {{ section.name }}
    Base scope: {{base.name}}
    <div ng-controller="FinalCtrl as final">
      {{ final.name }}
    </div>
  </div>
</div>
```
