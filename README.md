# AngularJS List Style Guide

## Purpose
*Opinionated Angular style guide for teams by [Fagner Silva Martins](https://www.linkedin.com/in/fagner-silva-martins-54780539/)*

If you are looking for an opinionated style guide for improve the performance of your project listing, conventions, and structuring Angular applications, then step right in. These styles are based on my development experience with [Angular](//angularjs.org).

## Table of Contents

  1. [To minimize creation of DOM elements in ngRepeat](#ng-repeat)
  1. [Optimize performace with One-time binding](#one-time)
  1. [Optimize performace to ng-show, ng-hide, ng-if and ng-repeat](#directives)
  1. [References](#reference)

## To minimize creation of DOM elements in ngRepeat

### Rule Track by
###### [Style [Y001](#style-y001)]

  - Always use `track by` in ng-repeat.

  *Why?*: ngRepeat will know that all other items already have DOM elements, and will not re-render them.

  ```html
  <!-- avoid -->
  <div ng-repeat="model in collection">
    {{model.name}}
  </div>
  ```

  ```html
  <!-- recommended -->
  <div ng-repeat="model in collection track by $index">
    {{model.name}}
  </div>
  ```
### Rule LimitTo
###### [Style [Y002](#style-y002)]

  - Use `limitTo` to avoid mass insertion in the list to be displayed. 
  
  *Why?*: Mass insertion causes a considerable delay in rendering leaving the feeling of slowness to the user. 
  
  ```html
  <!-- avoid -->
  <div ng-repeat="model in collection">
    {{model.name}}
  </div>
  ```
  
  ```html
  <!-- recommended -->
  <div ng-repeat="model in collection | limitTo : limit track by $index">
    {{model.name}}
  </div>
  ```
  
  *Note*: The increment of the variable that determines the `limitTo` must be placed in the function that executes the next page.

## Optimize performace with One-time binding

### Rule One-time binding
###### [Style [Y010](#style-y010)]

 - Use `::` for considered a unique expression.
 
 *Why?*: Using this expression avoids creating watches by decreasing rendering time.
 
 ```html
  <!-- avoid -->
  <div ng-controller="EventController">
    <p>Name: {{name}}</p>
  </div>
  ```
 ```html
  <!-- recommended -->
  <div ng-controller="EventController">
    <p>Name: {{::name}}</p>
  </div>
  ```
*Caution*: Do not use this expression for variables that can be updated while the page is displayed.

## Optimize performace to ng-show, ng-hide, ng-if and ng-repeat 

### Rule ng-show, ng-hide and ng-if 
###### [Style [Y020](#style-y020)]

- Never call a function directly to `ng-show`, `ng-hide` and `ng-if` directives.

*Why?*: The function will be called in all scope updates.

```html
  <!-- avoid -->
  <div ng-show="myFunction()">
    ...
  </div>
  ```
  Change your function to a variable
  
  ```html
  <!-- recommended -->
  <div ng-show="showDiv">
    ...
  </div>
  ```
  
### Rule ng-repeat 
###### [Style [Y021](#style-y021)]

- Never call a function directly to `ng-repeat` directive.

*Why?*: As `ng-show` the function will be called in all scope updates.

```html
  <!-- avoid -->
  <div ng-repeat="model in myFunctionGetCollection()">
    ...
  </div>
  ```
  Change your function to a variable
  
  ```html
  <!-- recommended -->
  <div ng-repeat="model in collection">
    ...
  </div>
  ```
  ## References
  ### Angular docs
  For anything else, API reference, check the [Angular documentation](//docs.angularjs.org/api).
  
  [Tracking and Duplicates](https://docs.angularjs.org/api/ng/directive/ngRepeat#tracking-and-duplicates).
  [limitTo](https://docs.angularjs.org/api/ng/filter/limitTo).
  [One-time binding](https://code.angularjs.org/1.3.15/docs/guide/expression#one-time-binding).
  
