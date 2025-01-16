# Blazor Basics: Router, Routes, Layout, Parameters, and NavLink

---

## Blazor Router and Routes

### What is a Router?
The router in Blazor is responsible for handling navigation between different pages in the application. It determines which component should be displayed based on the current URL.

### What are Routes?
Routes define the URL paths that correspond to specific components. In Blazor, you use the `@page` directive at the top of a component to define its route.

**Example:**
```razor
@page "/home"

<h3>Welcome to the Home Page</h3>
```

### Special Components: `Found` and `NotFound`
Blazor provides `Found` and `NotFound` components to handle scenarios where routes are successfully matched or not.

- **`Found`**: Defines the layout or content to show when a route is successfully matched.
- **`NotFound`**: Defines the content to show when no matching route is found.

**Example:**
```razor
<Router AppAssembly="typeof(Program).Assembly">
    <Found Context="routeData">
        <RouteView RouteData="routeData" DefaultLayout="typeof(MainLayout)" />
    </Found>
    <NotFound>
        <h3>Page Not Found</h3>
    </NotFound>
</Router>
```

### How It Works:
1. **Router**: Checks the current URL.
2. **Found**: Displays the matched component.
3. **NotFound**: Displays a fallback message (e.g., "Page Not Found") if no route matches.

---

## Layouts in Blazor
Layouts in Blazor are reusable templates that define a common structure for your application, such as headers, footers, or navigation menus.

### How to Define a Layout
1. Create a `.razor` file, e.g., `MainLayout.razor`.
2. Use the `@Body` directive to indicate where the page content will be rendered.

**Example:**
```razor
<h1>My Application</h1>

<nav>
    <a href="/">Home</a>
    <a href="/about">About</a>
</nav>

@Body
```

### How to Use a Layout in a Component
Specify the layout in your component using the `@layout` directive.

**Example:**
```razor
@page "/about"
@layout MainLayout

<h3>About Us</h3>
<p>This is the About page.</p>
```

---

## Parameters in Blazor
Parameters allow you to pass data into components. You define parameters in the child component using the `[Parameter]` attribute.

### Example of Passing Parameters
**Parent Component:**
```razor
<ChildComponent Title="Hello World" />
```

**Child Component:**
```razor
<h3>@Title</h3>

@code {
    [Parameter]
    public string Title { get; set; }
}
```

### Explanation of `?` and `??`
1. **`?` (Nullable):** Indicates that a value type can accept `null`.
   - **Example:**
     ```csharp
     int? age = null; // Nullable integer
     ```
2. **`??` (Null Coalescing):** Provides a default value if the left-hand operand is `null`.
   - **Example:**
     ```csharp
     string name = null;
     string displayName = name ?? "Guest"; // Outputs "Guest"
     ```

---

## NavLink in Blazor
The `NavLink` component is used for navigation and automatically applies a CSS class to indicate the active link.

### Example of Using `NavLink`
```razor
<NavLink href="/" class="nav-link" active-class="active">Home</NavLink>
<NavLink href="/about" class="nav-link" active-class="active">About</NavLink>
```

### Explanation:
- **`href`**: The URL the link points to.
- **`class`**: The base CSS class for the link.
- **`active-class`**: The CSS class applied when the link is active (the current page).

---

## Summary
### Key Takeaways:
1. **Router**: Manages navigation in your application.
2. **Routes**: Define URL paths with the `@page` directive.
3. **Found/NotFound**: Handle matched and unmatched routes.
4. **Layouts**: Provide reusable structures for pages.
5. **Parameters**: Pass data between components; use `?` for nullable types and `??` for default values.
6. **NavLink**: Provides navigation with automatic active state styling.
