# Angular

# Section 1: Getting Started

---

## 1. Welcome To The Course!

**What is this:** An introduction to the Angular course, covering what you'll learn and how the course is structured

**Description:** The instructor walks through the course goals, prerequisites, and what to expect. Angular is a full-featured frontend framework maintained by Google, used for building scalable single-page applications.

**Examples:**

```bash
# Prerequisites
- Basic HTML, CSS, JavaScript knowledge
- Familiarity with TypeScript is helpful but not required
```

---

## 2. What Exactly Is Angular?

**What is this:** A definition and conceptual overview of the Angular framework.

**Description:** Angular is a component-based frontend framework built with TypeScript. It provides a complete solution out of the box — routing, forms, HTTP, dependency injection, and more — unlike libraries such as React which require assembling those pieces yourself.

**Examples:**

```ts
// Angular is opinionated — it gives you structure
// A minimal Angular component looks like this:
import { Component } from '@angular/core';

@Component({
  selector: 'app-root',
  template: `<h1>Hello Angular</h1>`,
})
export class AppComponent {}
```

---

## 3. Why Would You Use Angular?

**What is this:** The case for choosing Angular over other frontend options.

**Description:** Angular is a good fit when you need a batteries-included, enterprise-ready framework with strong conventions. It enforces consistent architecture across large teams and long-lived projects. Its tight TypeScript integration and built-in tooling reduce decision fatigue.

**Examples:**

```ts
// Angular gives you dependency injection out of the box
import { Injectable } from '@angular/core';

@Injectable({ providedIn: 'root' })
export class UserService {
  getUser() {
    return { name: 'Alice' };
  }
}

// Inject it anywhere — no manual wiring
import { Component } from '@angular/core';
import { UserService } from './user.service';

@Component({ selector: 'app-profile', template: `<p>{{ user.name }}</p>` })
export class ProfileComponent {
  user = this.userService.getUser();
  constructor(private userService: UserService) {}
}
```

---

## 4. Angular's Evolution & Stability

**What is this:** A look at Angular's versioning history and commitment to backward compatibility.

**Description:** Angular follows semantic versioning with predictable major releases every 6 months. The Angular team provides long-term support (LTS) for major versions and clear migration paths. Recent versions (v14+) introduced standalone components, and v17+ brought a new control flow syntax, making Angular more ergonomic without breaking existing code.

**Examples:**

```ts
// Old module-based approach (still valid)
@NgModule({
  declarations: [AppComponent],
  bootstrap: [AppComponent],
})
export class AppModule {}

// Modern standalone approach (v14+)
@Component({
  selector: 'app-root',
  standalone: true,
  template: `<h1>Standalone Component</h1>`,
})
export class AppComponent {}
```

---

## 5. New Angular Projects (>= v21)

**What is this:** What changes and defaults apply when starting a new Angular project at version 21 and above.

**Description:** Angular v21 projects use standalone components by default, the new `@if` / `@for` control flow syntax, and zoneless change detection is available experimentally. The CLI scaffolds a modern project structure without legacy NgModules.

**Examples:**

```ts
// New control flow syntax (v17+, default in v21 projects)
@Component({
  standalone: true,
  template: `
    @if (isLoggedIn) {
      <p>Welcome back!</p>
    } @else {
      <p>Please log in.</p>
    }

    @for (item of items; track item.id) {
      <li>{{ item.name }}</li>
    }
  `,
})
export class DashboardComponent {
  isLoggedIn = true;
  items = [{ id: 1, name: 'Angular' }];
}
```

---

## 6. Creating A New Angular Project

**What is this:** Step-by-step process for scaffolding a new Angular application using the Angular CLI.

**Description:** The Angular CLI (`@angular/cli`) is the standard tool for generating, building, and serving Angular projects. `ng new` creates a fully configured project with TypeScript, ESLint, and a dev server ready to go.

**Examples:**

```bash
# Install the Angular CLI globally
npm install -g @angular/cli

# Create a new project
ng new my-angular-app

# Prompts:
# ? Which stylesheet format would you like to use? CSS
# ? Do you want to enable Server-Side Rendering (SSR)? No

# Navigate into the project and start the dev server
cd my-angular-app
ng serve
# App available at http://localhost:4200
```

```bash
# Key files created by ng new
my-angular-app/
├── src/
│   ├── app/
│   │   ├── app.component.ts      # Root component
│   │   ├── app.component.html    # Root template
│   │   └── app.config.ts         # App-level providers
│   └── main.ts                   # Bootstrap entry point
├── angular.json                  # CLI configuration
├── tsconfig.json                 # TypeScript configuration
└── package.json
```

---

## 7. Setting Up An Angular Development Environment

**What is this:** Installing and configuring the tools needed for Angular development.

**Description:** A proper Angular dev environment needs Node.js, npm, the Angular CLI, and a good editor. VS Code with the Angular Language Service extension provides autocomplete, inline errors, and template type-checking.

**Examples:**

```bash
# 1. Install Node.js (LTS recommended)
# https://nodejs.org

# 2. Verify installation
node -v   # e.g. v22.x.x
npm -v    # e.g. 10.x.x

# 3. Install Angular CLI
npm install -g @angular/cli

# 4. Verify CLI
ng version

# 5. Recommended VS Code extensions:
# - Angular Language Service (angular.ng-template)
# - ESLint
# - Prettier
```

---

## 8. About This Course

**What is this:** An overview of how the course is organized and how to get the most out of it.

**Description:** The course is structured progressively — starting with Angular fundamentals and building toward real-world application patterns. Each section builds on the previous one. Code examples and resources are provided alongside video lessons.

**Examples:**

```bash
# Recommended approach
# 1. Watch the video first
# 2. Read the notes in this README for each lesson
# 3. Type out the examples yourself — don't copy-paste
# 4. Experiment: break things and fix them
# 5. Build a small side project to reinforce each section
```

---

# Section 2: Angular Essentials - Components, Templates, Services & More

---

## 10. Module Introduction

**What is this:** An overview of what Section 2 covers — the core building blocks of every Angular application.

**Description:** This section covers everything you need to build real Angular apps: components, templates, data binding, events, signals, inputs/outputs, directives, services, and dependency injection. All examples use modern Angular (v17+) with standalone components and TypeScript.

**Examples:**

```ts
// The three things every Angular app is built from:
// 1. Components — UI blocks with logic + template
// 2. Services — shared business logic
// 3. Dependency Injection — wiring them together
```

---

## 11. A New Starting Project & Analyzing The Project Structure

**What is this:** Walkthrough of a freshly generated Angular project and what each file does.

**Description:** `ng new` creates a predictable folder structure. The entry point is `main.ts`, which bootstraps the root component. `angular.json` configures the CLI. All app code lives under `src/app/`.

**Examples:**

```
src/
├── app/
│   ├── app.component.ts       # Root component class + metadata
│   ├── app.component.html     # Root template
│   ├── app.component.css      # Component-scoped styles
│   └── app.config.ts          # App-level providers (replaces AppModule)
├── main.ts                    # Bootstraps the app
└── index.html                 # Shell HTML — <app-root> lives here
```

```ts
// main.ts — bootstraps the standalone root component
import { bootstrapApplication } from '@angular/platform-browser';
import { AppComponent } from './app/app.component';
import { appConfig } from './app/app.config';

bootstrapApplication(AppComponent, appConfig);
```

---

## 12. Understanding Components & How Content Ends Up On The Screen

**What is this:** How Angular components render HTML into the browser DOM.

**Description:** Angular reads the `selector` of the root component, finds that tag in `index.html`, and replaces it with the component's template. Child components follow the same pattern — each selector is replaced by its own template, building up the component tree.

**Examples:**

```html
<!-- index.html -->
<body>
  <app-root></app-root>
</body>
```

```ts
// app.component.ts — Angular finds <app-root> and renders this template there
import { Component } from '@angular/core';

@Component({
  selector: 'app-root',
  standalone: true,
  template: `<h1>My Angular App</h1>`,
})
export class AppComponent {}
```

---

## 13. Creating a First Custom Component

**What is this:** Building a reusable component from scratch.

**Description:** Every component is a TypeScript class decorated with `@Component`. The decorator defines the selector (the HTML tag), the template, and optional styles. Standalone components import everything they need directly — no NgModule required.

**Examples:**

```ts
// src/app/header/header.component.ts
import { Component } from '@angular/core';

@Component({
  selector: 'app-header',
  standalone: true,
  template: `
    <header>
      <h1>Task Manager</h1>
    </header>
  `,
})
export class HeaderComponent {}
```

```ts
// app.component.ts — use the custom component
import { Component } from '@angular/core';
import { HeaderComponent } from './header/header.component';

@Component({
  selector: 'app-root',
  standalone: true,
  imports: [HeaderComponent],
  template: `<app-header />`,
})
export class AppComponent {}
```

---

## 14. [Optional] JavaScript Refresher: Classes, Properties & More

**What is this:** A refresher on JS/TS class syntax used throughout Angular.

**Description:** Angular components are TypeScript classes. Understanding class properties, constructors, access modifiers, and methods is essential for reading and writing Angular code.

**Examples:**

```ts
class User {
  // Class property with type annotation
  name: string;
  age: number;

  constructor(name: string, age: number) {
    this.name = name;
    this.age = age;
  }

  greet(): string {
    return `Hi, I'm ${this.name}`;
  }
}

// Shorthand — TypeScript constructor parameter properties
class User {
  constructor(public name: string, private age: number) {}

  greet() {
    return `Hi, I'm ${this.name}`;
  }
}
```

---

## 15. Configuring the Custom Component

**What is this:** Setting up a component's selector, template, and styles via the `@Component` decorator.

**Description:** The `@Component` decorator accepts a configuration object. You can inline the template with `template` or point to a file with `templateUrl`. Same for styles: `styles` (inline array) or `styleUrl` (file path).

**Examples:**

```ts
// Inline template and styles
@Component({
  selector: 'app-header',
  standalone: true,
  template: `<h1>Hello</h1>`,
  styles: `h1 { color: navy; }`,
})
export class HeaderComponent {}

// External files (typical for larger components)
@Component({
  selector: 'app-header',
  standalone: true,
  templateUrl: './header.component.html',
  styleUrl: './header.component.css',
})
export class HeaderComponent {}
```

---

## 16. Using the Custom Component

**What is this:** Placing a child component inside another component's template.

**Description:** To use a standalone component, add it to the `imports` array of the parent component's `@Component` decorator. Then use its selector as an HTML tag in the template.

**Examples:**

```ts
import { Component } from '@angular/core';
import { HeaderComponent } from './header/header.component';
import { UserComponent } from './user/user.component';

@Component({
  selector: 'app-root',
  standalone: true,
  imports: [HeaderComponent, UserComponent],
  template: `
    <app-header />
    <main>
      <app-user />
    </main>
  `,
})
export class AppComponent {}
```

---

## 17. Styling the Header Component & Adding An Image

**What is this:** Applying component-scoped CSS and rendering images in a template.

**Description:** Styles defined in a component's `styleUrl` are scoped to that component only — they don't leak into child or parent components. Angular adds a unique attribute to elements for encapsulation. Images from the `public/` folder are referenced with a root-relative path.

**Examples:**

```ts
// header.component.ts
@Component({
  selector: 'app-header',
  standalone: true,
  templateUrl: './header.component.html',
  styleUrl: './header.component.css',
})
export class HeaderComponent {}
```

```html
<!-- header.component.html -->
<header>
  <img src="logo.png" alt="App Logo" />
  <h1>Task Manager</h1>
</header>
```

```css
/* header.component.css — only affects this component */
header {
  display: flex;
  align-items: center;
  gap: 1rem;
  background: #1a1a2e;
  color: white;
  padding: 1rem;
}

img {
  width: 48px;
}
```

---

## 18. Managing & Creating Components with the Angular CLI

**What is this:** Using `ng generate component` to scaffold components automatically.

**Description:** The CLI creates the component file, template, styles, and spec file, and wires them up correctly. It's the fastest way to add new components and avoids typos in boilerplate.

**Examples:**

```bash
# Generate a new standalone component
ng generate component user
# Shorthand
ng g c user

# Output:
# CREATE src/app/user/user.component.ts
# CREATE src/app/user/user.component.html
# CREATE src/app/user/user.component.css
# CREATE src/app/user/user.component.spec.ts

# Skip the test file if not needed
ng g c task --skip-tests
```

---

## 19. Styling & Using Our Next Custom Component

**What is this:** Building and styling a second component and composing it into the app.

**Description:** Each component owns its own template and styles. Components are composed by nesting them inside other components' templates. This keeps the UI modular and each piece independently maintainable.

**Examples:**

```ts
// user.component.ts
@Component({
  selector: 'app-user',
  standalone: true,
  templateUrl: './user.component.html',
  styleUrl: './user.component.css',
})
export class UserComponent {}
```

```html
<!-- user.component.html -->
<div class="user">
  <img src="user.jpg" alt="User avatar" />
  <span>Alice</span>
</div>
```

```css
/* user.component.css */
.user {
  display: flex;
  align-items: center;
  gap: 0.5rem;
  padding: 0.75rem;
  border-radius: 8px;
  background: #f5f5f5;
}
```

---

## 20. Preparing User Data (To Output Dynamic Content)

**What is this:** Setting up data in the component class so it can be displayed in the template.

**Description:** Data that should appear in the template is declared as class properties. Angular's template syntax can then read these properties and render them dynamically.

**Examples:**

```ts
@Component({
  selector: 'app-user',
  standalone: true,
  templateUrl: './user.component.html',
})
export class UserComponent {
  // Data that will be used in the template
  name = 'Alice';
  avatar = 'alice.jpg';
}
```

---

## 21. Storing Data in a Component Class

**What is this:** Declaring typed properties on the component class to hold component state.

**Description:** Component classes are plain TypeScript classes. Properties hold the component's state. TypeScript types make the data contracts explicit and enable IDE tooling.

**Examples:**

```ts
@Component({
  selector: 'app-user',
  standalone: true,
  templateUrl: './user.component.html',
})
export class UserComponent {
  name: string = 'Alice';
  age: number = 30;
  isActive: boolean = true;

  // TypeScript infers the type from the initializer — both are valid
  avatar = 'alice.jpg'; // inferred as string
}
```

---

## 22. Outputting Dynamic Content with String Interpolation

**What is this:** Rendering component class properties in the template using `{{ }}`.

**Description:** Double curly braces `{{ expression }}` evaluate a TypeScript expression and render the result as a string in the DOM. You can use properties, method calls, or simple expressions — but keep logic in the class, not the template.

**Examples:**

```ts
@Component({
  selector: 'app-user',
  standalone: true,
  template: `
    <p>Name: {{ name }}</p>
    <p>Greeting: {{ getGreeting() }}</p>
    <p>Upper: {{ name.toUpperCase() }}</p>
  `,
})
export class UserComponent {
  name = 'Alice';

  getGreeting() {
    return `Hello, ${this.name}!`;
  }
}
```

---

## 23. Property Binding & Outputting Computed Values

**What is this:** Binding component data to HTML element properties using `[property]="expression"`.

**Description:** String interpolation outputs text. Property binding sets DOM properties (not attributes) directly. Use `[src]`, `[disabled]`, `[value]` etc. to bind dynamic values to element properties.

**Examples:**

```ts
@Component({
  selector: 'app-user',
  standalone: true,
  template: `
    <!-- String interpolation — renders as text -->
    <p>{{ name }}</p>

    <!-- Property binding — sets the DOM property -->
    <img [src]="avatarPath" [alt]="name" />
    <button [disabled]="!isActive">Activate</button>
  `,
})
export class UserComponent {
  name = 'Alice';
  avatarPath = 'assets/alice.jpg';
  isActive = false;
}
```

---

## 24. Attribute Binding

**What is this:** Binding to HTML attributes (not DOM properties) using `[attr.name]="value"`.

**Description:** Some HTML attributes have no direct DOM property equivalent (e.g. `colspan`, `aria-*`, `data-*`). For these, use `[attr.attributeName]` to bind dynamically.

**Examples:**

```ts
@Component({
  selector: 'app-table',
  standalone: true,
  template: `
    <table>
      <tr>
        <!-- [attr.colspan] — no DOM property for colspan -->
        <td [attr.colspan]="columnSpan">Merged cell</td>
      </tr>
    </table>

    <!-- aria attributes for accessibility -->
    <button [attr.aria-label]="buttonLabel">+</button>
  `,
})
export class TableComponent {
  columnSpan = 3;
  buttonLabel = 'Add item';
}
```

---

## 25. Using Getters For Computed Values

**What is this:** Using TypeScript `get` accessors to derive template values from existing state.

**Description:** Getters let you compute a value from existing properties and expose it to the template as if it were a simple property. This keeps templates clean and avoids duplicating logic.

**Examples:**

```ts
@Component({
  selector: 'app-user',
  standalone: true,
  template: `
    <img [src]="imagePath" [alt]="name" />
    <p>{{ name }}</p>
  `,
})
export class UserComponent {
  name = 'Alice';
  avatar = 'alice.jpg';

  // Computed from other properties — no () needed in the template
  get imagePath(): string {
    return `assets/users/${this.avatar}`;
  }
}
```

---

## 26. Listening to Events with Event Binding

**What is this:** Reacting to DOM events (click, input, submit, etc.) using `(event)="handler()"`.

**Description:** Event binding connects DOM events to component methods. The `$event` object gives you access to the native event if needed.

**Examples:**

```ts
@Component({
  selector: 'app-user',
  standalone: true,
  template: `
    <button (click)="onSelect()">Select User</button>
    <input (input)="onInput($event)" />
  `,
})
export class UserComponent {
  onSelect() {
    console.log('User selected');
  }

  onInput(event: Event) {
    const input = event.target as HTMLInputElement;
    console.log(input.value);
  }
}
```

---

## 27. Managing State & Changing Data

**What is this:** Updating component properties in response to events and reflecting changes in the template.

**Description:** When an event handler modifies a class property, Angular's change detection picks up the change and re-renders the affected parts of the template automatically.

**Examples:**

```ts
@Component({
  selector: 'app-user',
  standalone: true,
  template: `
    <p>Selected: {{ selectedUser }}</p>
    <button (click)="selectUser('Alice')">Alice</button>
    <button (click)="selectUser('Bob')">Bob</button>
  `,
})
export class UserComponent {
  selectedUser = '';

  selectUser(name: string) {
    this.selectedUser = name;
  }
}
```

---

## 28. A Look Behind The Scenes Of Angular's Change Detection Mechanism

**What is this:** How Angular knows when to update the DOM after state changes.

**Description:** By default Angular uses Zone.js, which patches browser APIs (setTimeout, event listeners, etc.) to detect when async operations complete, then checks the entire component tree for changes. This is automatic but can be inefficient for large apps. Signals (covered next) offer a more targeted alternative.

**Examples:**

```ts
// Zone.js change detection — Angular checks everything after any event
@Component({
  selector: 'app-counter',
  standalone: true,
  template: `<p>{{ count }}</p> <button (click)="increment()">+</button>`,
})
export class CounterComponent {
  count = 0;

  increment() {
    this.count++; // Zone.js detects this event, Angular re-checks the template
  }
}
```

---

## 29. Introducing Signals

**What is this:** Angular's reactive primitive for fine-grained, efficient state management.

**Description:** A `signal` is a wrapper around a value that Angular tracks. When a signal's value changes, only the parts of the template that read that signal are updated — no Zone.js full-tree check required. Use `signal()` to create one, `.set()` / `.update()` to change it, and call it like a function `mySignal()` to read it.

**Examples:**

```ts
import { Component, signal, computed } from '@angular/core';

@Component({
  selector: 'app-counter',
  standalone: true,
  template: `
    <p>Count: {{ count() }}</p>
    <p>Double: {{ double() }}</p>
    <button (click)="increment()">+</button>
    <button (click)="reset()">Reset</button>
  `,
})
export class CounterComponent {
  count = signal(0);

  // computed() derives a value from one or more signals
  double = computed(() => this.count() * 2);

  increment() {
    this.count.update(c => c + 1);
  }

  reset() {
    this.count.set(0);
  }
}
```

---

## 30. We Need More Flexible Components!

**What is this:** The motivation for component inputs — passing data from parent to child.

**Description:** Hardcoded values in a component make it useless for reuse. To make a component flexible, it needs to accept data from the outside. Angular solves this with `@Input()` / `input()` — the parent passes data, the child receives it.

**Examples:**

```ts
// Problem — hardcoded, not reusable
@Component({
  selector: 'app-user',
  standalone: true,
  template: `<p>Alice</p>`,  // always "Alice"
})
export class UserComponent {}

// Goal — the parent decides who to show
// <app-user [name]="'Alice'" />
// <app-user [name]="'Bob'" />
```

---

## 31. Defining Component Inputs

**What is this:** Declaring properties that a parent component can pass data into using `@Input()`.

**Description:** Decorate a class property with `@Input()` to make it an input binding. The parent sets it using property binding syntax `[propertyName]="value"`.

**Examples:**

```ts
import { Component, Input } from '@angular/core';

@Component({
  selector: 'app-user',
  standalone: true,
  template: `<p>{{ name }}</p>`,
})
export class UserComponent {
  @Input() name: string = '';
  @Input() avatar: string = '';
}
```

```html
<!-- Parent template -->
<app-user [name]="'Alice'" [avatar]="'alice.jpg'" />
<app-user [name]="'Bob'" [avatar]="'bob.jpg'" />
```

---

## 32. Required & Optional Inputs

**What is this:** Marking inputs as required so Angular errors if the parent forgets to pass them.

**Description:** By default, `@Input()` properties are optional. Passing `{ required: true }` tells Angular to throw a compile-time error if the parent omits the binding.

**Examples:**

```ts
import { Component, Input } from '@angular/core';

@Component({
  selector: 'app-user',
  standalone: true,
  template: `<p>{{ name }}</p>`,
})
export class UserComponent {
  // Required — parent MUST provide this
  @Input({ required: true }) name!: string;

  // Optional — parent may omit this
  @Input() avatar: string = 'default.jpg';
}
```

```html
<!-- Error at compile time: required input 'name' not provided -->
<app-user />

<!-- Correct -->
<app-user [name]="'Alice'" />
```

---

## 33. Using Signal Inputs

**What is this:** The modern, signal-based alternative to `@Input()` using the `input()` function.

**Description:** `input()` returns a signal that the parent can bind to. Unlike `@Input()`, the value is reactive — you read it by calling it as a function `myInput()`. Use `input.required<T>()` for required inputs.

**Examples:**

```ts
import { Component, input, computed } from '@angular/core';

@Component({
  selector: 'app-user',
  standalone: true,
  template: `
    <img [src]="imagePath()" [alt]="name()" />
    <p>{{ name() }}</p>
  `,
})
export class UserComponent {
  // Optional signal input with default
  avatar = input<string>('default.jpg');

  // Required signal input
  name = input.required<string>();

  // Computed value derived from a signal input
  imagePath = computed(() => `assets/users/${this.avatar()}`);
}
```

---

## 34. We Need Custom Events!

**What is this:** The motivation for component outputs — child-to-parent communication.

**Description:** Inputs let data flow down (parent → child). To flow data back up (child → parent), a child emits a custom event. The parent listens with event binding `(eventName)="handler($event)"`.

**Examples:**

```ts
// Pattern:
// Parent passes data down via input:   [selectedUser]="user"
// Child sends data up via output:      (userSelected)="onUserSelected($event)"
```

---

## 35. Working with Outputs & Emitting Data

**What is this:** Emitting custom events from a child component using `@Output()` and `EventEmitter`.

**Description:** Decorate a property with `@Output()` and assign an `EventEmitter`. Call `.emit(value)` to fire the event. The parent listens with `(eventName)="handler($event)"`.

**Examples:**

```ts
import { Component, Input, Output, EventEmitter } from '@angular/core';

@Component({
  selector: 'app-user',
  standalone: true,
  template: `<button (click)="onSelect()">{{ name }}</button>`,
})
export class UserComponent {
  @Input({ required: true }) name!: string;
  @Output() select = new EventEmitter<string>();

  onSelect() {
    this.select.emit(this.name);
  }
}
```

```ts
// Parent
@Component({
  selector: 'app-root',
  standalone: true,
  imports: [UserComponent],
  template: `
    <app-user [name]="'Alice'" (select)="onUserSelected($event)" />
    <p>Selected: {{ selectedUser }}</p>
  `,
})
export class AppComponent {
  selectedUser = '';

  onUserSelected(name: string) {
    this.selectedUser = name;
  }
}
```

---

## 36. Using the output() Function

**What is this:** The modern signal-based alternative to `@Output()` using the `output()` function.

**Description:** `output()` is the new, cleaner way to define component outputs without decorators. It returns an `OutputEmitterRef` — call `.emit(value)` on it just like `EventEmitter`.

**Examples:**

```ts
import { Component, input, output } from '@angular/core';

@Component({
  selector: 'app-user',
  standalone: true,
  template: `<button (click)="onSelect()">{{ name() }}</button>`,
})
export class UserComponent {
  name = input.required<string>();
  select = output<string>();

  onSelect() {
    this.select.emit(this.name());
  }
}
```

---

## 37. Adding Extra Type Information To EventEmitter

**What is this:** Providing a typed payload to `EventEmitter<T>` so the parent gets a typed `$event`.

**Description:** The generic type parameter `EventEmitter<T>` tells TypeScript the shape of the emitted value. The parent's handler receives a correctly typed `$event` with full IDE autocomplete.

**Examples:**

```ts
type User = { id: string; name: string };

@Component({ selector: 'app-user', standalone: true, template: '' })
export class UserComponent {
  @Input({ required: true }) user!: User;

  // Parent receives a typed User object, not `any`
  @Output() select = new EventEmitter<User>();

  onSelect() {
    this.select.emit(this.user);
  }
}

// Parent handler — $event is typed as User
onUserSelected(user: User) {
  console.log(user.id, user.name);
}
```

---

## 38. Exercise: Create a Configurable Component

**What is this:** A hands-on exercise combining inputs and outputs to build a reusable component.

**Description:** The goal is a `TaskComponent` that accepts a task object as an input and emits an event when the task is completed. This exercises everything covered so far: `@Component`, `input()`, `output()`, and template binding.

**Examples:**

```ts
// task.model.ts
export interface Task {
  id: string;
  title: string;
  dueDate: string;
}

// task.component.ts
import { Component, input, output } from '@angular/core';
import { Task } from './task.model';

@Component({
  selector: 'app-task',
  standalone: true,
  template: `
    <article>
      <h3>{{ task().title }}</h3>
      <p>Due: {{ task().dueDate }}</p>
      <button (click)="onComplete()">Complete</button>
    </article>
  `,
})
export class TaskComponent {
  task = input.required<Task>();
  complete = output<string>();

  onComplete() {
    this.complete.emit(this.task().id);
  }
}
```

---

## 39. TypeScript: Working With Potentially Undefined Values & Union Types

**What is this:** Handling values that may be `undefined` or `null` in TypeScript and Angular templates.

**Description:** TypeScript's strict mode flags potentially undefined values. Use union types (`T | undefined`), optional chaining (`?.`), nullish coalescing (`??`), and type narrowing to handle them safely.

**Examples:**

```ts
// Union type — value is either a string or undefined
type MaybeString = string | undefined;

@Component({
  selector: 'app-user',
  standalone: true,
  template: `
    <!-- Optional chaining in template — safe if user is undefined -->
    <p>{{ user?.name ?? 'Guest' }}</p>
  `,
})
export class UserComponent {
  @Input() user: { name: string } | undefined;

  greet() {
    // Type narrowing — TypeScript knows user is defined here
    if (!this.user) return 'Hello, Guest!';
    return `Hello, ${this.user.name}!`;
  }
}
```

---

## 40. Accepting Objects As Inputs & Adding Appropriate Typings

**What is this:** Passing entire objects as component inputs instead of individual properties.

**Description:** Rather than passing each property separately, pass a typed object as a single input. Define the type or interface first, then use it in both the parent (data source) and the child (input type).

**Examples:**

```ts
// user.model.ts
export interface User {
  id: string;
  name: string;
  avatar: string;
}

// user.component.ts
import { Component, input } from '@angular/core';
import { User } from './user.model';

@Component({
  selector: 'app-user',
  standalone: true,
  template: `
    <img [src]="user().avatar" [alt]="user().name" />
    <p>{{ user().name }}</p>
  `,
})
export class UserComponent {
  user = input.required<User>();
}
```

```ts
// app.component.ts
users: User[] = [
  { id: 'u1', name: 'Alice', avatar: 'alice.jpg' },
  { id: 'u2', name: 'Bob', avatar: 'bob.jpg' },
];
```

---

## 41. TypeScript: Type Aliases & Interfaces

**What is this:** Defining named types with `type` aliases and `interface` declarations.

**Description:** Both `type` and `interface` describe the shape of an object. Prefer `interface` for object shapes that may be extended; prefer `type` for unions, intersections, or when you need more complex type expressions. In Angular, either works for model definitions.

**Examples:**

```ts
// Interface — extendable, preferred for object shapes / models
interface User {
  id: string;
  name: string;
  avatar: string;
}

interface AdminUser extends User {
  role: 'admin';
}

// Type alias — preferred for unions and complex types
type Status = 'open' | 'in-progress' | 'done';

type Task = {
  id: string;
  title: string;
  status: Status;
  assignedUser: User | undefined;
};
```

---

## 42. Outputting List Content

**What is this:** Rendering arrays of data in the template with the `@for` control flow block.

**Description:** The `@for` block (Angular v17+) iterates over an array and renders a template for each item. The `track` expression is required — it tells Angular how to identify items for efficient DOM updates.

**Examples:**

```ts
@Component({
  selector: 'app-user-list',
  standalone: true,
  template: `
    <ul>
      @for (user of users; track user.id) {
        <li>{{ user.name }}</li>
      }

      @empty {
        <li>No users found.</li>
      }
    </ul>
  `,
})
export class UserListComponent {
  users: User[] = [
    { id: 'u1', name: 'Alice', avatar: 'alice.jpg' },
    { id: 'u2', name: 'Bob', avatar: 'bob.jpg' },
  ];
}
```

---

## 43. Outputting Conditional Content

**What is this:** Showing or hiding template content based on a condition with `@if`.

**Description:** The `@if` block (Angular v17+) replaces `*ngIf`. It conditionally renders its content. Pair it with `@else` or `@else if` for branching logic.

**Examples:**

```ts
@Component({
  selector: 'app-status',
  standalone: true,
  template: `
    @if (isLoggedIn) {
      <p>Welcome back, {{ userName }}!</p>
    } @else if (isLoading) {
      <p>Loading...</p>
    } @else {
      <p>Please log in.</p>
    }
  `,
})
export class StatusComponent {
  isLoggedIn = false;
  isLoading = true;
  userName = 'Alice';
}
```

---

## 44. Legacy Angular: Using ngFor & ngIf

**What is this:** The older directive-based syntax for looping and conditionals — still valid but superseded.

**Description:** Before v17, Angular used structural directives `*ngFor` and `*ngIf`. You may encounter these in older codebases. Import `NgFor` and `NgIf` (or `CommonModule`) to use them. Prefer the new `@for` / `@if` syntax in new projects.

**Examples:**

```ts
import { NgFor, NgIf } from '@angular/common';

@Component({
  selector: 'app-legacy',
  standalone: true,
  imports: [NgFor, NgIf],
  template: `
    <!-- Legacy ngIf -->
    <p *ngIf="isLoggedIn; else guestBlock">Welcome!</p>
    <ng-template #guestBlock><p>Please log in.</p></ng-template>

    <!-- Legacy ngFor -->
    <ul>
      <li *ngFor="let user of users; trackBy: trackById">{{ user.name }}</li>
    </ul>
  `,
})
export class LegacyComponent {
  isLoggedIn = true;
  users = [{ id: 'u1', name: 'Alice' }];

  trackById(index: number, user: { id: string }) {
    return user.id;
  }
}
```

---

## 45. Adding More Components to the Demo App

**What is this:** Composing multiple components together to build a more complete application.

**Description:** Real apps are trees of components. Each component is responsible for one slice of the UI. This lesson adds more components to the task manager demo (user list, task list) and wires them into the app root.

**Examples:**

```ts
// app.component.ts
@Component({
  selector: 'app-root',
  standalone: true,
  imports: [HeaderComponent, UserComponent, TasksComponent],
  template: `
    <app-header />
    <main>
      <section id="users">
        @for (user of users; track user.id) {
          <app-user [user]="user" (select)="onSelectUser($event)" />
        }
      </section>
      <section id="tasks">
        <app-tasks [userId]="selectedUserId" />
      </section>
    </main>
  `,
})
export class AppComponent {
  users: User[] = DUMMY_USERS;
  selectedUserId = '';

  onSelectUser(id: string) {
    this.selectedUserId = id;
  }
}
```

---

## 46. Outputting User-specific Tasks

**What is this:** Filtering and displaying tasks that belong to a specific user.

**Description:** The `TasksComponent` receives a `userId` input and filters the global task list to show only that user's tasks. This demonstrates derived data from inputs.

**Examples:**

```ts
@Component({
  selector: 'app-tasks',
  standalone: true,
  imports: [TaskComponent],
  template: `
    @for (task of userTasks; track task.id) {
      <app-task [task]="task" />
    }
  `,
})
export class TasksComponent {
  @Input({ required: true }) userId!: string;

  get userTasks() {
    return DUMMY_TASKS.filter(t => t.userId === this.userId);
  }
}
```

---

## 47. Outputting Task Data in the Task Component

**What is this:** Rendering a single task's data in a dedicated `TaskComponent`.

**Description:** The `TaskComponent` receives a `Task` object as input and renders its details. Keeping display logic in its own component makes each piece independently testable and reusable.

**Examples:**

```ts
@Component({
  selector: 'app-task',
  standalone: true,
  templateUrl: './task.component.html',
  styleUrl: './task.component.css',
})
export class TaskComponent {
  task = input.required<Task>();
}
```

```html
<!-- task.component.html -->
<article>
  <h3>{{ task().title }}</h3>
  <p>Due: {{ task().dueDate }}</p>
  <p>{{ task().summary }}</p>
  <button>Complete</button>
</article>
```

---

## 48. Storing Data Models in Separate Files

**What is this:** Organizing TypeScript interfaces and dummy data into dedicated model files.

**Description:** Keeping interfaces and constants in their own files (`*.model.ts`, `*.data.ts`) keeps component files focused on behavior. Other files import what they need — clean separation of concerns.

**Examples:**

```ts
// task.model.ts
export interface Task {
  id: string;
  userId: string;
  title: string;
  summary: string;
  dueDate: string;
}

// tasks.data.ts
import { Task } from './task.model';

export const DUMMY_TASKS: Task[] = [
  { id: 't1', userId: 'u1', title: 'Buy groceries', summary: '...', dueDate: '2025-12-31' },
  { id: 't2', userId: 'u2', title: 'Fix bug', summary: '...', dueDate: '2025-11-01' },
];
```

---

## 49. Dynamic CSS Styling with Class Bindings

**What is this:** Conditionally applying CSS classes based on component state.

**Description:** Use `[class.className]="condition"` to toggle a single class, or `[ngClass]="{ className: condition }"` for multiple classes. The modern alternative is `[class]="expression"`.

**Examples:**

```ts
@Component({
  selector: 'app-user',
  standalone: true,
  template: `
    <!-- Toggle a single class -->
    <button
      [class.active]="isSelected"
      (click)="onSelect()"
    >
      {{ name() }}
    </button>
  `,
  styles: `
    button { background: transparent; }
    button.active { background: #4a90e2; color: white; }
  `,
})
export class UserComponent {
  name = input.required<string>();
  isSelected = false;

  onSelect() {
    this.isSelected = !this.isSelected;
  }
}
```

---

## 50. More Component Communication: Deleting Tasks

**What is this:** Propagating a "delete" action from a grandchild component up through the component tree.

**Description:** When a deeply nested component needs to affect parent state, it emits an event. The parent listens and mutates its data. This bubbles up one level at a time — Angular does not support event bubbling across component boundaries automatically.

**Examples:**

```ts
// task.component.ts — emits the task id to delete
complete = output<string>();
onComplete() { this.complete.emit(this.task().id); }

// tasks.component.ts — listens and removes the task
onCompleteTask(taskId: string) {
  this.tasks = this.tasks.filter(t => t.id !== taskId);
}
```

```html
<!-- tasks.component.html -->
<app-task
  [task]="task"
  (complete)="onCompleteTask($event)"
/>
```

---

## 51. Creating & Conditionally Rendering Another Component

**What is this:** Adding a "New Task" form component and showing it only when the user clicks a button.

**Description:** A boolean flag on the parent controls whether the form component is rendered. `@if` shows or hides it. The form emits an event when done (submit or cancel), and the parent hides it again.

**Examples:**

```ts
@Component({
  selector: 'app-tasks',
  standalone: true,
  imports: [NewTaskComponent, TaskComponent],
  template: `
    <button (click)="showForm = true">Add Task</button>

    @if (showForm) {
      <app-new-task (cancel)="showForm = false" (add)="onAdd($event)" />
    }

    @for (task of tasks; track task.id) {
      <app-task [task]="task" />
    }
  `,
})
export class TasksComponent {
  showForm = false;
  tasks: Task[] = [];

  onAdd(task: Task) {
    this.tasks.push(task);
    this.showForm = false;
  }
}
```

---

## 52. Managing The "New Task" Dialog

**What is this:** Building the form component that collects new task data.

**Description:** The `NewTaskComponent` manages its own local form state and emits the result upward. It does not directly modify the parent's task list — that is the parent's responsibility.

**Examples:**

```ts
@Component({
  selector: 'app-new-task',
  standalone: true,
  imports: [FormsModule],
  templateUrl: './new-task.component.html',
})
export class NewTaskComponent {
  cancel = output<void>();
  add = output<{ title: string; summary: string; dueDate: string }>();

  title = '';
  summary = '';
  dueDate = '';

  onCancel() { this.cancel.emit(); }

  onSubmit() {
    this.add.emit({ title: this.title, summary: this.summary, dueDate: this.dueDate });
  }
}
```

---

## 53. Using Directives & Two-Way-Binding

**What is this:** Keeping a form input and a component property in sync with `[(ngModel)]`.

**Description:** Two-way binding combines property binding `[ngModel]` and event binding `(ngModelChange)` into the "banana in a box" syntax `[(ngModel)]`. It requires importing `FormsModule`.

**Examples:**

```ts
import { FormsModule } from '@angular/forms';

@Component({
  selector: 'app-new-task',
  standalone: true,
  imports: [FormsModule],
  template: `
    <input type="text" [(ngModel)]="title" placeholder="Task title" />
    <p>Preview: {{ title }}</p>
  `,
})
export class NewTaskComponent {
  title = '';
}
```

---

## 54. Signals & Two-Way-Binding

**What is this:** Using signals with two-way binding via the `model()` function.

**Description:** `model()` creates a signal that supports two-way binding. The parent binds with `[(propertyName)]` and the child reads/writes via the signal — fully reactive, no `FormsModule` required for the signal itself.

**Examples:**

```ts
import { Component, model } from '@angular/core';

@Component({
  selector: 'app-new-task',
  standalone: true,
  template: `
    <input [value]="title()" (input)="title.set($any($event.target).value)" />
    <p>Preview: {{ title() }}</p>
  `,
})
export class NewTaskComponent {
  title = model('');
}
```

```html
<!-- Parent — two-way bind to the signal -->
<app-new-task [(title)]="taskTitle" />
```

---

## 55. Handling Form Submission

**What is this:** Capturing form submit events and preventing the default browser behavior.

**Description:** Bind `(ngSubmit)` on a `<form>` element (when using `FormsModule`) or `(submit)` on a plain form to handle submission in the component. Call `$event.preventDefault()` if not using Angular's form directives.

**Examples:**

```ts
@Component({
  selector: 'app-new-task',
  standalone: true,
  imports: [FormsModule],
  template: `
    <form (ngSubmit)="onSubmit()">
      <input name="title" [(ngModel)]="title" required />
      <input name="dueDate" type="date" [(ngModel)]="dueDate" required />
      <button type="submit">Add</button>
      <button type="button" (click)="onCancel()">Cancel</button>
    </form>
  `,
})
export class NewTaskComponent {
  title = '';
  dueDate = '';
  cancel = output<void>();
  add = output<{ title: string; dueDate: string }>();

  onSubmit() { this.add.emit({ title: this.title, dueDate: this.dueDate }); }
  onCancel() { this.cancel.emit(); }
}
```

---

## 56. Using the Submitted Data

**What is this:** Receiving the emitted form data in the parent and adding it to the task list.

**Description:** The parent listens for the `add` output, creates a new task with a generated id, and pushes it to the tasks array (or updates a signal). The form component is then hidden.

**Examples:**

```ts
onAddTask(data: { title: string; dueDate: string }) {
  this.tasks.push({
    id: `t${Date.now()}`,
    userId: this.userId,
    title: data.title,
    summary: '',
    dueDate: data.dueDate,
  });
  this.showForm = false;
}
```

---

## 57. Content Projection with ng-content

**What is this:** Passing template content into a component from the outside using `<ng-content>`.

**Description:** `<ng-content>` is a slot — it renders whatever the parent places between the component's opening and closing tags. This lets you build wrapper or layout components without knowing the inner content in advance.

**Examples:**

```ts
// card.component.ts — a reusable wrapper
@Component({
  selector: 'app-card',
  standalone: true,
  template: `
    <div class="card">
      <ng-content />
    </div>
  `,
  styles: `.card { border-radius: 8px; padding: 1rem; box-shadow: 0 2px 8px rgba(0,0,0,.1); }`,
})
export class CardComponent {}
```

```html
<!-- Parent — any content goes inside the card -->
<app-card>
  <h2>Task Title</h2>
  <p>Due tomorrow</p>
</app-card>
```

---

## 58. Transforming Template Data with Pipes

**What is this:** Formatting values in templates using built-in Angular pipes.

**Description:** Pipes transform data for display without mutating the underlying value. Apply them with the `|` operator in template expressions. Common built-in pipes: `date`, `uppercase`, `lowercase`, `currency`, `number`, `json`.

**Examples:**

```ts
import { DatePipe, UpperCasePipe, CurrencyPipe } from '@angular/common';

@Component({
  selector: 'app-task',
  standalone: true,
  imports: [DatePipe, UpperCasePipe, CurrencyPipe],
  template: `
    <h3>{{ task().title | uppercase }}</h3>
    <p>Due: {{ task().dueDate | date: 'mediumDate' }}</p>
    <p>Cost: {{ task().cost | currency: 'USD' }}</p>
  `,
})
export class TaskComponent {
  task = input.required<Task & { cost: number }>();
}
```

---

## 59. Getting Started with Services

**What is this:** Extracting shared logic into a service class.

**Description:** Services are plain TypeScript classes decorated with `@Injectable`. They hold logic or data that multiple components need — keeping components lean and logic reusable. A service has no template; it is pure TypeScript.

**Examples:**

```ts
// tasks.service.ts
import { Injectable } from '@angular/core';
import { Task } from './task.model';
import { DUMMY_TASKS } from './tasks.data';

@Injectable({ providedIn: 'root' })
export class TasksService {
  private tasks: Task[] = DUMMY_TASKS;

  getTasksForUser(userId: string): Task[] {
    return this.tasks.filter(t => t.userId === userId);
  }

  addTask(task: Task): void {
    this.tasks.push(task);
  }

  removeTask(taskId: string): void {
    this.tasks = this.tasks.filter(t => t.id !== taskId);
  }
}
```

---

## 60. Getting Started with Dependency Injection

**What is this:** How Angular automatically provides and injects services into components.

**Description:** Angular's DI system reads the constructor parameter types and injects the right service instance. `providedIn: 'root'` means Angular creates a single shared instance for the whole app. Components don't create services — they declare them as dependencies.

**Examples:**

```ts
import { Component, inject } from '@angular/core';
import { TasksService } from './tasks.service';

@Component({
  selector: 'app-tasks',
  standalone: true,
  template: `...`,
})
export class TasksComponent {
  // Modern approach — inject() function
  private tasksService = inject(TasksService);

  // Or constructor injection (both work)
  // constructor(private tasksService: TasksService) {}

  tasks = this.tasksService.getTasksForUser('u1');
}
```

---

## 61. More Service Usage & Alternative Dependency Injection Mechanism

**What is this:** Using a service across multiple components and understanding injection alternatives.

**Description:** Multiple components can inject the same service — they all share the same singleton instance (when `providedIn: 'root'`). You can also provide a service at a component level using the `providers` array, which creates a new instance scoped to that component subtree.

**Examples:**

```ts
// Singleton — shared across the whole app
@Injectable({ providedIn: 'root' })
export class TasksService {}

// Component-scoped — new instance per component
@Component({
  selector: 'app-tasks',
  standalone: true,
  providers: [TasksService],  // new instance, not the global one
  template: `...`,
})
export class TasksComponent {
  private tasksService = inject(TasksService);
}
```

---

## 62. Time to Practice: Services

**What is this:** An exercise to refactor the demo app so all task data is managed by a service.

**Description:** Move the tasks array and all CRUD methods from the component into `TasksService`. Components inject the service and call its methods. This makes data accessible from anywhere without prop-drilling.

**Examples:**

```ts
// Before — data lives in the component (not reusable)
export class TasksComponent {
  tasks: Task[] = DUMMY_TASKS;
  onComplete(id: string) { this.tasks = this.tasks.filter(t => t.id !== id); }
}

// After — data lives in the service (reusable, shareable)
export class TasksComponent {
  private service = inject(TasksService);

  get tasks() { return this.service.getTasksForUser(this.userId); }
  onComplete(id: string) { this.service.removeTask(id); }
}
```

---

## 63. Using localStorage for Data Storage

**What is this:** Persisting app data across page refreshes using the browser's `localStorage` API.

**Description:** `localStorage` stores key-value pairs as strings in the browser. Serialize with `JSON.stringify` and deserialize with `JSON.parse`. In Angular, this belongs in the service so components remain unaware of the storage mechanism.

**Examples:**

```ts
@Injectable({ providedIn: 'root' })
export class TasksService {
  private tasks: Task[] = [];

  constructor() {
    const stored = localStorage.getItem('tasks');
    this.tasks = stored ? (JSON.parse(stored) as Task[]) : DUMMY_TASKS;
  }

  private save() {
    localStorage.setItem('tasks', JSON.stringify(this.tasks));
  }

  addTask(task: Task): void {
    this.tasks.push(task);
    this.save();
  }

  removeTask(taskId: string): void {
    this.tasks = this.tasks.filter(t => t.id !== taskId);
    this.save();
  }

  getTasksForUser(userId: string): Task[] {
    return this.tasks.filter(t => t.userId === userId);
  }
}
```

---

# Section 3: Angular Essentials - Working with Modules

---

## 65. Module Introduction

**What is this:** An overview of what NgModules are and why this section exists alongside the standalone approach.

**Description:** Angular originally organized code into `NgModule` classes. While standalone components are now the default (v17+), many real-world projects and libraries still use modules. This section teaches you to read, work in, and migrate module-based Angular apps.

**Examples:**

```ts
// Two valid ways to build an Angular app:
// 1. Standalone (modern default — no NgModule needed)
// 2. Module-based (legacy, still widely used in existing projects)
```

---

## 66. A First Introduction To Angular Modules (NgModule)

**What is this:** What `NgModule` is and what its decorator properties mean.

**Description:** An `NgModule` is a class decorated with `@NgModule`. It declares which components, directives, and pipes belong to it (`declarations`), which other modules it depends on (`imports`), and which pieces it exposes to other modules (`exports`). Every non-standalone component must belong to exactly one module.

**Examples:**

```ts
import { NgModule } from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
import { AppComponent } from './app.component';

@NgModule({
  declarations: [
    AppComponent,  // components/directives/pipes that belong to this module
  ],
  imports: [
    BrowserModule, // other modules whose exports this module needs
  ],
  exports: [
    AppComponent,  // what this module exposes to other modules
  ],
  bootstrap: [AppComponent], // root component to bootstrap (root module only)
})
export class AppModule {}
```

---

## 67. Angular 19, Standalone Components & Modules

**What is this:** How standalone components and NgModules coexist in Angular v17+.

**Description:** Standalone components (`standalone: true`) don't need a module — they declare their dependencies directly in `imports`. NgModules can import standalone components, and standalone components can import NgModules. Both approaches are fully supported and can be mixed in one project.

**Examples:**

```ts
// Standalone component importing a module
@Component({
  selector: 'app-root',
  standalone: true,
  imports: [SharedModule],  // can import a whole NgModule
  template: `...`,
})
export class AppComponent {}

// NgModule importing a standalone component
@NgModule({
  imports: [
    HeaderComponent,  // standalone component used as an import
  ],
  declarations: [DashboardComponent],
})
export class DashboardModule {}
```

---

## 68. Creating a First Empty Module

**What is this:** Scaffolding a new NgModule file manually and with the CLI.

**Description:** An NgModule is a class with `@NgModule({})` and empty arrays. The CLI can generate one with `ng generate module`. A newly created module is isolated until you import it into another module or the root.

**Examples:**

```bash
# Generate a module with the CLI
ng generate module tasks
# Shorthand
ng g m tasks

# Output:
# CREATE src/app/tasks/tasks.module.ts
```

```ts
// src/app/tasks/tasks.module.ts — minimal empty module
import { NgModule } from '@angular/core';
import { CommonModule } from '@angular/common';

@NgModule({
  declarations: [],
  imports: [CommonModule],
  exports: [],
})
export class TasksModule {}
```

---

## 69. Bootstrapping Apps with Angular Modules

**What is this:** How a module-based Angular app starts up via `main.ts`.

**Description:** Instead of `bootstrapApplication()` (standalone), a module-based app uses `platformBrowserDynamic().bootstrapModule(AppModule)`. The `AppModule`'s `bootstrap` array names the root component Angular renders into `<app-root>`.

**Examples:**

```ts
// main.ts — module-based bootstrap
import { platformBrowserDynamic } from '@angular/platform-browser-dynamic';
import { AppModule } from './app/app.module';

platformBrowserDynamic()
  .bootstrapModule(AppModule)
  .catch(err => console.error(err));
```

```ts
// app.module.ts — root module
import { NgModule } from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
import { AppComponent } from './app.component';

@NgModule({
  declarations: [AppComponent],
  imports: [BrowserModule],
  bootstrap: [AppComponent],
})
export class AppModule {}
```

```ts
// app.component.ts — no standalone: true in module-based apps
import { Component } from '@angular/core';

@Component({
  selector: 'app-root',
  templateUrl: './app.component.html',
})
export class AppComponent {}
```

---

## 70. Declaring & Using Components

**What is this:** How to register a component in a module and use it in another component's template.

**Description:** In a module-based app, a component must be declared in exactly one `NgModule` before any other component in that module can use it in a template. There are no `imports` arrays on the `@Component` decorator — the module handles all the wiring.

**Examples:**

```ts
// header.component.ts — no standalone flag
@Component({
  selector: 'app-header',
  templateUrl: './header.component.html',
})
export class HeaderComponent {}

// app.module.ts — declare it here so AppComponent can use it
@NgModule({
  declarations: [
    AppComponent,
    HeaderComponent,  // registered here
  ],
  imports: [BrowserModule],
  bootstrap: [AppComponent],
})
export class AppModule {}
```

```html
<!-- app.component.html — works because HeaderComponent is declared in the same module -->
<app-header />
<main>...</main>
```

---

## 71. A First Summary

**What is this:** A recap of the key differences between standalone and module-based Angular.

**Description:** At this point you have seen both approaches. The mental model is: standalone components are self-contained (they list their own dependencies), while module-based components delegate dependency management to the module they belong to.

**Examples:**

```ts
// Standalone — component is self-contained
@Component({
  selector: 'app-user',
  standalone: true,
  imports: [DatePipe, RouterLink], // declares its own dependencies
  template: `...`,
})
export class UserComponent {}

// Module-based — module handles dependencies
@Component({
  selector: 'app-user',
  // no standalone, no imports here
  template: `...`,
})
export class UserComponent {}

@NgModule({
  declarations: [UserComponent],
  imports: [CommonModule], // module declares shared dependencies
})
export class UserModule {}
```

---

## 72. Migrating All Components To Use Modules

**What is this:** Converting a standalone-component app to a fully module-based architecture.

**Description:** Migration steps: (1) remove `standalone: true` and `imports` from each `@Component`, (2) add each component to the `declarations` array of the appropriate module, (3) switch `main.ts` from `bootstrapApplication` to `bootstrapModule`.

**Examples:**

```ts
// Before — standalone
@Component({ selector: 'app-task', standalone: true, imports: [DatePipe], template: `...` })
export class TaskComponent {}

// After — module-based
@Component({ selector: 'app-task', template: `...` })
export class TaskComponent {}

// tasks.module.ts
@NgModule({
  declarations: [TaskComponent, TasksComponent],
  imports: [CommonModule],
  exports: [TasksComponent],
})
export class TasksModule {}
```

```ts
// main.ts — switch to bootstrapModule
import { platformBrowserDynamic } from '@angular/platform-browser-dynamic';
import { AppModule } from './app/app.module';

platformBrowserDynamic().bootstrapModule(AppModule);
```

---

## 73. Creating & Using Shared Modules

**What is this:** Grouping commonly used pieces into a `SharedModule` that multiple feature modules can import.

**Description:** If several modules need the same components, directives, or pipes, declare and export them from a `SharedModule`. Feature modules then import `SharedModule` instead of duplicating those declarations. `CommonModule` (which provides `NgIf`, `NgFor`, etc.) is typically re-exported from `SharedModule` as well.

**Examples:**

```ts
// shared/shared.module.ts
import { NgModule } from '@angular/core';
import { CommonModule } from '@angular/common';
import { CardComponent } from './card/card.component';

@NgModule({
  declarations: [CardComponent],
  imports: [CommonModule],
  exports: [
    CommonModule,  // re-export so importers get NgIf, NgFor, etc.
    CardComponent, // shared UI component available to all importers
  ],
})
export class SharedModule {}

// tasks/tasks.module.ts — just import SharedModule
@NgModule({
  declarations: [TasksComponent, TaskComponent],
  imports: [SharedModule],
})
export class TasksModule {}
```

---

## 74. Creating More Complex Module-based App Structures

**What is this:** Organizing a larger app into feature modules, each owning its own components and routing.

**Description:** As an app grows, split it into feature modules (e.g. `UsersModule`, `TasksModule`). Each module declares its own components and exports what the root or other modules need. The root `AppModule` imports only the feature modules — not individual components.

**Examples:**

```ts
// users/users.module.ts
@NgModule({
  declarations: [UsersComponent, UserComponent],
  imports: [SharedModule],
  exports: [UsersComponent],
})
export class UsersModule {}

// tasks/tasks.module.ts
@NgModule({
  declarations: [TasksComponent, TaskComponent, NewTaskComponent],
  imports: [SharedModule, FormsModule],
  exports: [TasksComponent],
})
export class TasksModule {}

// app.module.ts — clean root: imports feature modules, not individual components
@NgModule({
  declarations: [AppComponent],
  imports: [
    BrowserModule,
    UsersModule,
    TasksModule,
  ],
  bootstrap: [AppComponent],
})
export class AppModule {}
```

```
// Resulting folder structure
src/app/
├── shared/
│   ├── shared.module.ts
│   └── card/card.component.ts
├── users/
│   ├── users.module.ts
│   ├── users.component.ts
│   └── user/user.component.ts
├── tasks/
│   ├── tasks.module.ts
│   ├── tasks.component.ts
│   ├── task/task.component.ts
│   └── new-task/new-task.component.ts
├── app.module.ts
└── app.component.ts
```

---

# Section 4: Angular Essentials - Time To Practice

> This section builds an **Investment Calculator** app end-to-end, applying everything from Sections 1–3. Each lesson adds one piece to the app.

---

## 75. Module Introduction & Starting Project

**What is this:** Introduction to the practice project — an investment calculator that computes annual growth from user inputs.

**Description:** The app takes four inputs (initial investment, annual investment, expected return rate, investment duration) and outputs a year-by-year breakdown of the investment value, interest, and total invested. The section walks through building it from a blank `ng new` project.

**Examples:**

```bash
ng new investment-calculator --standalone
cd investment-calculator
ng serve
```

```
src/app/
├── header/
├── user-input/
├── investment-results/
├── app.component.ts
└── app.config.ts
```

---

## 76. Exercise Hints

**What is this:** Guidance on how to approach the exercise before watching the solution.

**Description:** Before watching each solution video, try to implement the feature yourself. The hints remind you which Angular concepts to use for each step — components, two-way binding, outputs, inputs, services, signals.

**Examples:**

```ts
// Hints checklist for the investment calculator:
// 1. Header   → standalone component, image + title
// 2. Input    → two-way binding with signals or [(ngModel)], form submission
// 3. Results  → receives data via @Input / input(), renders a table
// 4. Logic    → calculation function (pure TS, no Angular needed)
// 5. Wiring   → parent passes data down, child emits data up
// 6. Pipe     → format currency values with the built-in CurrencyPipe
// 7. Service  → lift state out of components for clean communication
```

---

## 77. Adding a Header Component With An Image

**What is this:** Creating and styling the app's header as a standalone component.

**Description:** A simple presentational component — no inputs, no outputs. Demonstrates the minimal component setup: `@Component` decorator, external template, scoped CSS, and registering it in `AppComponent`'s `imports`.

**Examples:**

```ts
// header/header.component.ts
import { Component } from '@angular/core';

@Component({
  selector: 'app-header',
  standalone: true,
  templateUrl: './header.component.html',
  styleUrl: './header.component.css',
})
export class HeaderComponent {}
```

```html
<!-- header/header.component.html -->
<header>
  <img src="investment-icon.png" alt="Investment calculator icon" />
  <h1>Investment Calculator</h1>
</header>
```

```css
/* header/header.component.css */
header {
  display: flex;
  align-items: center;
  gap: 1rem;
  padding: 1.5rem;
  background: #1a1a2e;
  color: #fff;
}

img { width: 48px; }
```

```ts
// app.component.ts
import { Component } from '@angular/core';
import { HeaderComponent } from './header/header.component';

@Component({
  selector: 'app-root',
  standalone: true,
  imports: [HeaderComponent],
  template: `
    <app-header />
    <main>...</main>
  `,
})
export class AppComponent {}
```

---

## 78. Adding a User Input Component

**What is this:** Building the form component that collects the four investment parameters.

**Description:** The `UserInputComponent` owns the form fields. Each field maps to a local property. The component is responsible only for collecting input — calculation happens elsewhere.

**Examples:**

```ts
// user-input/user-input.component.ts
import { Component } from '@angular/core';
import { FormsModule } from '@angular/forms';

@Component({
  selector: 'app-user-input',
  standalone: true,
  imports: [FormsModule],
  templateUrl: './user-input.component.html',
  styleUrl: './user-input.component.css',
})
export class UserInputComponent {
  initialInvestment = 1000;
  annualInvestment = 500;
  expectedReturn = 5;
  duration = 10;
}
```

```html
<!-- user-input/user-input.component.html -->
<section>
  <div>
    <label for="initial">Initial Investment</label>
    <input id="initial" type="number" [(ngModel)]="initialInvestment" />
  </div>
  <div>
    <label for="annual">Annual Investment</label>
    <input id="annual" type="number" [(ngModel)]="annualInvestment" />
  </div>
  <div>
    <label for="return">Expected Return (%)</label>
    <input id="return" type="number" [(ngModel)]="expectedReturn" />
  </div>
  <div>
    <label for="duration">Duration (years)</label>
    <input id="duration" type="number" [(ngModel)]="duration" />
  </div>
  <button type="button">Calculate</button>
</section>
```

---

## 79. Handling Form Submission

**What is this:** Wiring the Calculate button to a method that reads the form values.

**Description:** A `(click)` or `(submit)` binding calls `onSubmit()`. The method reads the current field values and — for now — logs them. In the next lessons this data gets passed up to the parent.

**Examples:**

```ts
export class UserInputComponent {
  initialInvestment = 1000;
  annualInvestment = 500;
  expectedReturn = 5;
  duration = 10;

  onSubmit() {
    console.log({
      initialInvestment: this.initialInvestment,
      annualInvestment: this.annualInvestment,
      expectedReturn: this.expectedReturn,
      duration: this.duration,
    });
  }
}
```

```html
<button type="button" (click)="onSubmit()">Calculate</button>
```

---

## 80. Extracting Values with Two-Way-Binding

**What is this:** Using `[(ngModel)]` to keep form fields and component properties in sync automatically.

**Description:** Two-way binding means the component property updates whenever the user types (no manual event handling needed), and the input field reflects any programmatic change to the property. Requires `FormsModule` in `imports`.

**Examples:**

```ts
import { FormsModule } from '@angular/forms';

@Component({
  standalone: true,
  imports: [FormsModule],
  template: `
    <input type="number" [(ngModel)]="duration" />
    <p>You entered: {{ duration }} years</p>
  `,
})
export class UserInputComponent {
  duration = 10;

  // duration updates automatically as the user types
  // No (input) handler needed
}
```

---

## 81. Calculating the Annual Investment Data

**What is this:** Writing the pure TypeScript function that computes year-by-year investment results.

**Description:** The calculation logic is plain TypeScript — no Angular APIs involved. Keeping it in a separate utility or service makes it easy to test and reuse. The function returns an array of annual result objects.

**Examples:**

```ts
// investment-calculator.util.ts
export interface InvestmentResult {
  year: number;
  interest: number;
  valueEndOfYear: number;
  annualInvestment: number;
  totalInterest: number;
  totalAmountInvested: number;
}

export function calculateInvestmentResults(
  initialInvestment: number,
  annualInvestment: number,
  expectedReturn: number,
  duration: number,
): InvestmentResult[] {
  const results: InvestmentResult[] = [];
  let investmentValue = initialInvestment;

  for (let i = 0; i < duration; i++) {
    const year = i + 1;
    const interestEarnedInYear = investmentValue * (expectedReturn / 100);
    investmentValue += interestEarnedInYear + annualInvestment;
    const totalAmountInvested = initialInvestment + annualInvestment * year;

    results.push({
      year,
      interest: interestEarnedInYear,
      valueEndOfYear: investmentValue,
      annualInvestment,
      totalInterest: investmentValue - totalAmountInvested,
      totalAmountInvested,
    });
  }

  return results;
}
```

---

## 82. Cross-Component Communication with Outputs

**What is this:** Emitting the collected form data from `UserInputComponent` up to `AppComponent`.

**Description:** `UserInputComponent` emits an `InvestmentData` object when the user submits. `AppComponent` receives it, runs the calculation, and passes the results down to `InvestmentResultsComponent`.

**Examples:**

```ts
// user-input/user-input.component.ts
import { Component, output } from '@angular/core';

export interface InvestmentData {
  initialInvestment: number;
  annualInvestment: number;
  expectedReturn: number;
  duration: number;
}

@Component({ selector: 'app-user-input', standalone: true, imports: [FormsModule], templateUrl: '...' })
export class UserInputComponent {
  calculate = output<InvestmentData>();

  initialInvestment = 1000;
  annualInvestment = 500;
  expectedReturn = 5;
  duration = 10;

  onSubmit() {
    this.calculate.emit({
      initialInvestment: this.initialInvestment,
      annualInvestment: this.annualInvestment,
      expectedReturn: this.expectedReturn,
      duration: this.duration,
    });
  }
}
```

```html
<!-- app.component.html -->
<app-user-input (calculate)="onCalculate($event)" />
```

---

## 83. Creating & Using a Data Model

**What is this:** Defining TypeScript interfaces for the app's data shapes in dedicated model files.

**Description:** Centralizing type definitions in model files means every component and function that touches that data shares the same contract. Changes to the model propagate everywhere TypeScript catches mismatches.

**Examples:**

```ts
// models/investment-input.model.ts
export interface InvestmentInput {
  initialInvestment: number;
  annualInvestment: number;
  expectedReturn: number;
  duration: number;
}

// models/investment-result.model.ts
export interface InvestmentResult {
  year: number;
  interest: number;
  valueEndOfYear: number;
  annualInvestment: number;
  totalInterest: number;
  totalAmountInvested: number;
}
```

```ts
// All components and utilities import from the same source
import { InvestmentInput } from '../models/investment-input.model';
import { InvestmentResult } from '../models/investment-result.model';
```

---

## 84. Passing Data from Parent to Child with Inputs

**What is this:** Sending the calculated results array from `AppComponent` down to `InvestmentResultsComponent`.

**Description:** `AppComponent` holds the computed `InvestmentResult[]` and passes it to the results component via an `input()`. The results component renders the table — it has no calculation logic of its own.

**Examples:**

```ts
// app.component.ts
import { Component } from '@angular/core';
import { InvestmentResult, calculateInvestmentResults } from './investment-calculator.util';

@Component({
  selector: 'app-root',
  standalone: true,
  imports: [HeaderComponent, UserInputComponent, InvestmentResultsComponent],
  template: `
    <app-header />
    <app-user-input (calculate)="onCalculate($event)" />
    <app-investment-results [results]="results" />
  `,
})
export class AppComponent {
  results: InvestmentResult[] = [];

  onCalculate(data: InvestmentInput) {
    this.results = calculateInvestmentResults(
      data.initialInvestment,
      data.annualInvestment,
      data.expectedReturn,
      data.duration,
    );
  }
}
```

```ts
// investment-results/investment-results.component.ts
import { Component, input } from '@angular/core';
import { InvestmentResult } from '../models/investment-result.model';

@Component({
  selector: 'app-investment-results',
  standalone: true,
  templateUrl: './investment-results.component.html',
})
export class InvestmentResultsComponent {
  results = input.required<InvestmentResult[]>();
}
```

---

## 85. Outputting Data in a Table

**What is this:** Rendering the results array as an HTML table using `@for`.

**Description:** Each row represents one year. `@for` iterates over the results signal, and each column displays the corresponding property. The `@empty` block shows a placeholder before the user calculates.

**Examples:**

```html
<!-- investment-results/investment-results.component.html -->
<table>
  <thead>
    <tr>
      <th>Year</th>
      <th>Investment Value</th>
      <th>Interest (Year)</th>
      <th>Total Interest</th>
      <th>Total Invested</th>
    </tr>
  </thead>
  <tbody>
    @for (result of results(); track result.year) {
      <tr>
        <td>{{ result.year }}</td>
        <td>{{ result.valueEndOfYear }}</td>
        <td>{{ result.interest }}</td>
        <td>{{ result.totalInterest }}</td>
        <td>{{ result.totalAmountInvested }}</td>
      </tr>
    }
    @empty {
      <tr>
        <td colspan="5">No data yet — enter values and calculate.</td>
      </tr>
    }
  </tbody>
</table>
```

---

## 86. Formatting Output with a Pipe

**What is this:** Applying the built-in `CurrencyPipe` to format monetary values in the table.

**Description:** Raw numbers like `15234.5678` are hard to read. The `currency` pipe formats them as `$15,234.57`. Import `CurrencyPipe` from `@angular/common` and add it to the component's `imports`.

**Examples:**

```ts
import { CurrencyPipe } from '@angular/common';

@Component({
  selector: 'app-investment-results',
  standalone: true,
  imports: [CurrencyPipe],
  templateUrl: './investment-results.component.html',
})
export class InvestmentResultsComponent {
  results = input.required<InvestmentResult[]>();
}
```

```html
<!-- Before -->
<td>{{ result.valueEndOfYear }}</td>

<!-- After — formatted as currency -->
<td>{{ result.valueEndOfYear | currency }}</td>
<td>{{ result.interest | currency: 'USD' : 'symbol' : '1.2-2' }}</td>
```

---

## 87. Using Signals & Resetting The Form After Submission

**What is this:** Replacing plain properties with signals in the input component and adding a reset.

**Description:** Convert `UserInputComponent`'s fields to `signal()`. This makes values reactive. After emitting the calculate event, call `.set()` on each signal to reset the form back to defaults.

**Examples:**

```ts
import { Component, signal, output } from '@angular/core';

@Component({
  selector: 'app-user-input',
  standalone: true,
  imports: [FormsModule],
  templateUrl: './user-input.component.html',
})
export class UserInputComponent {
  initialInvestment = signal(1000);
  annualInvestment = signal(500);
  expectedReturn = signal(5);
  duration = signal(10);

  calculate = output<InvestmentInput>();

  onSubmit() {
    this.calculate.emit({
      initialInvestment: this.initialInvestment(),
      annualInvestment: this.annualInvestment(),
      expectedReturn: this.expectedReturn(),
      duration: this.duration(),
    });

    // Reset form after submission
    this.initialInvestment.set(1000);
    this.annualInvestment.set(500);
    this.expectedReturn.set(5);
    this.duration.set(10);
  }
}
```

```html
<!-- Bind signals with two-way binding using [value] + (input) -->
<input
  type="number"
  [value]="initialInvestment()"
  (input)="initialInvestment.set(+$any($event.target).value)"
/>
```

---

## 88. Using a Service for Cross-Component Communication

**What is this:** Moving the results state into a service so components communicate through it instead of through the parent.

**Description:** Instead of `AppComponent` holding the results array and passing it down, an `InvestmentService` holds the data. `UserInputComponent` calls the service to trigger calculation; `InvestmentResultsComponent` reads results from the service. The parent becomes a thin shell.

**Examples:**

```ts
// investment.service.ts
import { Injectable } from '@angular/core';
import { InvestmentInput } from './models/investment-input.model';
import { InvestmentResult, calculateInvestmentResults } from './investment-calculator.util';

@Injectable({ providedIn: 'root' })
export class InvestmentService {
  results: InvestmentResult[] = [];

  calculate(data: InvestmentInput) {
    this.results = calculateInvestmentResults(
      data.initialInvestment,
      data.annualInvestment,
      data.expectedReturn,
      data.duration,
    );
  }
}
```

```ts
// user-input.component.ts — calls the service directly
export class UserInputComponent {
  private investmentService = inject(InvestmentService);

  onSubmit() {
    this.investmentService.calculate({ ... });
  }
}

// investment-results.component.ts — reads from the service
export class InvestmentResultsComponent {
  private investmentService = inject(InvestmentService);

  get results() {
    return this.investmentService.results;
  }
}
```

---

## 89. Using Signals in Services

**What is this:** Replacing the plain array in `InvestmentService` with a `signal` for automatic reactivity.

**Description:** When `results` is a signal, any template that reads `results()` automatically re-renders when the signal changes — no manual change detection or `@Input` updates required. This is the recommended pattern for shared state in modern Angular.

**Examples:**

```ts
import { Injectable, signal } from '@angular/core';

@Injectable({ providedIn: 'root' })
export class InvestmentService {
  // Private writable signal
  private _results = signal<InvestmentResult[]>([]);

  // Public read-only view
  readonly results = this._results.asReadonly();

  calculate(data: InvestmentInput) {
    this._results.set(
      calculateInvestmentResults(
        data.initialInvestment,
        data.annualInvestment,
        data.expectedReturn,
        data.duration,
      ),
    );
  }
}
```

```ts
// investment-results.component.ts — reads the signal directly
export class InvestmentResultsComponent {
  private investmentService = inject(InvestmentService);
  results = this.investmentService.results; // already a readonly signal
}
```

```html
<!-- template calls the signal like a function -->
@for (result of results(); track result.year) {
  <tr>...</tr>
}
```

---

## 90. Migrating to Angular Modules

**What is this:** Converting the standalone investment calculator app to use NgModules.

**Description:** A practical exercise in the migration path: remove `standalone: true` and component-level `imports`, add every component to a module's `declarations`, switch `main.ts` to `bootstrapModule`, and ensure `FormsModule` and `CommonModule` are imported at the module level.

**Examples:**

```ts
// app.module.ts
import { NgModule } from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
import { FormsModule } from '@angular/forms';

import { AppComponent } from './app.component';
import { HeaderComponent } from './header/header.component';
import { UserInputComponent } from './user-input/user-input.component';
import { InvestmentResultsComponent } from './investment-results/investment-results.component';

@NgModule({
  declarations: [
    AppComponent,
    HeaderComponent,
    UserInputComponent,
    InvestmentResultsComponent,
  ],
  imports: [
    BrowserModule,
    FormsModule,   // needed for [(ngModel)]
  ],
  bootstrap: [AppComponent],
})
export class AppModule {}
```

```ts
// main.ts — switch from bootstrapApplication to bootstrapModule
import { platformBrowserDynamic } from '@angular/platform-browser-dynamic';
import { AppModule } from './app/app.module';

platformBrowserDynamic().bootstrapModule(AppModule);
```

```ts
// Each component — remove standalone: true and imports: []
@Component({
  selector: 'app-user-input',
  // standalone: true  ← removed
  // imports: [...]    ← removed
  templateUrl: './user-input.component.html',
})
export class UserInputComponent { ... }
```

---

# Section 5: Debugging Angular Apps

---

## 92. Module Introduction

**What is this:** An overview of the debugging tools and techniques available for Angular apps.

**Description:** Bugs fall into two categories: compile-time errors (TypeScript catches these before the app runs) and logical errors (the app runs but produces wrong results). This section covers reading Angular's error messages, using browser DevTools breakpoints, and the Angular-specific DevTools browser extension.

**Examples:**

```ts
// Two categories of bugs in Angular:

// 1. Compile-time — TypeScript catches these immediately
@Component({ ... })
export class UserComponent {
  name = input.required<string>();
}
// Error: Property 'name' does not exist  ← IDE highlights before you even run

// 2. Logical — app runs but output is wrong
calculateTotal() {
  return this.price * this.quantity; // no TS error, but wrong if quantity is a string
}
```

---

## 93. Understanding Error Messages & Fixing Errors

**What is this:** How to read Angular's console errors and template compilation errors to find the root cause.

**Description:** Angular errors usually tell you the component, the file, and the line number. Template errors appear in the browser console with a stack trace pointing to the component class. Reading the full message — not just the first line — almost always reveals the fix.

**Examples:**

```ts
// Common error: missing import in standalone component
// Console: "Can't bind to 'ngModel' since it isn't a known property of 'input'"
// Fix: add FormsModule to imports

@Component({
  standalone: true,
  imports: [FormsModule], // ← was missing
  template: `<input [(ngModel)]="name" />`,
})
export class UserInputComponent {
  name = '';
}
```

```ts
// Common error: wrong selector
// Console: "'app-headr' is not a known element" (typo)
// Fix: match the selector exactly

@Component({ selector: 'app-header', ... }) // selector is 'app-header'
// template used 'app-headr' ← typo
```

```ts
// Common error: required input not passed
// Console: "Required input 'name' from component UserComponent must be specified"
// Fix: provide the input in the parent template

// Wrong
<app-user />

// Correct
<app-user [name]="selectedUser.name" />
```

---

## 94. Debugging Logical Errors with the Browser DevTools & Breakpoints

**What is this:** Using Chrome/Firefox DevTools to pause execution and inspect values at runtime.

**Description:** When the app runs without errors but produces wrong output, set a breakpoint in the Sources panel. Angular source maps let you break directly in your TypeScript files. You can inspect variables, step through code line by line, and watch expressions change in real time.

**Examples:**

```ts
// Option 1: debugger statement — pauses execution here in DevTools
calculateTotal() {
  debugger; // browser pauses here, you can inspect all local variables
  return this.price * this.quantity;
}

// Option 2: set a breakpoint in DevTools
// Chrome → F12 → Sources → src/app/investment-calculator.util.ts
// Click the line number to set a breakpoint
// Reload or trigger the action — execution pauses at that line
```

```ts
// Option 3: console.log for quick checks (remove before committing)
onCalculate(data: InvestmentInput) {
  console.log('Input received:', data);
  const results = calculateInvestmentResults(...);
  console.log('Results:', results);
  this.results = results;
}
```

```
// DevTools workflow for a logical bug:
// 1. Open DevTools (F12) → Sources tab
// 2. Ctrl+P → type the .ts filename to open it
// 3. Click the gutter (line number) to set a breakpoint
// 4. Trigger the action in the UI
// 5. Execution pauses → inspect variables in the Scope panel
// 6. Step over (F10), step into (F11) to trace the flow
```

---

## 95. Exploring the Angular DevTools

**What is this:** Using the Angular DevTools browser extension to inspect the component tree, inputs, and signals at runtime.

**Description:** Angular DevTools is an official Chrome/Edge extension that adds an "Angular" panel to DevTools. It shows the live component tree, lets you inspect and edit component inputs and state, and visualizes signal values — invaluable for understanding data flow without adding `console.log` calls.

**Examples:**

```bash
# Install Angular DevTools
# Chrome Web Store → search "Angular DevTools" → Add to Chrome
# Works with any Angular app running in development mode (ng serve)
```

```
// What Angular DevTools shows:

// Components panel:
// AppComponent
// ├── HeaderComponent
// ├── UserInputComponent
// │     initialInvestment: signal(1000)
// │     annualInvestment:  signal(500)
// └── InvestmentResultsComponent
//       results: signal([...])

// Click any component to:
// - See its current input values
// - See its signal values live
// - Edit values directly to test different states
// - Highlight the component in the DOM
```

```ts
// Tip: DevTools only works in development mode
// ng serve          ← DevTools works here
// ng build          ← production build, DevTools disabled (by design)

// If DevTools shows "Angular not detected":
// Make sure you are running ng serve, not opening index.html directly
```

---

# Section 6: Components & Templates - Deep Dive

> Lessons marked "Repetition" in the course (101, 102, 119, 128, 140, 141, 147) are skipped — they recap earlier material without introducing new concepts.

---

## 96. Module Introduction

**What is this:** Overview of what this deep-dive section covers.

**Description:** This section goes beyond the basics — component architecture decisions, content projection, host elements, view encapsulation, lifecycle hooks, template variables, ViewChild, signals effects, and custom two-way binding. These are the tools that separate beginner Angular from production-quality Angular.

---

## 97. Starting Project & An Opportunity For Smaller Components?

**What is this:** Reviewing a starting project and identifying where to split large components.

**Description:** A common smell in Angular is a component that does too much — large template, many properties, mixed responsibilities. The first step is identifying natural split points: repeated UI blocks, logically distinct sections, or reusable pieces.

**Examples:**

```ts
// Smell — one component handling everything
@Component({ selector: 'app-dashboard', template: `
  <!-- user card -->
  <!-- task list -->
  <!-- stats chart -->
  <!-- filter controls -->
` })
export class DashboardComponent { /* 200+ lines */ }

// Better — each concern is its own component
@Component({ selector: 'app-dashboard', template: `
  <app-user-card [user]="user" />
  <app-task-list [tasks]="tasks" />
  <app-stats [data]="stats" />
  <app-filters (change)="onFilterChange($event)" />
` })
export class DashboardComponent { }
```

---

## 98. When & How To Split Up Components

**What is this:** Decision rules for when splitting a component adds value vs. adds noise.

**Description:** Split when: (1) a UI block is reused in multiple places, (2) a section has its own distinct state or logic, (3) the template exceeds ~50 lines and reads poorly. Don't split just to be tidy — a small component with one `<p>` and no logic is usually not worth the overhead.

**Examples:**

```ts
// Good split — reused in multiple places
@Component({ selector: 'app-avatar', standalone: true,
  template: `<img [src]="src()" [alt]="name()" class="avatar" />` })
export class AvatarComponent {
  src = input.required<string>();
  name = input.required<string>();
}

// Bad split — wraps a single element with no added value
@Component({ selector: 'app-title', standalone: true,
  template: `<h1>My App</h1>` }) // just use <h1> directly
export class TitleComponent {}
```

---

## 99. Splitting A Component Into Multiple Components

**What is this:** Hands-on refactoring — extracting a piece of a large template into its own component.

**Description:** The mechanics: (1) create the new component, (2) move the HTML slice into its template, (3) identify what data it needs and add `input()` for each, (4) identify what actions it triggers and add `output()` for each, (5) replace the original HTML slice with the new selector.

**Examples:**

```ts
// Before — task row inline in TasksComponent
// <li>{{ task.title }} <button (click)="remove(task.id)">X</button></li>

// After — extracted into TaskItemComponent
@Component({
  selector: 'app-task-item',
  standalone: true,
  template: `
    <li>
      {{ task().title }}
      <button (click)="remove.emit(task().id)">X</button>
    </li>
  `,
})
export class TaskItemComponent {
  task = input.required<Task>();
  remove = output<string>();
}

// TasksComponent template — cleaner
@for (task of tasks(); track task.id) {
  <app-task-item [task]="task" (remove)="onRemove($event)" />
}
```

---

## 100. Creating Reusable Components

**What is this:** Designing a component generic enough to be used in multiple contexts.

**Description:** A reusable component takes inputs for everything that varies and emits outputs for everything it triggers. It owns no external state. The classic example is a `CardComponent` that wraps any content, or a `ButtonComponent` that accepts a label and variant.

**Examples:**

```ts
@Component({
  selector: 'app-button',
  standalone: true,
  template: `
    <button [class]="variant()" (click)="clicked.emit()">
      {{ label() }}
    </button>
  `,
  styles: `
    .primary { background: #4a90e2; color: white; }
    .danger  { background: #e24a4a; color: white; }
  `,
})
export class ButtonComponent {
  label = input.required<string>();
  variant = input<'primary' | 'danger'>('primary');
  clicked = output<void>();
}
```

```html
<!-- Used anywhere -->
<app-button label="Save" variant="primary" (clicked)="onSave()" />
<app-button label="Delete" variant="danger" (clicked)="onDelete()" />
```

---

## 103. Using Content Projection & ng-content

**What is this:** Projecting arbitrary template content into a component via `<ng-content>`.

**Description:** `<ng-content>` acts as a slot — the parent writes content between the component's tags and Angular renders it inside the slot. The component does not know or care what the content is.

**Examples:**

```ts
@Component({
  selector: 'app-card',
  standalone: true,
  template: `
    <div class="card">
      <ng-content />
    </div>
  `,
})
export class CardComponent {}
```

```html
<!-- Parent passes any content -->
<app-card>
  <h2>Task: Fix bug</h2>
  <p>Due: tomorrow</p>
  <app-button label="Done" (clicked)="onDone()" />
</app-card>
```

---

## 104. Adding Forms to Components

**What is this:** Embedding a form inside a wrapper component and projecting or handling submission.

**Description:** Forms can live inside container components. The form element and its submission logic belong in the component that owns the data — wrapper components stay layout-only.

**Examples:**

```ts
@Component({
  selector: 'app-auth-card',
  standalone: true,
  imports: [FormsModule],
  template: `
    <app-card>
      <form (ngSubmit)="onSubmit()">
        <input name="email" [(ngModel)]="email" type="email" />
        <button type="submit">Login</button>
      </form>
    </app-card>
  `,
})
export class AuthCardComponent {
  email = '';
  onSubmit() { console.log(this.email); }
}
```

---

## 105. A Possible, But Not Ideal Way Of Extending Built-in Elements

**What is this:** Wrapping a native element (e.g. `<button>`) in a custom component — and why this causes issues.

**Description:** Wrapping `<button>` in `<app-button>` introduces a host `<app-button>` element in the DOM, breaking native button behaviors like `type`, `form` association, and accessibility. This is why attribute selectors are a better fit for extending native elements.

**Examples:**

```ts
// Problem — wrapping <button> adds an extra DOM element
@Component({
  selector: 'app-button',
  template: `<button><ng-content /></button>`,
})
export class ButtonComponent {}

// In the DOM this becomes:
// <app-button>        ← extra element, breaks form/a11y semantics
//   <button>Click</button>
// </app-button>

// Clicking the outer element does not activate the inner button in all browsers
```

---

## 106. Extending Built-in Elements with Custom Components via Attribute Selectors

**What is this:** Using an attribute selector so the component IS the native element, not a wrapper around it.

**Description:** Instead of `selector: 'app-button'`, use `selector: 'button[appButton]'`. Angular applies the component directly to the native `<button>` element — no extra DOM node. All native button behaviors are preserved.

**Examples:**

```ts
@Component({
  selector: 'button[appButton]', // applies TO a <button>, not around it
  standalone: true,
  template: `<ng-content />`,
  styles: `:host { background: #4a90e2; color: white; padding: .5rem 1rem; border: none; border-radius: 4px; cursor: pointer; }`,
})
export class ButtonComponent {}
```

```html
<!-- Usage — just a real <button> with an attribute -->
<button appButton type="submit">Save</button>
<button appButton type="button" (click)="onCancel()">Cancel</button>

<!-- DOM output — no wrapper element -->
<!-- <button appButton ...>Save</button> -->
```

---

## 107. Supporting Content Projection with Multiple Slots

**What is this:** Using named `<ng-content select="">` slots to project content into specific locations.

**Description:** A single `<ng-content>` catches everything. Named slots let you project different pieces of content into different positions in the template using CSS selectors.

**Examples:**

```ts
@Component({
  selector: 'app-dialog',
  standalone: true,
  template: `
    <div class="dialog">
      <header>
        <ng-content select="[slot=title]" />
      </header>
      <main>
        <ng-content />
      </main>
      <footer>
        <ng-content select="[slot=actions]" />
      </footer>
    </div>
  `,
})
export class DialogComponent {}
```

```html
<app-dialog>
  <h2 slot="title">Confirm Delete</h2>

  <p>Are you sure? This cannot be undone.</p>

  <div slot="actions">
    <button appButton (click)="onConfirm()">Delete</button>
    <button (click)="onCancel()">Cancel</button>
  </div>
</app-dialog>
```

---

## 108. Exploring Advanced Content Projection

**What is this:** Using `ngProjectAs` to control how projected content is matched by named slots.

**Description:** When a slot selector targets an element type or attribute but you need to wrap content in an `<ng-container>`, use `ngProjectAs` to tell Angular to treat the container as if it were the target element.

**Examples:**

```html
<!-- Without ngProjectAs — ng-container breaks the slot selector -->
<app-dialog>
  <ng-container slot="title">
    <h2>Title</h2>  <!-- may not match [slot=title] as expected -->
  </ng-container>
</app-dialog>

<!-- With ngProjectAs — ng-container masquerades as the selector -->
<app-dialog>
  <ng-container ngProjectAs="[slot=title]">
    <h2>Title</h2>
  </ng-container>
</app-dialog>
```

---

## 109. Defining Content Projection Fallbacks

**What is this:** Providing default content inside `<ng-content>` that renders when the parent projects nothing.

**Description:** Place fallback content between the `<ng-content>` opening and closing tags. Angular renders it only when no projected content is provided for that slot.

**Examples:**

```ts
@Component({
  selector: 'app-card',
  standalone: true,
  template: `
    <div class="card">
      <header>
        <ng-content select="[slot=title]">
          <span>Untitled</span>  <!-- fallback if no title is projected -->
        </ng-content>
      </header>
      <ng-content>
        <p>No content provided.</p>  <!-- fallback for default slot -->
      </ng-content>
    </div>
  `,
})
export class CardComponent {}
```

---

## 110. Multi-Element Custom Components & Content Projection

**What is this:** Building components whose template has multiple top-level elements alongside projected content.

**Description:** A component's template can have any structure — multiple sibling elements, projected slots interspersed with static markup. This is common in layout components like tabs, accordions, and step wizards.

**Examples:**

```ts
@Component({
  selector: 'app-section',
  standalone: true,
  template: `
    <section>
      <div class="section-icon">
        <ng-content select="[slot=icon]" />
      </div>
      <div class="section-body">
        <h3><ng-content select="[slot=heading]" /></h3>
        <div class="section-content">
          <ng-content />
        </div>
      </div>
    </section>
  `,
})
export class SectionComponent {}
```

---

## 111. Scoping CSS Styles to Components

**What is this:** How Angular isolates component styles so they don't affect the rest of the app.

**Description:** Styles in `styleUrl` only apply to the component's own template. Angular adds a unique attribute (e.g. `_ngcontent-abc`) to every element in the template and scopes each CSS rule to that attribute. This is View Encapsulation — on by default.

**Examples:**

```css
/* card.component.css — only affects CardComponent's template */
h2 { color: navy; }
/* Compiled to: h2[_ngcontent-xyz] { color: navy; } */
/* Does NOT affect <h2> in any other component */
```

```ts
// To write styles that DO escape the component (use sparingly):
@Component({
  styles: `
    :host { display: block; }           /* styles the host element itself */
    :host(.active) { border: 2px solid blue; }  /* conditional host styling */
  `,
})
export class CardComponent {}
```

---

## 112. Understanding & Configuring View Encapsulation

**What is this:** The three View Encapsulation modes and when to change the default.

**Description:** `Emulated` (default) — Angular adds scoping attributes. `None` — styles are global (no scoping). `ShadowDom` — uses the browser's native Shadow DOM. Change only when you have a specific reason (e.g. a global theme component or a web component).

**Examples:**

```ts
import { Component, ViewEncapsulation } from '@angular/core';

@Component({
  selector: 'app-theme',
  standalone: true,
  encapsulation: ViewEncapsulation.None, // styles leak globally — use with care
  styles: `body { font-family: 'Inter', sans-serif; }`,
  template: `<ng-content />`,
})
export class ThemeComponent {}

// ShadowDom — true browser isolation (styles can't leak in OR out)
@Component({
  encapsulation: ViewEncapsulation.ShadowDom,
  ...
})
export class IsolatedWidget {}
```

---

## 113. Making Sense of Component Host Elements

**What is this:** What the "host element" is and why it matters for styling and DOM structure.

**Description:** Every component has a host element — the DOM node that matches its selector (e.g. `<app-card>`). The host element wraps the component's template in the DOM. By default it is an unstyled inline element. You control it with `:host` in CSS or `host` in the decorator.

**Examples:**

```ts
@Component({
  selector: 'app-card',
  standalone: true,
  template: `<p>Content</p>`,
  styles: `
    :host {
      display: block;          /* make the host a block element */
      border-radius: 8px;
      padding: 1rem;
      box-shadow: 0 2px 8px rgba(0,0,0,.1);
    }
  `,
})
export class CardComponent {}

// DOM:
// <app-card style="display:block; ...">   ← host element
//   <p>Content</p>
// </app-card>
```

---

## 114. Using Host Elements Like Regular Elements

**What is this:** Styling and binding properties directly on the host element via the `host` decorator property.

**Description:** The `host` object in `@Component` lets you add classes, attributes, and event listeners to the host element without touching the template. This keeps the template clean and the host behavior co-located with the component definition.

**Examples:**

```ts
@Component({
  selector: 'app-card',
  standalone: true,
  template: `<ng-content />`,
  host: {
    class: 'card',           // always adds class="card" to the host
    role: 'region',          // static attribute
    '[class.highlighted]': 'isHighlighted', // dynamic class binding
  },
})
export class CardComponent {
  isHighlighted = false;
}
```

---

## 115. Interacting With Host Elements From Inside Components

**What is this:** Reading and reacting to events on the host element from within the component class.

**Description:** Use the `host` property with event bindings `(eventName): 'method()'` to listen for events on the host element itself — useful for keyboard, focus, or click handling without wrapping the template in an extra element.

**Examples:**

```ts
@Component({
  selector: 'app-card',
  standalone: true,
  template: `<ng-content />`,
  host: {
    '(click)': 'onClick()',
    '(mouseenter)': 'isHovered = true',
    '(mouseleave)': 'isHovered = false',
    '[class.hovered]': 'isHovered',
  },
})
export class CardComponent {
  isHovered = false;

  onClick() {
    console.log('Card clicked');
  }
}
```

---

## 116. When (Not) To Rely On Host Elements

**What is this:** Guidelines on when host-element styling/binding is appropriate vs. when to use a wrapper `<div>`.

**Description:** Use host element bindings for layout properties (`display`, `padding`) and simple event reactions. Avoid relying on the host for complex template logic — if you need conditional structure or multiple sibling elements responding differently, a wrapper `<div>` inside the template is clearer.

**Examples:**

```ts
// Good — layout on host, keeps template clean
host: { '[style.display]': '"flex"', '[style.gap.px]': '16' }

// Questionable — complex conditional logic on host is hard to follow
// Better to put this inside the template with @if
host: { '[class.mode-a]': 'x && !y && z > 2' }
```

---

## 117. Interacting with Host Elements via @HostListener & @HostBinding

**What is this:** The decorator-based alternative to the `host` object for listening to host events and binding host properties.

**Description:** `@HostListener('event')` decorates a method to run when the host element emits that event. `@HostBinding('property')` binds a class property to a host element property or attribute. Both are older style — the `host: {}` object is now preferred, but you'll encounter these in existing codebases.

**Examples:**

```ts
import { Component, HostListener, HostBinding } from '@angular/core';

@Component({ selector: 'app-card', standalone: true, template: `<ng-content />` })
export class CardComponent {
  @HostBinding('class.hovered') isHovered = false;
  @HostBinding('attr.role') role = 'region';

  @HostListener('mouseenter') onEnter() { this.isHovered = true; }
  @HostListener('mouseleave') onLeave() { this.isHovered = false; }

  // Listen to document-level events
  @HostListener('document:keydown.escape') onEscape() {
    console.log('Escape pressed');
  }
}
```

---

## 118. Accessing Host Elements Programmatically

**What is this:** Getting a direct reference to the host DOM element using `ElementRef`.

**Description:** Inject `ElementRef` to access the raw `nativeElement`. Use this sparingly — direct DOM access bypasses Angular's rendering pipeline and breaks SSR. Prefer `@HostBinding` or the `host` object for styling, and `Renderer2` for DOM manipulation.

**Examples:**

```ts
import { Component, ElementRef, inject, afterNextRender } from '@angular/core';

@Component({ selector: 'app-card', standalone: true, template: `<ng-content />` })
export class CardComponent {
  private el = inject(ElementRef);

  constructor() {
    // Access the native DOM element — only safe after render
    afterNextRender(() => {
      console.log(this.el.nativeElement); // <app-card> DOM node
      console.log(this.el.nativeElement.offsetWidth); // actual rendered width
    });
  }
}
```

---

## 120. There's More Than One Way Of Binding CSS Classes Dynamically

**What is this:** All the ways to conditionally apply CSS classes in Angular templates.

**Description:** Angular provides several syntaxes for class binding — each has a use case. `[class.name]` for a single toggle, `[class]` for replacing all classes, `[ngClass]` for multiple conditions at once.

**Examples:**

```html
<!-- 1. Single class toggle -->
<div [class.active]="isActive">...</div>

<!-- 2. Replace all classes with a string or array -->
<div [class]="isActive ? 'card active' : 'card'">...</div>

<!-- 3. ngClass — object syntax for multiple conditions -->
<div [ngClass]="{ active: isActive, highlighted: isHighlighted, disabled: !isEnabled }">
  ...
</div>
```

```ts
import { NgClass } from '@angular/common';

@Component({ standalone: true, imports: [NgClass], template: `...` })
export class CardComponent {
  isActive = true;
  isHighlighted = false;
  isEnabled = true;
}
```

---

## 121. A Closer Look At Dynamic Inline Style Binding

**What is this:** Binding inline styles dynamically using `[style.property]` and `[ngStyle]`.

**Description:** Use `[style.propertyName]` for a single style, or `[ngStyle]` for multiple. Units can be included in the binding key (e.g. `[style.width.px]`). Prefer CSS classes over inline styles for anything that can be expressed in CSS.

**Examples:**

```html
<!-- Single style -->
<div [style.color]="textColor">Text</div>

<!-- With unit shorthand -->
<div [style.width.px]="cardWidth">Card</div>
<div [style.font-size.rem]="fontSize">Text</div>

<!-- Multiple styles — object syntax -->
<div [ngStyle]="{ color: textColor, 'font-size': fontSize + 'rem', opacity: isVisible ? 1 : 0 }">
  ...
</div>
```

---

## 122. Manipulating State & Using Literal Values

**What is this:** Passing static literal values (not variables) through property binding.

**Description:** Property binding `[prop]="expression"` evaluates the expression as TypeScript. To pass a string literal, wrap it in quotes: `[prop]="'hello'"`. To pass a number or boolean, no quotes needed: `[count]="5"`, `[active]="true"`.

**Examples:**

```html
<!-- Passing a literal string — note the inner single quotes -->
<app-button [label]="'Save Changes'" />

<!-- Passing a literal number -->
<app-progress [max]="100" [value]="75" />

<!-- Passing a literal boolean -->
<app-input [required]="true" [disabled]="false" />

<!-- Shorthand for static string — no binding needed -->
<app-button label="Save Changes" />
<!-- Angular treats unbound attributes as string literals automatically -->
```

---

## 123. Introducing the Component Lifecycle: ngOnInit

**What is this:** The first lifecycle hook — `ngOnInit` — and when to use it instead of the constructor.

**Description:** The constructor runs before Angular has set input values. `ngOnInit` runs after inputs are set, making it the right place for initialization logic that depends on inputs. With signal inputs, `ngOnInit` is less needed — signal values are available immediately.

**Examples:**

```ts
import { Component, Input, OnInit } from '@angular/core';

@Component({ selector: 'app-user', standalone: true, template: `<p>{{ greeting }}</p>` })
export class UserComponent implements OnInit {
  @Input({ required: true }) name!: string;
  greeting = '';

  constructor() {
    // this.name is NOT available here yet — inputs not set
    console.log(this.name); // undefined
  }

  ngOnInit() {
    // this.name IS available here — inputs have been set
    this.greeting = `Hello, ${this.name}!`;
  }
}
```

---

## 124. Implementing Lifecycle Interfaces

**What is this:** Declaring lifecycle interfaces (`OnInit`, `OnDestroy`, etc.) for type safety and intent clarity.

**Description:** Angular's lifecycle hooks are just methods with specific names. Implementing the interface (`implements OnInit`) makes TypeScript enforce that the method signature is correct and signals your intent to other developers.

**Examples:**

```ts
import { Component, OnInit, OnDestroy, OnChanges, SimpleChanges } from '@angular/core';

@Component({ selector: 'app-demo', standalone: true, template: `` })
export class DemoComponent implements OnInit, OnDestroy, OnChanges {
  ngOnChanges(changes: SimpleChanges) {
    // Called when any @Input value changes
    console.log('Inputs changed:', changes);
  }

  ngOnInit() {
    // Called once after first ngOnChanges
  }

  ngOnDestroy() {
    // Called just before the component is removed from the DOM
  }
}
```

---

## 125. Component Lifecycle - A Deep Dive

**What is this:** The full lifecycle hook sequence and what each hook is for.

**Description:** Angular calls hooks in a fixed order. Most real-world code only needs `ngOnInit` and `ngOnDestroy`. `ngOnChanges` is useful when you need to react to input changes with `@Input()` (signal inputs use `effect()` instead).

**Examples:**

```ts
// Full lifecycle order:
// 1. constructor()           — DI only, no inputs yet
// 2. ngOnChanges(changes)    — called before ngOnInit and on every @Input change
// 3. ngOnInit()              — once, after first ngOnChanges
// 4. ngDoCheck()             — every change detection cycle (rarely needed)
// 5. ngAfterContentInit()    — once, after ng-content is projected
// 6. ngAfterContentChecked() — after every content check
// 7. ngAfterViewInit()       — once, after the component's view (and children) are initialized
// 8. ngAfterViewChecked()    — after every view check
// 9. ngOnDestroy()           — once, just before removal

// Most components only need:
export class MyComponent implements OnInit, OnDestroy {
  ngOnInit() { /* setup */ }
  ngOnDestroy() { /* cleanup */ }
}
```

---

## 126. Component Cleanup with ngOnDestroy

**What is this:** Preventing memory leaks by cleaning up subscriptions, timers, and listeners in `ngOnDestroy`.

**Description:** When a component is removed from the DOM, any setInterval, event listener, or observable subscription it started keeps running unless explicitly stopped. `ngOnDestroy` is the place to cancel them.

**Examples:**

```ts
import { Component, OnInit, OnDestroy } from '@angular/core';

@Component({ selector: 'app-timer', standalone: true, template: `<p>{{ seconds }}</p>` })
export class TimerComponent implements OnInit, OnDestroy {
  seconds = 0;
  private intervalId!: ReturnType<typeof setInterval>;

  ngOnInit() {
    this.intervalId = setInterval(() => this.seconds++, 1000);
  }

  ngOnDestroy() {
    clearInterval(this.intervalId); // prevent leak when component is removed
  }
}
```

---

## 127. Component Cleanup with DestroyRef

**What is this:** The modern alternative to `ngOnDestroy` — registering cleanup callbacks with `DestroyRef`.

**Description:** Inject `DestroyRef` and call `.onDestroy(callback)` to register cleanup logic anywhere in the class — not just in the `ngOnDestroy` method. This is cleaner for services or composable utilities, and works well alongside `inject()`.

**Examples:**

```ts
import { Component, OnInit, inject, DestroyRef } from '@angular/core';

@Component({ selector: 'app-timer', standalone: true, template: `<p>{{ seconds }}</p>` })
export class TimerComponent implements OnInit {
  seconds = 0;
  private destroyRef = inject(DestroyRef);

  ngOnInit() {
    const id = setInterval(() => this.seconds++, 1000);

    // Register cleanup — runs when the component is destroyed
    this.destroyRef.onDestroy(() => clearInterval(id));
  }
}
```

---

## 129. Working with Template Variables

**What is this:** Declaring a reference to a DOM element or component instance directly in the template with `#varName`.

**Description:** A template variable (`#ref`) gives you a reference to the element or component it is placed on. You can pass it to event handlers or read its value without going through the component class.

**Examples:**

```html
<!-- #titleInput is a reference to the <input> DOM element -->
<input #titleInput type="text" />
<button (click)="onAdd(titleInput.value)">Add</button>
<!-- No [(ngModel)] or property needed — read the value on demand -->
```

```ts
export class TasksComponent {
  onAdd(title: string) {
    console.log('New task:', title);
  }
}
```

---

## 130. Extracting Input Values via Template Variables

**What is this:** Using template variables to read form field values on submit instead of two-way binding.

**Description:** For simple, read-once scenarios (submit button), a template variable is lighter than `[(ngModel)]`. The variable holds the live DOM element, so `.value` always reflects the current input content.

**Examples:**

```html
<form (ngSubmit)="onSubmit(titleInput.value, dateInput.value)">
  <input #titleInput type="text" placeholder="Task title" />
  <input #dateInput type="date" />
  <button type="submit">Add Task</button>
</form>
```

```ts
onSubmit(title: string, date: string) {
  if (!title || !date) return;
  this.tasks.push({ id: Date.now().toString(), title, dueDate: date });
}
```

---

## 131. Template Variables & Component Instances

**What is this:** Using a template variable on a component selector to get a reference to the component instance.

**Description:** When `#ref` is placed on a component element (not a plain DOM element), the variable holds the component class instance — giving you access to its public properties and methods.

**Examples:**

```ts
@Component({ selector: 'app-new-task', standalone: true, template: `...` })
export class NewTaskComponent {
  title = '';
  reset() { this.title = ''; }
}
```

```html
<!-- #taskForm is the NewTaskComponent instance -->
<app-new-task #taskForm />
<button (click)="taskForm.reset()">Clear Form</button>
<p>Current title: {{ taskForm.title }}</p>
```

---

## 132. Getting Access to Template Elements via ViewChild

**What is this:** Querying a template element or child component from the class using `@ViewChild`.

**Description:** `@ViewChild` injects a reference to a DOM element or child component into the class property. It is available after `ngAfterViewInit`. Use it when you need access to the element in TypeScript, not just in the template.

**Examples:**

```ts
import { Component, ViewChild, ElementRef, AfterViewInit } from '@angular/core';

@Component({
  selector: 'app-search',
  standalone: true,
  template: `<input #searchInput type="text" />`,
})
export class SearchComponent implements AfterViewInit {
  @ViewChild('searchInput') searchInput!: ElementRef<HTMLInputElement>;

  ngAfterViewInit() {
    // Auto-focus the input when the component renders
    this.searchInput.nativeElement.focus();
  }
}
```

---

## 133. Using The viewChild Signal Function

**What is this:** The modern, signal-based alternative to `@ViewChild`.

**Description:** `viewChild()` returns a signal that holds the queried element or component instance. No `AfterViewInit` needed — the signal value is available reactively. Use `viewChild.required()` when the element is always present.

**Examples:**

```ts
import { Component, viewChild, ElementRef, afterNextRender } from '@angular/core';

@Component({
  selector: 'app-search',
  standalone: true,
  template: `<input #searchInput type="text" />`,
})
export class SearchComponent {
  searchInput = viewChild.required<ElementRef<HTMLInputElement>>('searchInput');

  constructor() {
    afterNextRender(() => {
      this.searchInput().nativeElement.focus();
    });
  }
}
```

---

## 134. ViewChild vs ContentChild

**What is this:** The difference between querying the component's own view vs. querying projected content.

**Description:** `viewChild` / `@ViewChild` queries elements inside the component's own template. `contentChild` / `@ContentChild` queries elements that were projected in via `<ng-content>`. Use the right one based on where the element lives.

**Examples:**

```ts
import { Component, contentChild, viewChild, ElementRef } from '@angular/core';

@Component({
  selector: 'app-card',
  standalone: true,
  template: `
    <div #wrapper>           <!-- viewChild targets this -->
      <ng-content />         <!-- contentChild targets what the parent projects here -->
    </div>
  `,
})
export class CardComponent {
  wrapper = viewChild.required<ElementRef>('wrapper');  // own template
  projectedTitle = contentChild<ElementRef>('title');   // parent's projected #title
}
```

```html
<!-- Parent -->
<app-card>
  <h2 #title>Projected Heading</h2>  <!-- contentChild finds this -->
</app-card>
```

---

## 135. A Closer Look at Decorator-based Queries & Lifecycle Hooks

**What is this:** When decorator queries (`@ViewChild`, `@ContentChild`) become available relative to lifecycle hooks.

**Description:** `@ViewChild` results are ready in `ngAfterViewInit`. `@ContentChild` results are ready in `ngAfterContentInit`. Signal-based queries (`viewChild()`, `contentChild()`) are reactive and don't require these hooks — they update automatically.

**Examples:**

```ts
import { Component, ViewChild, ContentChild, AfterViewInit, AfterContentInit, ElementRef } from '@angular/core';

@Component({ selector: 'app-example', standalone: true, template: `<div #box></div><ng-content />` })
export class ExampleComponent implements AfterViewInit, AfterContentInit {
  @ViewChild('box') box!: ElementRef;
  @ContentChild('label') label!: ElementRef;

  ngAfterContentInit() {
    console.log(this.label); // projected content ready
  }

  ngAfterViewInit() {
    console.log(this.box); // own view ready
  }
}
```

---

## 137. The afterRender and afterNextRender Lifecycle Functions

**What is this:** Running code after every render (`afterRender`) or only after the first render (`afterNextRender`).

**Description:** These are functions (not interfaces) called in the constructor. `afterNextRender` is ideal for one-time DOM setup (focus, scroll, measuring). `afterRender` runs after every render cycle — use it only when you need to react to every change.

**Examples:**

```ts
import { Component, afterNextRender, afterRender, viewChild, ElementRef } from '@angular/core';

@Component({ selector: 'app-chart', standalone: true, template: `<canvas #canvas></canvas>` })
export class ChartComponent {
  canvas = viewChild.required<ElementRef<HTMLCanvasElement>>('canvas');

  constructor() {
    // Runs once — after the first render
    afterNextRender(() => {
      const ctx = this.canvas().nativeElement.getContext('2d');
      // Initialize chart library here
    });

    // Runs after every render — use sparingly
    afterRender(() => {
      console.log('View updated');
    });
  }
}
```

---

## 138. Making Sense of Signal Effects

**What is this:** Running side effects automatically whenever a signal's value changes using `effect()`.

**Description:** `effect()` takes a function that Angular re-runs whenever any signal read inside it changes. It replaces `ngOnChanges` for signal inputs and is the signal-world equivalent of a reactive subscription. Call it in the constructor.

**Examples:**

```ts
import { Component, signal, effect, input } from '@angular/core';

@Component({ selector: 'app-user', standalone: true, template: `<p>{{ name() }}</p>` })
export class UserComponent {
  name = input.required<string>();
  private logCount = signal(0);

  constructor() {
    effect(() => {
      // Re-runs automatically whenever name() or logCount() changes
      console.log(`Name changed to: ${this.name()}, log #${this.logCount()}`);
    });
  }
}
```

---

## 139. Signal Effects Cleanup Functions

**What is this:** Registering a cleanup callback inside `effect()` that runs before the next execution.

**Description:** Pass a cleanup function to `onCleanup` (provided as the first argument to the effect callback) to tear down any resources (timers, listeners) before the effect re-runs or the component is destroyed.

**Examples:**

```ts
import { Component, signal, effect } from '@angular/core';

@Component({ selector: 'app-search', standalone: true, template: `` })
export class SearchComponent {
  query = signal('');

  constructor() {
    effect((onCleanup) => {
      const timeoutId = setTimeout(() => {
        console.log('Search for:', this.query());
        // fire API call here
      }, 300); // debounce

      // Cleanup runs before the next effect execution
      onCleanup(() => clearTimeout(timeoutId));
    });
  }
}
```

---

## 142. A Closer Look At Template For Loops

**What is this:** Advanced `@for` features — `track`, loop variables, and `@empty`.

**Description:** The `track` expression is required and tells Angular how to identify items for efficient DOM updates. Loop exposes local variables: `$index`, `$first`, `$last`, `$even`, `$odd`, `$count`.

**Examples:**

```html
@for (task of tasks(); track task.id; let i = $index, isLast = $last) {
  <li [class.last]="isLast">
    {{ i + 1 }}. {{ task.title }}
  </li>
} @empty {
  <li>No tasks yet.</li>
}
```

```ts
// track by index — use when items have no stable id
@for (item of items; track $index) { ... }

// track by id — preferred when items have unique ids
@for (item of items; track item.id) { ... }
```

---

## 143. Revisiting Inputs & Signals

**What is this:** Combining `input()` signal inputs with `computed()` for derived values.

**Description:** Signal inputs are reactive — any `computed()` or `effect()` that reads them updates automatically when the parent changes the value. This makes derived display values clean and free of manual lifecycle management.

**Examples:**

```ts
import { Component, input, computed } from '@angular/core';

@Component({
  selector: 'app-user-card',
  standalone: true,
  template: `
    <img [src]="avatarUrl()" [alt]="fullName()" />
    <p>{{ fullName() }}</p>
  `,
})
export class UserCardComponent {
  firstName = input.required<string>();
  lastName = input.required<string>();
  avatarFile = input<string>('default.png');

  fullName = computed(() => `${this.firstName()} ${this.lastName()}`);
  avatarUrl = computed(() => `assets/avatars/${this.avatarFile()}`);
}
```

---

## 144. Updating Signal Values

**What is this:** The three ways to change a signal's value: `set`, `update`, and `mutate` (arrays/objects).

**Description:** `set(newValue)` replaces the value. `update(fn)` derives the new value from the old one. For objects and arrays, always produce a new reference — signals use reference equality to detect changes.

**Examples:**

```ts
count = signal(0);

// set — replace entirely
this.count.set(10);

// update — derive from current value
this.count.update(c => c + 1);

// Arrays — produce a new array (don't mutate in place)
tasks = signal<Task[]>([]);

addTask(task: Task) {
  this.tasks.update(current => [...current, task]);
}

removeTask(id: string) {
  this.tasks.update(current => current.filter(t => t.id !== id));
}
```

---

## 145. Cross-Component Communication & State Management

**What is this:** Choosing between inputs/outputs, services with signals, and shared state for component communication.

**Description:** Direct parent-child communication uses inputs and outputs. For sibling or distant components, lift state into a service. For complex apps, a signal-based service acts as a lightweight store — components read from it reactively and call methods to mutate it.

**Examples:**

```ts
// Signal-based service as a simple state store
@Injectable({ providedIn: 'root' })
export class TasksStore {
  private _tasks = signal<Task[]>([]);
  readonly tasks = this._tasks.asReadonly();

  add(task: Task) { this._tasks.update(ts => [...ts, task]); }
  remove(id: string) { this._tasks.update(ts => ts.filter(t => t.id !== id)); }
}

// Any component — reads reactively, no prop drilling
@Component({ ... })
export class TaskListComponent {
  store = inject(TasksStore);
  // template uses store.tasks() — updates automatically
}
```

---

## 146. Configuring Component Inputs & Outputs

**What is this:** Advanced `input()` and `output()` configuration options.

**Description:** `input()` accepts a transform function to coerce the incoming value. `output()` accepts no config options but the type parameter sets the emitted payload type. `input.required()` enforces that the parent always provides a value.

**Examples:**

```ts
import { Component, input, output } from '@angular/core';

@Component({ selector: 'app-item', standalone: true, template: `` })
export class ItemComponent {
  // Transform: convert string "true"/"false" attribute to boolean
  disabled = input(false, { transform: (v: boolean | string) => v === true || v === 'true' });

  // Alias: parent binds with [item-label], component reads as label()
  label = input.required<string>({ alias: 'item-label' });

  // Typed output
  selected = output<{ id: string; label: string }>();
}
```

```html
<app-item item-label="Task A" [disabled]="false" (selected)="onSelect($event)" />
```

---

## 148. Setting Up Custom Two-Way Binding

**What is this:** Implementing a custom two-way binding by pairing an `@Input` with a matching `@Output` named `inputNameChange`.

**Description:** Angular's `[(x)]` syntax desugars to `[x]="val" (xChange)="val = $event"`. To support it, name the output `<inputName>Change`. The child emits the new value; the parent's variable updates automatically.

**Examples:**

```ts
import { Component, Input, Output, EventEmitter } from '@angular/core';

@Component({
  selector: 'app-counter',
  standalone: true,
  template: `
    <button (click)="decrement()">-</button>
    <span>{{ count }}</span>
    <button (click)="increment()">+</button>
  `,
})
export class CounterComponent {
  @Input() count = 0;
  @Output() countChange = new EventEmitter<number>(); // must be inputName + "Change"

  increment() { this.countChange.emit(this.count + 1); }
  decrement() { this.countChange.emit(this.count - 1); }
}
```

```html
<!-- Two-way binding — parentCount updates automatically -->
<app-counter [(count)]="parentCount" />
<p>Parent sees: {{ parentCount }}</p>
```

---

## 149. An Easier Way of Setting Up Custom Two-Way Binding

**What is this:** Using the `model()` signal function for custom two-way binding with less boilerplate.

**Description:** `model()` creates a signal that supports two-way binding automatically — no need to manually create a paired `@Input` + `@Output`. The parent binds with `[(property)]` and the child reads/writes the signal.

**Examples:**

```ts
import { Component, model } from '@angular/core';

@Component({
  selector: 'app-counter',
  standalone: true,
  template: `
    <button (click)="decrement()">-</button>
    <span>{{ count() }}</span>
    <button (click)="increment()">+</button>
  `,
})
export class CounterComponent {
  count = model(0); // replaces @Input() count + @Output() countChange

  increment() { this.count.update(c => c + 1); }
  decrement() { this.count.update(c => c - 1); }
}
```

```html
<!-- Same [(count)] syntax — no extra setup needed -->
<app-counter [(count)]="parentCount" />
```

---

# Section 7: Enhancing Elements with Directives - Deep Dive

> Lessons 150 (1min intro) and 152 (1min project setup) are skipped — no new concepts.

---

## 151. Understanding Directives

**What is this:** What directives are and how they differ from components.

**Description:** A directive adds behavior or structure to an existing element without creating a new one. Components are directives with a template. There are two other kinds: **attribute directives** (change the look or behavior of an element) and **structural directives** (add/remove elements from the DOM).

**Examples:**

```ts
// Three kinds of directives:

// 1. Component — directive WITH a template
@Component({ selector: 'app-card', template: `<ng-content />` })
export class CardComponent {}

// 2. Attribute directive — changes an existing element's behavior/style
// <p appHighlight>Hello</p>  ← same <p>, just enhanced

// 3. Structural directive — adds/removes DOM elements
// <p *ngIf="show">Hello</p>  ← <p> may or may not exist in the DOM
// @for, @if are the modern built-in structural directives
```

---

## 153. Analyzing a Built-in Attribute Directive: ngModel

**What is this:** How `ngModel` works internally as an attribute directive.

**Description:** `ngModel` is an attribute directive from `FormsModule`. It attaches to a form control element, listens for value changes, and syncs the element's value with a component property — bidirectionally. Understanding it as a directive explains why you must import `FormsModule` to use it.

**Examples:**

```ts
// ngModel under the hood (simplified concept):
// It does two things at once:
// 1. [ngModel]="value"     → sets the element's value property
// 2. (ngModelChange)="value = $event"  → listens for changes and updates the property

// These are equivalent:
<input [(ngModel)]="title" />
<input [ngModel]="title" (ngModelChange)="title = $event" />

// ngModel is just a directive — it needs FormsModule to be available
import { FormsModule } from '@angular/forms';

@Component({
  standalone: true,
  imports: [FormsModule], // ← directive is provided here
  template: `<input [(ngModel)]="title" />`,
})
export class FormComponent {
  title = '';
}
```

---

## 154. Analyzing a Built-in Structural Directive: ngIf

**What is this:** How `*ngIf` works and what the `*` syntax desugars to.

**Description:** The `*` prefix is syntactic sugar. `*ngIf="condition"` expands to `[ngIf]="condition"` on an `<ng-template>`. Angular uses the directive to decide whether to stamp the template into the DOM or remove it entirely — not just hide it.

**Examples:**

```ts
// *ngIf syntactic sugar — these are identical:
<p *ngIf="isLoggedIn">Welcome</p>

<ng-template [ngIf]="isLoggedIn">
  <p>Welcome</p>
</ng-template>

// Key point: *ngIf REMOVES the element from the DOM (not just hidden)
// Compare:
<p *ngIf="show">Removed from DOM when false</p>
<p [style.display]="show ? 'block' : 'none'">Hidden with CSS, still in DOM</p>

// Modern equivalent — prefer @if in new projects:
@if (isLoggedIn) { <p>Welcome</p> }
```

---

## 155. Getting Started with Custom Directives

**What is this:** Creating your first attribute directive from scratch.

**Description:** A custom attribute directive is a class decorated with `@Directive`. Its selector is typically an attribute in square brackets `[appMyDirective]`. Angular instantiates it whenever it finds that attribute on an element and injects the host `ElementRef` so you can interact with the DOM.

**Examples:**

```ts
// highlight.directive.ts
import { Directive, ElementRef, inject, OnInit } from '@angular/core';

@Directive({
  selector: '[appHighlight]', // matches any element with the appHighlight attribute
  standalone: true,
})
export class HighlightDirective implements OnInit {
  private el = inject(ElementRef);

  ngOnInit() {
    this.el.nativeElement.style.backgroundColor = 'yellow';
  }
}
```

```ts
// Using it — import and apply the attribute
@Component({
  standalone: true,
  imports: [HighlightDirective],
  template: `<p appHighlight>This text has a yellow background.</p>`,
})
export class AppComponent {}
```

---

## 156. Using Attribute Directives To Change Element Behavior

**What is this:** Reacting to host events inside a directive to change element behavior dynamically.

**Description:** Use the `host` property (or `@HostListener`) in the directive to listen for events on the element the directive is applied to. This keeps behavior encapsulated in the directive and out of the component.

**Examples:**

```ts
import { Directive, ElementRef, inject } from '@angular/core';

@Directive({
  selector: '[appHighlight]',
  standalone: true,
  host: {
    '(mouseenter)': 'onEnter()',
    '(mouseleave)': 'onLeave()',
  },
})
export class HighlightDirective {
  private el = inject(ElementRef);

  onEnter() {
    this.el.nativeElement.style.backgroundColor = 'yellow';
  }

  onLeave() {
    this.el.nativeElement.style.backgroundColor = '';
  }
}
```

```html
<!-- Applied to any element — no component logic needed -->
<p appHighlight>Hover over me</p>
<button appHighlight>Or me</button>
```

---

## 157. Working with Inputs in Custom Directives

**What is this:** Making a directive configurable by accepting `input()` values from the parent.

**Description:** Directives can declare inputs just like components. The parent passes values through attribute binding. This lets one directive cover many scenarios (e.g. a highlight directive that accepts the color).

**Examples:**

```ts
import { Directive, ElementRef, inject, input, OnInit } from '@angular/core';

@Directive({
  selector: '[appHighlight]',
  standalone: true,
})
export class HighlightDirective implements OnInit {
  private el = inject(ElementRef);

  color = input<string>('yellow');       // optional — defaults to yellow
  hoverColor = input<string>('orange');  // color on hover

  ngOnInit() {
    this.el.nativeElement.style.backgroundColor = this.color();
  }
}
```

```html
<!-- Default color -->
<p appHighlight>Yellow background</p>

<!-- Custom color -->
<p appHighlight [color]="'lightblue'" [hoverColor]="'deepskyblue'">Blue background</p>
```

---

## 158. Directives & Dependency Injection

**What is this:** Injecting services into a directive the same way as in a component.

**Description:** Directives participate in Angular's DI system fully. Use `inject()` in the class body to get a service. This enables directives to read from or write to shared state — for example, a directive that logs to an analytics service on click.

**Examples:**

```ts
import { Directive, inject } from '@angular/core';
import { LoggingService } from '../logging.service';

@Directive({
  selector: '[appTrackClick]',
  standalone: true,
  host: { '(click)': 'onClick()' },
})
export class TrackClickDirective {
  private logger = inject(LoggingService);

  onClick() {
    this.logger.log('Element clicked');
  }
}
```

```ts
// logging.service.ts
@Injectable({ providedIn: 'root' })
export class LoggingService {
  log(message: string) {
    console.log(`[Log] ${message}`);
  }
}
```

---

## 159. Building Another Directive

**What is this:** A second directive example — `appSafeLink` — that warns before navigating to an external URL.

**Description:** This directive attaches to `<a>` elements, intercepts the click, and shows a confirmation dialog before allowing external navigation. It shows how directives compose cleanly with native HTML semantics.

**Examples:**

```ts
import { Directive, inject, input } from '@angular/core';

@Directive({
  selector: 'a[appSafeLink]',  // only matches <a> elements with the attribute
  standalone: true,
  host: {
    '(click)': 'onConfirm($event)',
  },
})
export class SafeLinkDirective {
  queryParam = input<string>('myapp');

  onConfirm(event: MouseEvent) {
    const confirmed = window.confirm('Do you want to leave this app?');
    if (!confirmed) {
      event.preventDefault(); // block navigation
    }
  }
}
```

```html
<a href="https://angular.dev" appSafeLink>Angular Docs</a>
```

---

## 160. Building a Custom Structural Directive

**What is this:** Creating a directive that conditionally adds or removes elements from the DOM.

**Description:** Structural directives use `TemplateRef` (the template to stamp) and `ViewContainerRef` (the container to stamp it into). Calling `createEmbeddedView()` adds the template; `clear()` removes it. This is exactly how `*ngIf` works internally.

**Examples:**

```ts
import { Directive, TemplateRef, ViewContainerRef, inject, input, effect } from '@angular/core';

@Directive({
  selector: '[appShowIf]',
  standalone: true,
})
export class ShowIfDirective {
  private template = inject(TemplateRef);
  private container = inject(ViewContainerRef);

  condition = input.required<boolean>({ alias: 'appShowIf' });

  constructor() {
    effect(() => {
      if (this.condition()) {
        this.container.createEmbeddedView(this.template); // add to DOM
      } else {
        this.container.clear(); // remove from DOM
      }
    });
  }
}
```

```html
<!-- Works like *ngIf -->
<p *appShowIf="isLoggedIn">Welcome back!</p>
```

---

## 161. Structural Directives & Syntactic Sugar

**What is this:** How the `*directive` shorthand expands to `<ng-template [directive]>`.

**Description:** The `*` prefix is always syntactic sugar for `<ng-template>`. Understanding the expansion helps when you need to use `*ngIf` with `else`, pass context variables from `*ngFor`, or write custom structural directives with the correct input names.

**Examples:**

```html
<!-- Sugar form -->
<li *ngFor="let item of items; let i = index; trackBy: trackById">
  {{ i }}: {{ item.name }}
</li>

<!-- Expanded form (what Angular actually compiles) -->
<ng-template ngFor [ngForOf]="items" let-item let-i="index" [ngForTrackBy]="trackById">
  <li>{{ i }}: {{ item.name }}</li>
</ng-template>

<!-- Custom directive — input alias must match the selector for * to work -->
<!-- selector: '[appShowIf]', input alias: 'appShowIf' -->
<p *appShowIf="isLoggedIn">...</p>
<!-- expands to: -->
<ng-template [appShowIf]="isLoggedIn"><p>...</p></ng-template>
```

---

## 162. Host Directives & Composition

**What is this:** Composing multiple directives onto a component's host element via `hostDirectives`.

**Description:** `hostDirectives` lets a component apply other directives to itself without the parent needing to add them. This is Angular's version of directive composition — instead of inheritance, you compose behavior. Inputs and outputs from the host directive can be exposed on the component.

**Examples:**

```ts
import { Component } from '@angular/core';
import { HighlightDirective } from './highlight.directive';
import { TrackClickDirective } from './track-click.directive';

@Component({
  selector: 'app-button',
  standalone: true,
  template: `<ng-content />`,
  // These directives are applied to <app-button> automatically
  hostDirectives: [
    TrackClickDirective, // no inputs/outputs exposed
    {
      directive: HighlightDirective,
      inputs: ['color'],   // expose HighlightDirective's input on <app-button>
      outputs: [],
    },
  ],
})
export class ButtonComponent {}
```

```html
<!-- Parent uses ButtonComponent — gets HighlightDirective behavior for free -->
<app-button [color]="'lightgreen'">Save</app-button>
<!-- No need to add appHighlight — it's composed in -->
```

---

# Section 8: Transforming Values with Pipes - Deep Dive

> Lesson 163 (1min intro) is skipped.

---

## 164. Making Sense of Pipes

**What is this:** What pipes are, where they run, and why they exist.

**Description:** A pipe transforms a value for display only — it does not mutate the underlying data. Pipes live entirely in the template, are applied with `|`, and receive the value on their left as input. Angular re-runs a pipe only when its input changes (pure pipes) or on every change detection cycle (impure pipes).

**Examples:**

```ts
// Pipes sit between the data and the DOM — they never touch the source
component property: 'hello world'
        ↓  | uppercase
template output: 'HELLO WORLD'   ← original property is still 'hello world'

// Syntax: {{ value | pipeName }}
// Pipes can be chained: {{ value | pipe1 | pipe2 }}
// Pipes can accept arguments: {{ value | pipeName:arg1:arg2 }}
```

---

## 165. Using Built-in Pipes

**What is this:** The most commonly used Angular built-in pipes.

**Description:** Angular ships many pipes in `@angular/common`. Standalone components import each one individually; module-based apps get them via `CommonModule`.

**Examples:**

```ts
import { UpperCasePipe, LowerCasePipe, DatePipe, CurrencyPipe, DecimalPipe, PercentPipe } from '@angular/common';

@Component({
  standalone: true,
  imports: [UpperCasePipe, LowerCasePipe, DatePipe, CurrencyPipe, DecimalPipe, PercentPipe],
  template: `
    <p>{{ 'hello' | uppercase }}</p>           <!-- HELLO -->
    <p>{{ 'WORLD' | lowercase }}</p>           <!-- world -->
    <p>{{ today | date }}</p>                  <!-- Jan 1, 2025 -->
    <p>{{ today | date:'yyyy-MM-dd' }}</p>     <!-- 2025-01-01 -->
    <p>{{ price | currency }}</p>              <!-- $1,234.56 -->
    <p>{{ price | currency:'EUR':'symbol' }}</p> <!-- €1,234.56 -->
    <p>{{ 3.14159 | number:'1.2-2' }}</p>     <!-- 3.14 -->
    <p>{{ 0.85 | percent }}</p>               <!-- 85% -->
  `,
})
export class DemoComponent {
  today = new Date();
  price = 1234.56;
}
```

---

## 166. More Built-in Pipes Examples

**What is this:** Lesser-used but useful built-in pipes — `json`, `slice`, `keyvalue`, `async`.

**Description:** `json` is invaluable for debugging. `slice` works on arrays and strings. `keyvalue` lets you iterate over object properties with `@for`. `async` unwraps Observables and Promises directly in the template.

**Examples:**

```ts
import { JsonPipe, SlicePipe, KeyValuePipe, AsyncPipe } from '@angular/common';

@Component({
  standalone: true,
  imports: [JsonPipe, SlicePipe, KeyValuePipe, AsyncPipe],
  template: `
    <!-- Debug any value -->
    <pre>{{ user | json }}</pre>

    <!-- First 3 items of an array -->
    @for (item of items | slice:0:3; track item) { <p>{{ item }}</p> }

    <!-- Iterate object entries -->
    @for (entry of config | keyvalue; track entry.key) {
      <p>{{ entry.key }}: {{ entry.value }}</p>
    }

    <!-- Unwrap a Promise or Observable -->
    <p>{{ userData$ | async }}</p>
  `,
})
export class DemoComponent {
  user = { name: 'Alice', age: 30 };
  items = ['a', 'b', 'c', 'd', 'e'];
  config = { theme: 'dark', lang: 'en' };
  userData$ = fetch('/api/user').then(r => r.json());
}
```

---

## 167. Building a First Custom Pipe

**What is this:** Creating a standalone pipe class with `@Pipe`.

**Description:** A pipe is a class decorated with `@Pipe` that implements `PipeTransform`. The `transform(value, ...args)` method receives the value and any arguments, and returns the transformed result. Add it to the component's `imports` to use it.

**Examples:**

```ts
// temperature.pipe.ts
import { Pipe, PipeTransform } from '@angular/core';

@Pipe({
  name: 'temperature',  // used as {{ value | temperature }}
  standalone: true,
})
export class TemperaturePipe implements PipeTransform {
  transform(value: number): string {
    return `${value.toFixed(1)} °C`;
  }
}
```

```ts
// Using it
@Component({
  standalone: true,
  imports: [TemperaturePipe],
  template: `<p>{{ temp | temperature }}</p>`,  // 36.6 °C
})
export class WeatherComponent {
  temp = 36.6;
}
```

---

## 168. Using Custom Pipes to Perform Custom Transformations

**What is this:** A more practical custom pipe — truncating long text.

**Description:** Any transformation that would clutter a template expression is a good candidate for a pipe. Keeping the template declarative and the logic in the pipe class makes both easier to test and read.

**Examples:**

```ts
// truncate.pipe.ts
import { Pipe, PipeTransform } from '@angular/core';

@Pipe({ name: 'truncate', standalone: true })
export class TruncatePipe implements PipeTransform {
  transform(value: string, limit = 50): string {
    if (value.length <= limit) return value;
    return value.slice(0, limit).trimEnd() + '…';
  }
}
```

```ts
@Component({
  standalone: true,
  imports: [TruncatePipe],
  template: `
    <p>{{ description | truncate }}</p>        <!-- default 50 chars -->
    <p>{{ description | truncate:20 }}</p>     <!-- 20 chars -->
  `,
})
export class CardComponent {
  description = 'This is a very long description that goes well beyond fifty characters.';
}
```

---

## 169. Accepting Parameters in Custom Pipes

**What is this:** Passing one or more arguments to a custom pipe with `:arg` syntax.

**Description:** Arguments after the first in `transform(value, arg1, arg2)` map to the `:arg1:arg2` template syntax. Each argument can have a default value. TypeScript types the parameters so callers know what to pass.

**Examples:**

```ts
// temperature.pipe.ts — convert between units
import { Pipe, PipeTransform } from '@angular/core';

type TempUnit = 'C' | 'F' | 'K';

@Pipe({ name: 'temperature', standalone: true })
export class TemperaturePipe implements PipeTransform {
  transform(value: number, fromUnit: TempUnit = 'C', toUnit: TempUnit = 'F'): string {
    let result: number;

    if (fromUnit === 'C' && toUnit === 'F') result = value * 9/5 + 32;
    else if (fromUnit === 'F' && toUnit === 'C') result = (value - 32) * 5/9;
    else result = value;

    return `${result.toFixed(1)} °${toUnit}`;
  }
}
```

```html
<p>{{ 100 | temperature:'C':'F' }}</p>   <!-- 212.0 °F -->
<p>{{ 32 | temperature:'F':'C' }}</p>    <!-- 0.0 °C -->
<p>{{ 37 | temperature }}</p>            <!-- 98.6 °F (defaults) -->
```

---

## 170. Chaining Pipes & Being Aware of Limitations

**What is this:** Applying multiple pipes in sequence and understanding operator precedence with parameters.

**Description:** Pipes chain left to right — the output of one becomes the input of the next. When chaining a pipe that takes parameters, wrap the parameterized pipe in parentheses if the result feeds another pipe, to avoid ambiguity.

**Examples:**

```html
<!-- Chain: format as date, then uppercase -->
<p>{{ today | date:'fullDate' | uppercase }}</p>
<!-- SUNDAY, JANUARY 5, 2025 -->

<!-- Chain: truncate, then uppercase -->
<p>{{ longText | truncate:30 | uppercase }}</p>

<!-- Limitation: operator precedence -->
<!-- This is parsed as: {{ (value | a) : (b | c) }} — wrong! -->
<p>{{ value | a:b | c }}</p>

<!-- Correct — a gets argument b, result goes to c -->
<p>{{ (value | a:b) | c }}</p>
```

---

## 171. Building a Pipe That Sorts Items

**What is this:** A pipe that returns a sorted copy of an array.

**Description:** Sorting is a classic pipe use case — keep the original array untouched and return a new sorted copy. This also illustrates why impurity matters: if the array reference doesn't change (e.g. `push()`), a pure pipe won't re-run.

**Examples:**

```ts
// sort.pipe.ts
import { Pipe, PipeTransform } from '@angular/core';

@Pipe({ name: 'sort', standalone: true })
export class SortPipe implements PipeTransform {
  transform<T>(value: T[], key: keyof T, direction: 'asc' | 'desc' = 'asc'): T[] {
    return [...value].sort((a, b) => {
      const valA = a[key];
      const valB = b[key];
      if (valA < valB) return direction === 'asc' ? -1 : 1;
      if (valA > valB) return direction === 'asc' ? 1 : -1;
      return 0;
    });
  }
}
```

```html
@for (task of tasks | sort:'dueDate':'asc'; track task.id) {
  <p>{{ task.title }} — {{ task.dueDate }}</p>
}
```

---

## 172. Understanding How Pipes Are Executed

**What is this:** When Angular re-runs a pipe's `transform` method.

**Description:** Angular re-runs a **pure** pipe only when its input value reference changes — for primitives this means a new value, for objects/arrays this means a new reference. It does not deep-check object contents. This is why mutating an array in place (`push`, `splice`) won't trigger a pure pipe — the reference stays the same.

**Examples:**

```ts
// Pure pipe — DOES NOT re-run when you mutate in place
this.tasks.push(newTask);       // same array reference → pipe skips
this.tasks = [...this.tasks, newTask]; // new reference → pipe re-runs ✓

// This is why signal + spread is the correct pattern:
addTask(task: Task) {
  this.tasks.update(current => [...current, task]); // new array → pipe triggered
}
```

---

## 173. Pure & Impure Pipes

**What is this:** The difference between pure pipes (default) and impure pipes, and when to use each.

**Description:** A **pure** pipe runs only when its input reference changes — fast and efficient. An **impure** pipe (`pure: false`) runs on every change detection cycle — powerful but potentially slow. Use impure pipes only when you must react to internal mutations you can't avoid (rare).

**Examples:**

```ts
// Pure pipe (default) — runs only on reference change
@Pipe({ name: 'sort', standalone: true })
export class SortPipe implements PipeTransform {
  transform<T>(arr: T[], key: keyof T): T[] {
    return [...arr].sort(...);
  }
}

// Impure pipe — runs on every change detection tick
@Pipe({
  name: 'filterLive',
  standalone: true,
  pure: false,  // ← opt-in to impure
})
export class FilterLivePipe implements PipeTransform {
  transform(items: string[], query: string): string[] {
    return items.filter(i => i.includes(query));
  }
}
// Warning: impure pipes can cause performance issues in large lists
// Prefer signal-based filtering in the component class instead
```

---

## 174. Pipe Limitations & When Not To Use Them

**What is this:** When to avoid pipes and use component class logic or services instead.

**Description:** Pipes are display-only transformations. Avoid pipes when: (1) the transformation is expensive and runs frequently (impure); (2) you need the transformed value in TypeScript logic, not just the template; (3) the transformation has side effects. For those cases, compute the value in the class as a `computed()` signal or a getter.

**Examples:**

```ts
// Bad — async side effect in a pipe
@Pipe({ name: 'fetchUser', standalone: true, pure: false })
export class FetchUserPipe implements PipeTransform {
  transform(id: string) {
    return fetch(`/api/users/${id}`); // fires on every change detection — never do this
  }
}

// Good — use async pipe with a signal or observable prepared in the class
@Component({
  standalone: true,
  imports: [AsyncPipe],
  template: `<p>{{ user$ | async }}</p>`,
})
export class UserComponent {
  user$ = fetch('/api/user').then(r => r.json()); // prepared once in the class
}

// Best for filtering/sorting — computed signal, no pipe needed
filteredTasks = computed(() =>
  this.tasks().filter(t => t.title.includes(this.query()))
);
```
