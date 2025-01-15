# Getting Started with Blazor WebAssembly

Blazor WebAssembly is a framework for building interactive web applications using C# that run entirely in the browser. It uses WebAssembly to execute C# code directly on the client-side, making it standalone and efficient for creating modern web apps.

## Prerequisites
To start with Blazor WebAssembly, ensure you have the following tools installed:

- **.NET SDK**: Required to create and build Blazor applications.
- **Visual Studio** or **Visual Studio Code**: Recommended for writing and managing your code.

## Steps to Create a Blazor WebAssembly Project

### 1. Create a New Project
To create a Blazor WebAssembly project, run the following command in your terminal:
```bash
dotnet new blazorwasm -o Helloworld
```
This command generates a new Blazor WebAssembly project in a directory named `Helloworld`.

### 2. Navigate to the Project Directory
Move into the newly created project directory:
```bash
cd .\Helloworld\
```

### 3. Run the Project
Start the application by running the following command:
```bash
dotnet run
```
Once the application starts, open your browser and navigate to `http://localhost:5000` to see your Blazor WebAssembly app in action.

## Examples
Here is an example of a simple counter component in Blazor WebAssembly:

```csharp
@page "/counter"

<h3>Counter</h3>

<p>Current count: @currentCount</p>

<button @onclick="IncrementCount">Click me</button>

@code {
    private int currentCount = 0;

    private void IncrementCount()
    {
        currentCount++;
    }
}
```
In this example, clicking the button increases the `currentCount` value and updates the display instantly.

## Notes
- Blazor WebAssembly applications work offline if configured as Progressive Web Apps (PWAs).
- The initial load time may be larger since the framework and application files are downloaded to the browser.


