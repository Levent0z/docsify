# Key Concepts in Angular

<details><summary style="font-size:1.5em">Prologue</summary>
<p>In my previous post, <a href="gettings-started-with-angular.html">Getting Started With Angular</a>, I discussed how to quickly set up an Angular project and create a basic, reusable component. In there, I demonstrated the syntax for conditional inclusion (*ngIf), repeaters (*ngFor) and one-way binding and briefly touched on two-way binding.</p>
<p>In this post, I take a step back and discuss some of the key concepts of Angular. Any Angular developer should have a thorough understanding of these concepts.</p>
</details>

## Components
A `Component` is a visual element, a user-interface control that has 4 parts:
1. an HTML file that defines the `View`,
2. a LESS (or SCSS/SASS) file that defines optional styling of that view,
3. a TypeScript (.TS) file that defines the logic that drives that component,
4. a spec (.SPEC.TS) file that contains the unit test for that component.

Quick notes:
- The HTML file for a component is not a full HTML document but a fragment.
- Styling is scoped to the component. Any CSS rules defined for that component will not affect others, unless explicitly written to go beyond the scope.
- TypeScript is a transpiler that transpiles down to pure JavaScript. If you're used to modern ECMAScript standards (using `class`, for example) then the switch shouldn't too difficult. 
- For testing, Angular uses [Karma](https://karma-runner.github.io/latest/index.html) test runner, which uses [Jasmine](https://jasmine.github.io/) -- a behavior-driven development framework for testing.
- By convention, a component's name uses _component-name_.**component**._file_extension_.
- Every app has at least one component.
- The app `module` declares app.component to be the `bootstrap` component.

> Components are used to display or manipulate data -- they should not store the data. This is because a component's life-cycle is determined by the app's UI and it may come and go as needed. For example, a panel may exist only to show a message and disappear. Data and state should be controlled by `services`.

## Services
A `Service` is just a regular TypeScript class that's used to provide non-view-related functionality and/or store state. 

A service can be introduced as a `provider` or a `viewProvider` to the component hierarchy. The difference between them is important to know but I will defer it for another post. I will simply refer to both as "provider" from now on.

Service classes are decorated with `@Injectable()` so they can participate in Angular's dependency injection system. 

Components are typically created and destroyed **automatically** based on what's going on with the view. We don't `new` the component classes. This is fine for components whose constructors have no arguments, but what if they do? This is where the dependency injection system comes in. 

The arguments to the constructor are the class' _dependencies_. When a constructor argument is of an injectable type, and that type is declared as a provider __for that component or one of its ancestors in the component hierarchy__, Angular will pass in the correct service instance. Which one is that? Angular will start at the component's providers list, and walk up the component hierarchy all the way to the root component (i.e. `app.component`) and finally to the `app.module` until it finds the instance. It will fail with a runtime error if it can't.

This means:
- services that should live for the life of the app should be defined at the module or app.component level. 
- a **different instance** of the service will be used for each instance of the component where the service is defined. The service lives and dies with the component that defines it.
- the descendants of a component will use the **same instance** of the service as the ancestor component that defined it (unless they themselves define the provider and override the instance).

> The key takeaway is that a shared service should be defined further up in the component hierarchy but only as high as it's needed.

## Routes

A **`route`** is an entry in the routes array defined in `app-routing.module.ts`. Each entry maps a token of the path part of the URI to a component, and can have child entries. Route ordering is important as Angular matches the URI path top-to-bottom. 
For example:

```TypeScript
const routes: Routes = [
   { path: '', redirectTo: 'welcome', pathMatch: 'full' },
   { path: 'welcome', component: WelcomeComponent },
   { path: 'home', component: HomeComponent, children: [
      { path: 'items', component: ItemsComponent },
      { path: ':id', component: ItemComponent }
   ]}
];
```

Parent components have a a special HTML element called `router-outlet` that acts as a placeholder and defines where the child component should live. Note that it's possible to have multiple `router-outlet` elements in a component so long as they have unique values for their `name` attributes. Route entries can target these placeholders with the `outlet` field. 

In the above configuration, a URL like: 
- _https://hostname_ maps to the empty path route, which redirects to the welcome route, which then activates the WelcomeComponent.
- _https://hostname/home/items_ maps the home route (skips the empty path route due to the pathMatch rule) and activates the home component. Next it maps to the items route, and activates an `ItemsComponent` where `router-outlet` is defined in `HomeComponent`'s view. 
- _https://hostname/home/5_ maps to the home route and activates `HomeComponent` like before. The `id` variable (designated with the colon character) gets the value 5, which is passed to an `ItemComponent`, which is activated at the `router-outlet` of home.

## More Reading
- [(Official) Architecture Overview](https://angular.io/guide/architecture)
- [Named Router Outlets](https://onehungrymind.com/named-router-outlets-in-angular-2/)