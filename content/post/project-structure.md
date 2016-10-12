+++
date = "2016-10-12T02:15:37-04:00"
draft = true
title = "Project Structure"

+++

## Standard Structure

<b>Description:</b>  This is a very typical app structure that I see. On the surface, it seems to make a lot of sense and is very similar to a lot of MVC frameworks. We have a separation of concerns, controllers have their own folder, views have their own folder, external libraries have their own folder, etc.


<b>Drawback:</b> The disadvantage of this structure is when you have more number of controllers, views and directives, you are going to have to do a lot of scrolling in your directory tree to find the required files, thus not suitable for larger projects.

## Recommended Structure

<b>Description:</b> An ideal AngularJS app structure should be modularized into very specific functions. In the above structure we have separate folder for app specific functionality. This we can modularize the above structure and thus helps in handling large projects.

<b>Advantages:</b>

   * CODE MAINTAINABILITY- The above structure will logically compartmentalize apps and will easily be able to locate and edit code.
   * SCALABLE-  Code will be much easier to scale. Adding new directives and pages will not add bloat to existing folders.
   * DEBUGGING- Debugging your code will be much easier with this modularized approach to app development. It will be easier to find the offending pieces of code and fix them.
   * TESTING- Writing test scripts and testing modernized apps is a whole lot easier then non-modularized ones.
