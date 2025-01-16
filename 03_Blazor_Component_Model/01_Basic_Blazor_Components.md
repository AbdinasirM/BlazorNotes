# Blazor Components
---

## What Are Blazor Components?
Blazor components are like small, reusable building blocks that make up your Blazor application. Each component has its own UI and logic, which helps you create clean and modular code. Typically, components are located in the **`Pages`** folder of your project. However, shared components, like headers or menus, are often placed in the **`Shared`** folder.

### Key Characteristics of Components:
1. **Reusable**: You can use components across multiple pages.
2. **Modular**: Encapsulate UI and logic in a single file.
3. **Dynamic**: Handle data changes and user interactions efficiently.

---

## Key Concepts and Features

### 1. **Creating a Component**
To create a new component in Blazor, follow these steps:

1. Create a new `.razor` file, for example, `MyComponent.razor`.
2. Add a route to the top of the file using the `@page` directive.
3. Define HTML and C# code for your component.

**Real-Life Example:**
Imagine you are creating a page to display a "Contact Us" form.

**Code Example:**
```razor
@page "/contact-us"

<h3>Contact Us</h3>

<form>
    <label for="name">Name:</label>
    <input id="name" type="text" />

    <label for="email">Email:</label>
    <input id="email" type="email" />

    <button type="submit">Submit</button>
</form>
```

**Explanation:**
- **`@page`**: Defines the URL route for the component (`/contact-us`).
- **HTML Structure**: Contains form fields for user input.

---

### 2. **Data Services and Dependency Injection (DI)**

#### What Are Data Services?
Data services handle operations like fetching or saving data from/to a database or API. They are used to separate business logic from UI code, making applications cleaner and easier to maintain.

#### Using Dependency Injection
Blazor uses DI to provide components with required services. You must register the service in `Program.cs` and inject it into your component.

**Real-Life Example:**
A weather app fetching data from an API.

#### Registering a Service
Register the service in the `Program.cs` file:

**Code Example:**
```csharp
// Registering the service in Program.cs
builder.Services.AddScoped<WeatherService>();
```

#### Using a Service in a Component
Inject the service into your component:

**Code Example:**
```razor
@inject WeatherService WeatherService

<h3>Weather Information</h3>

<p>Current Temperature: @temperature°C</p>

@code {
    private string temperature;

    protected override async Task OnInitializedAsync()
    {
        temperature = await WeatherService.GetCurrentTemperatureAsync();
    }
}
```

**Explanation:**
- **`@inject`**: Injects the `WeatherService` into the component.
- **Real-Life Use:** Fetching and displaying live weather data.

---

### 3. **Async Programming in Blazor**
Blazor handles asynchronous operations, like data fetching, using `async` and `await`. Lifecycle methods such as `OnInitializedAsync` are designed to handle these operations.

**Real-Life Example:**
A dashboard loading user data on initialization.

**Code Example:**
```razor
<h3>@message</h3>

@code {
    private string message = "Loading user data...";

    protected override async Task OnInitializedAsync()
    {
        await Task.Delay(3000); // Simulate a delay
        message = "Welcome, John Doe!";
    }
}
```

**Explanation:**
- **Delay Simulation:** Simulates fetching data.
- **Lifecycle Method:** Ensures logic runs when the component initializes.

---

### 4. **Shared Components**
Shared components are reusable pieces of UI used across the application. For example, navigation menus, headers, or footers. Shared components are typically stored in the **`Shared`** folder.

#### Example of a Shared Component
**Real-Life Example:**
A navigation menu consistent across all pages.

**Code Example:**
**File:** `NavMenu.razor`
```razor
<nav>
    <ul>
        <li><a href="/">Home</a></li>
        <li><a href="/about">About</a></li>
        <li><a href="/contact-us">Contact Us</a></li>
    </ul>
</nav>
```

Use this shared component in other components by referencing it:
```razor
<NavMenu />
```

**Explanation:**
- **Centralized UI:** Write the menu once, use it everywhere.
- **Reusable:** Eliminates duplication.

---

### 5. **JavaScript Interop (JS Interop)**
Blazor enables calling JavaScript functions from C# and vice versa. This is helpful for integrating JavaScript libraries or using browser APIs.

#### Calling JavaScript from Blazor
To call a JavaScript function, use the `IJSRuntime` service.

**Real-Life Example:**
Show a browser alert when a button is clicked.

**Code Example:**
```razor
@inject IJSRuntime JS

<button @onclick="ShowAlert">Show Alert</button>

@code {
    private async Task ShowAlert()
    {
        await JS.InvokeVoidAsync("alert", "This is a JavaScript alert!");
    }
}
```

#### Calling C# from JavaScript
To call C# methods from JavaScript, use the `DotNetObjectReference` class.

**Explanation:**
- **JS Integration:** Combine Blazor with existing JavaScript libraries.
- **Real-Life Use:** Adding interactivity or animations.

---


### 6. **Passing Parameters to Components**
Components can receive parameters from their parent components.

**Real-Life Example:**
A reusable button component that accepts a label.

**Code Example:**
**File:** `ButtonComponent.razor`
```razor
<button>@Label</button>

@code {
    [Parameter]
    public string Label { get; set; }
}
```

**Usage:**
```razor
<ButtonComponent Label="Click Me" />
```

**Explanation:**
- **`[Parameter]` Attribute:** Allows the parent to pass data.
- **Reusable Components:** Create flexible components for different scenarios.

### 7. **Event Handling**
Blazor components can handle events like button clicks or form submissions.

**Real-Life Example:**
A login form handling a submit event.

**Code Example:**
```razor
<form @onsubmit="HandleSubmit">
    <input type="text" @bind="username" placeholder="Username" />
    <button type="submit">Login</button>
</form>

@code {
    private string username;

    private void HandleSubmit()
    {
        Console.WriteLine($"Logging in as {username}");
    }
}
```

**Explanation:**
- **Event Binding:** Connect UI events to C# methods.
- **`@onsubmit` Event:** Captures form submissions.

---

## Summary
### Key Points
- **Components:** Reusable blocks of UI and logic in `.razor` files.
- **Data Services:** Encapsulate data logic, injected into components using DI.
- **Async Programming:** Handle long-running tasks with `async` and `await`.
- **Shared Components:** Store reusable components in the `Shared` folder.
- **JavaScript Interop:** Enables communication between Blazor and JavaScript.
- **Parameters and Events:** Pass data to components and handle user interactions.


