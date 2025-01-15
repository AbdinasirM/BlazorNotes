# Basic Razor Overview

Razor is a markup syntax used in ASP.NET for creating dynamic web pages with C#. It seamlessly combines HTML and C# code, making it easy to create interactive and data-driven web applications.

## Key Features of Razor
- **Server-Side Code Integration**: Razor allows embedding C# code directly within HTML.
- **Clean Syntax**: Simple and intuitive syntax for switching between HTML and C#.
- **Code Reusability**: Supports reusable components and layouts.
- **Model Binding**: Easily bind data models to the UI.

## Razor Syntax Basics

### Inline C# Code
Use `@` to switch from HTML to C# within a Razor file.
```html
<p>The current year is @DateTime.Now.Year</p>
```
This will render as:
```html
<p>The current year is 2025</p>
```

### Code Blocks
Use `@code` or `@{}` to define larger blocks of C# code.
```html
@{
    var message = "Hello, Razor!";
}
<p>@message</p>
```
Output:
```html
<p>Hello, Razor!</p>
```

### Conditional Statements
Razor supports standard C# control structures like `if`, `else`, and `switch`.
```html
@{
    var isAuthenticated = true;
}
@if (isAuthenticated)
{
    <p>Welcome, user!</p>
}
else
{
    <p>Please log in.</p>
}
```

### Loops
You can use loops to generate repetitive HTML.
```html
@for (int i = 1; i <= 5; i++)
{
    <p>Item @i</p>
}
```
Output:
```html
<p>Item 1</p>
<p>Item 2</p>
<p>Item 3</p>
<p>Item 4</p>
<p>Item 5</p>
```

### Using Models
Razor pages can use models to bind data to the UI.
```csharp
@model YourNamespace.Models.Product
<h2>Product Details</h2>
<p>Name: @Model.Name</p>
<p>Price: $@Model.Price</p>
```

### Partial Views
Partial views allow you to reuse UI components across pages.
```html
@await Html.PartialAsync("_Header")
```
This will include the `_Header.cshtml` partial view.

## Example Razor Page
Below is a full example of a Razor page:
```html
@page ""
@model RazorPagesExample.Pages.IndexModel

<h1>Welcome to Razor!</h1>

@{
    var today = DateTime.Now;
}
<p>Today is @today.ToString("dddd, MMMM dd, yyyy")</p>

@if (Model.Products.Any())
{
    <ul>
    @foreach (var product in Model.Products)
    {
        <li>@product.Name - $@product.Price</li>
    }
    </ul>
}
else
{
    <p>No products available.</p>
}
```

## Notes
- Razor files have a `.cshtml` extension.
- Razor integrates seamlessly with ASP.NET, making it a powerful tool for dynamic web development.
- Razor pages support layouts for consistent structure across multiple pages.
