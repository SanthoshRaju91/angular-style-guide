+++
date = "2016-10-12T02:17:46-04:00"
draft = true
title = "Angular $ Wrapper Services"

+++

When building an Angular applications avoid using default Javascript web API’s like document, window, setTimeout and setInterval, because Angular has a set of services provided that support these API’s.

   <b>Use $document & $window instead of document and window of default Javascript API’s.</b>

   These services are wrapped by Angular and more easily testable than using document and window in tests. This helps you avoid having to mock document and window yourself.

   <b>Use $timeout and $interval instead of setTimeout and setInterval.</b>

   These services are wrapped by Angular and more easily testable and handle Angular's digest cycle thus keeping data binding in sync.
