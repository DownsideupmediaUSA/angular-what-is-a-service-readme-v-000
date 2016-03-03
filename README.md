# What is a Service?

## Overview

We've thrown around the idea of services before - let's dig in deep and learn all about them!

## Objectives

- Describe the role of a Service
- Describe dependency injection to inject Services
- Inject a Service into a Controller
- Use the Service inside the Controller

## Our little helpers

Services are helpers. They're JavaScript functions and are responsible for doing specific tasks only. For example, we might have a `UserService` that communicates with our API for everything user based. Or a `NotificationService` to deal with showing notifications to the user.

Services can be used anywhere and everywhere. It's what makes Angular so useful - we can reuse our code over and over so we don't have to repeat ourselves.

## Where do they come from?

It's all great being able to create services, but how do we get them when we need them? Introducing another piece of Angular magic - Dependency Injection.

Dependency Injection is something you never knew you wanted until it's been given to you - now you won't be able to live without it. Dependency Injection allows us to define *what* we want our controllers to have access to and Angular gives them it!

For instance, we could have 123 different services in our Angular application, but our controller only wants to use three of them. It's important to only include the services we need to use otherwise we may have a massive impact on performance. To do this, all we need to do is specify the three services names as parameters for our controller:

```js
function ContactController(NotificationService, UserService, AuthService) {
  NotificationService.notify('Hello!');
}
```

Angular then, before initiating our controller, looks at what parameters we require and takes a note of them. They are all identified using their names. Then when we initiate our controller, Angular knows exactly what services we need to be "injected".

You'll notice that we've actually done something like this already with `$scope`. We don't have to use `$scope`, but as we specify it as a parameter to our controller, Angular injects it for us. We could have put `$scope` as the second or fifth parameter - it wouldn't matter. 

Our `NotificationService` could look like this: 

```js
function NotificationService() {
  this.notify = function (message) {
    alert(message);
  };
}

angular
  .module('app')
  .service('NotificationService', NotificationService);
```

Notice how we tell Angular about our service in a similar way that we notify it about our controllers - we use `.service` on our modules. We attach all our methods to the `this` keyword as they're properties. Then, we can access all created properties in our controllers. What is important here is the first paramater - this is the name of our service and will be used when we need to inject it elsewhere. The function doesn't need to have the same name, but for debugging purposes, we keep it the same (as it'll be printed in the console if we ever get errors.)
<p data-visibility='hidden'>View <a href='https://learn.co/lessons/angular-what-is-a-service-readme'>Angular What Is A Service</a> on Learn.co and start learning to code for free.</p>
