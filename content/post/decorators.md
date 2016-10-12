+++
date = "2016-10-12T02:18:29-04:00"
draft = false
title = "Decorators"

+++

Decorators are a design pattern that is used to separate modification or decoration of a class without modifying the original source code. In Angular, decorators are functions that allow a service, directive or filter to be modified prior to its usage.

There are two ways to register decorators.

  * $provide.decorator (In Angular 1.4.x modules have decorator method, this method no longer needed)
  * module.decorator

Each provide access to a $delegate, which is the instantiated service/directive/filter, prior to being passed to the service that required it.

<b>Example and Reference</b>

[Angular Decorators](https://docs.angularjs.org/guide/decorators)
