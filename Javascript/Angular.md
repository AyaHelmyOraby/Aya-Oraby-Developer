# Angular Cheat Sheet and Guide

This README serves as a quick reference guide and cheat sheet for Angular, covering core concepts, API integration, forms, routing, observables, and essential commands for an Angular project.

## Table of Contents
1. [Introduction to Angular](#introduction-to-angular)
2. [Setting Up an Angular Project](#setting-up-an-angular-project)
3. [Core Angular Concepts](#core-angular-concepts)
4. [Components in Angular](#components-in-angular)
5. [Services and Dependency Injection](#services-and-dependency-injection)
6. [Routing in Angular](#routing-in-angular)
7. [API Integration with HTTP Client](#api-integration-with-http-client)
8. [Observables and RxJS](#observables-and-rxjs)
9. [Angular Forms](#angular-forms)
10. [Common Angular CLI Commands](#common-angular-cli-commands)

---

## 1. Introduction to Angular

Angular is a TypeScript-based front-end framework by Google, designed for building scalable, single-page applications (SPAs). With a component-based structure, Angular allows modularity, reusability, and a robust development experience.

## 2. Setting Up an Angular Project

### Install Angular CLI
```bash
npm install -g @angular/cli
# Angular Cheat Sheet and Guide

This README serves as a quick reference guide and cheat sheet for Angular, covering core concepts, API integration, forms, routing, observables, and essential commands for an Angular project.

## Table of Contents
1. Introduction to Angular
2. Setting Up an Angular Project
3. Core Angular Concepts
4. Components in Angular
5. Services and Dependency Injection
6. Routing in Angular
7. API Integration with HTTP Client
8. Observables and RxJS
9. Angular Forms
10. Common Angular CLI Commands

---

## 1. Introduction to Angular

Angular is a TypeScript-based front-end framework by Google, designed for building scalable, single-page applications (SPAs). With a component-based structure, Angular allows modularity, reusability, and a robust development experience.

## 2. Setting Up an Angular Project

Install Angular CLI by running: `npm install -g @angular/cli`

Create a New Project: `ng new project-name`

Run the Application: `ng serve`

## 3. Core Angular Concepts

- **Modules**: Organize the app into cohesive blocks of functionality.
- **Components**: Building blocks of Angular applications, managing view logic.
- **Templates**: Define component views using HTML, directives, and binding.
- **Directives**: Extend HTML with custom behaviors like `*ngIf`, `*ngFor`, etc.
- **Data Binding**: Synchronize data between model and view.
  - **Interpolation**: `{{ value }}`
  - **Property Binding**: `[property]="value"`
  - **Event Binding**: `(event)="function()"`
- **Pipes**: Transform data in the template using `| date`, `| uppercase`, etc.

## 4. Components in Angular

### Creating a Component
Run: `ng generate component component-name`

### Component Structure
Each component consists of:
1. TypeScript file (logic)
2. HTML file (template/view)
3. CSS file (styling)

### Basic Component Example
1. Import `{ Component }` from Angular core.
2. Use `@Component` decorator with `selector`, `templateUrl`, and `styleUrls`.
3. Create a `class ComponentNameComponent` to define component logic.

## 5. Services and Dependency Injection

Services provide shared data and logic across components.

### Creating a Service
Run: `ng generate service service-name`

### Using Dependency Injection in Components
1. Import `ServiceName` from the service file.
2. Inject the service in the component's constructor by using `private serviceName: ServiceName`.

## 6. Routing in Angular

### Setting Up Routes
1. Import `{ RouterModule, Routes }` from `@angular/router`.
2. Define routes using the `Routes` array. Example: `{ path: 'path', component: ComponentName }`.
3. Add `<router-outlet></router-outlet>` in `app.component.html`.

## 7. API Integration with HTTP Client

### Setup HTTP Client
1. Import `HttpClientModule` in `app.module.ts`.
2. Use `HttpClient` in a service to make API calls. Define `getData` and `postData` methods that return an observable for API responses.

### Making API Requests in Components
- Use `this.apiService.getData().subscribe(data => console.log(data))`.
- Use `this.apiService.postData({ key: 'value' }).subscribe(response => console.log(response))`.

## 8. Observables and RxJS

Observables are a key part of Angular's async data handling. They manage async operations like API calls and real-time data streams.

### Example Observable Usage
- Import `Observable` from `rxjs`.
- Return an observable by calling `this.http.get<DataType>(url)`.

### Common RxJS Operators
- **map**: Transform each item
- **filter**: Filter items by condition
- **catchError**: Handle errors in streams

## 9. Angular Forms

Angular supports two types of forms:
1. **Template-driven Forms**: Form controls are defined in the HTML.
2. **Reactive Forms**: Form controls are created and managed in code.

### Template-driven Form Example
Create an HTML form with `#form="ngForm"` and bind `ngModel` for each input.

### Reactive Form Example
1. Import `FormBuilder` and `FormGroup`.
2. Create a form group with fields using `this.fb.group({ username: [''], email: [''] })`.

## 10. Common Angular CLI Commands

- Generate a Component: `ng generate component component-name`
- Generate a Service: `ng generate service service-name`
- Build the Project: `ng build`
- Run Tests: `ng test`

---

Happy coding! 🎉
