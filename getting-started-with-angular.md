# Getting Started with Angular

<details><summary style="font-size:1.5em">Prologue</summary>
<p>In one of my previous jobs, I used Angular 2 (and later versions) to build from scratch the front-end for a complete full-stack application. I loved the simplicity of Angular components, the elegance of one-way and two-way bindings, scoped CSS, and the power of TypeScript.</p>
<p>Here I revisit the basics, which is really important to eliminate the "activation-energy" needed to start a new project. The <a href="https://angular.io/guide/quickstart">official documentation</a> is great, and I urge you to read it, but reading different perspectives (such as this post) can help you understand things better. This one is for beginners to Angular, or those who need a quick refresher.</p>
</details>

## Prerequisites
I will be using the latest 64-bit versions of Visual Studio Code (1.20.1), Node (10.13.0) and Angular (7.0.0) at the time of writing. This version of Node comes with version of 6.4.1 of Node Package Manager (NPM). 

### Download links
- [VS Code](https://code.visualstudio.com/download) If asked, check the "automatically install the necessary tools" checkbox during install. Note: This might force reboot your machine multiple times.
- [Node.JS](https://nodejs.org/en/download/)


## Starting Up
Only 4 simple commands are all it takes to get going:
```sh
npm install -g @angular/cli    # globally install the ng command
ng new angular-starter         # create a new project
cd angular-starter             
ng serve                       # starts HTTP server and file watcher
```

In the second command, Angular will:
1. Ask you to have Angular routing (I selected yes) and
2. Choose to have a stylesheet format (I selected LESS - that rhymes).

`LESS` is a CSS compiler, and so are the other options `SASS` and `SCSS`. They are similar, but LESS is JavaScript based, wheras SCSS is Ruby based. SASS is an older version of SCSS.

In the 4th command, Angular will start an HTTP server at port 4200. On Windows, this can bring up the Windows Firewall security dialog. (I allowed Node to access the network for both private and public networks.) It also starts watching file changes, to continuously build and serve the most updated files.

The server by default can be accessed via `http://localhost:4200/`.

## Creating Your First Component

A component allows you to, well componentize, parts of your user-interface so they can be reused in multiple places. To see how this works, let's create a simple component.

In the root folder of your project do:
```sh
ng g component list-of-links
```
This will do a few things:
1. Create a new folder called list-of-links under src/apps
2. Create the HTML, Less, TS and Spec.TS files in that folder
3. Import your component in `app.module.ts` and make it part of the module by including it in the `declarations` array.

> Your component can now be referenced in any HTML file using its `selector` defined in the TS file. By default, components get the `app-` prefix, which you can configure using the `prefix` field in `angular.json`.

Next, do the following:

1. Cut the HTML section defined by the `<ul>...</ul>` tags from `app.component.html`.
2. Put in `<app-list-of-links></app-list-of-links>` where the `ul` tags used to live.
3. Paste what you cut into `list-of-links.component.html`.
4. Save all files and check `http://localhost:4200` to see that the list is still shown.
5. If there are any issues, use the Developer Tools in your browser and check any error messages in the console.

The component here is completely static. To make it dynamic, we can create `bindings` to variables of the view's class.

In the component's TS file, create a class member as follows:

```TypeScript
  items = [
    { href: "https://angular.io/tutorial", label: "Tour of Heroes" },
    { href: "https://github.com/angular/angular-cli/wiki", label: "CLI Documentation" },
    { href: "https://blog.angular.io/", label: "Angular blog" }
  ];    
```

Edit the component's HTML file to have only the following:

```html
<ul *ngIf="items?.length">
  <li *ngFor="let item of items">
    <h2><a target="_blank" rel="noopener" [href]="item.href">{{ item.label }}</a></h2>
  </li>  
</ul>
```

While functionally the same as before, this change allows our component to display an arbitrary number of links defined in the list. In a real-world application, the data would be retrieved from a web service.

Let's look at this new syntax in detail.

1. In the `ul` element, ***ngIf** evaluates the expression to determine whether its element should be included in the view. Here we're using the null-coalescing operator, which is shorthand for items && items.length. If items is undefined or is empty, this section will be skipped completely.
2. In the `li` element, ***ngFor** is indicating that we want an instance of this element for each item in the items array (or none if items is empty). The `of` keyword is important here.
3. In the `a` element, the **square brackets** around `href` is indicating that its value should be _one-way bound_ to the expression `item.href`. Item takes on the value of each object as Angular iterates over the items array. 
4. The **double curly brackets** around `item.label` is also a one-way binding.

If using one-way binding for an HTML attribute, use square brackets around the attribute name. If using one-way binding for HTML content, use double curly brackets around the expression.

It's also possible, and very simple, to do _two-way binding_ for input controls such as the input box. The syntax for this is `[(attribute)]="field"`. This is really a shorthand. An equivalent, albeit not as elegant, appriach is to set up the one-way binding in one direction, and define an event handler for the opposite direction: `[attribute]="field" (attributeChange)="field=$event"`. **Change** prefix is used by convention.  **$event** is an important keyword that denotes the argument passed to the component's `EventEmitter`'s `emit` method, which then calls our event handler. The event handler is defined inline and sets the field to the new value. 

Note that the value side of a two-way binding cannot be an expression: it has to be a _field_ or a _property_ of the class. The field or the setter of that property should be decorated with `@Input()`.

---

This is just the tip of the iceberg, but should cover enough ground to get you going. Make sure to check out my next post [Key Concepts in Angular](./angular-key-concepts.html), which would have been part of this post had it been not so long.
