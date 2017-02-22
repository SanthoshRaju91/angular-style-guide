+++
date = "2016-10-12T02:16:46-04:00"
draft = false
title = "Directives"

+++

Directives are one of the most powerful components of AngularJS, helping you extend basic HTML elements/attributes and create reusable and testable code.

<b>Types</b>

  Types         |     Usage     
  ---           |     ---
  Attribute     |     `<div book></div>`
  Class         |     `<div class="book"></div>`
  Element       |     `<book data="book_data"></book>`
  Comment       |     `<!--directive:book -->`


<b>Best Practices</b>

   * Create one directive per file. One directive per file is easy to maintain.
   * When manipulating the DOM directly, use a directive.
   * Use bindToController = true when using controller as syntax with a directive when you want to bind the outer scope to the directive's controller's scope.


<b>Using Attribute vs. Element</b>

   * Use your directive as an element name instead of attribute If the need is to create a component with core behavior and possibility to decorate the component with additional behavior in future.
   * Use your directive as an attribute instead of element name when you are adding functionality to an existing element.
   * Always it is recommended to restrict to element and attributes directive.


<b>Naming Convention</b>
Prefer using two or three letter prefix (except ng) while naming directives to avoid collision with future HTML releases. Using “ng” as prefix might collide with AngularJS OOTB directives in future.

```html
<!-- Avoid -->
<example>

<!-- Recommended-->
<my-directive>, <my-test-directive>
```
<b>Directive Scope</b>

    * Directives are one of the most powerful features of AngularJS. You can imagine them as building blocks ( aka re-usable components ) of any    AngularJS application.
    * All directives have a scope associated with them. They use this scope for accessing data/methods inside the template and link function. By default, unless explicitly set, directives don’t create their own scope. Therefore, directives use their parent scope ( usually a controller ) as their own.
    * However, AngularJS allows us to change the default scope of directives by passing a configuration object known as directive definition object

<b>Different types of directive scopes-</b>
  Scope: False - Directive uses its parent scope 

  Example -

<div ng-app="test">
    
    <div ng-controller="Ctrl1">
        <h2 ng-click="reverseName()">Hey {{name}}, Click me to reverse your name</h2>
        <div my-directive class='directive'></div>
    </div>
</div>

var app = angular.module("test",[]);

app.controller("Ctrl1",function($scope){
    $scope.name = "Harry";
    $scope.reverseName = function(){
        $scope.name = $scope.name.split('').reverse().join('');
    };
});

app.directive("myDirective", function(){
    return {
        restrict: "EA",
        scope: false,
        template: "<div>Your name is : {{name}}</div>"+
    };
});

  Since there’s no scope provided in the DDO, the directive uses its parent scope

<b>Clean-up function</b>

   * Consider defining clean-up function by registering an event, element.on( ‘$destroy’, …).
   * It is a good practice to remove event listeners once the ‘$destroy’ event is broadcasted, to avoid instances of memory leaks.
   * Listeners registered to scopes and elements are automatically cleaned up when they are destroyed.
