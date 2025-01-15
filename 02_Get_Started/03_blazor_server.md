# Blazor Server Overview

Blazor Server is a hosting model for Blazor applications where the application logic runs on the server. The client and server maintain an open connection using SignalR, enabling fast two-way communication.

## Key Concepts

### SignalR
- **What is SignalR?**
  SignalR is a library that establishes and maintains a persistent connection between the client and server, allowing for real-time two-way communication.

### Application State
In a Blazor Server application, the entire application state is managed on the server, including:
- **HTML DOM**: The Document Object Model of the web page.
- **Data and Memory**: All application data and memory are stored server-side.
- **Services**: Any injected services are available in the server context.
- **Application Instance**: The running instance of the application is maintained on the server.

In contrast, Blazor WebAssembly stores the state in the client’s memory.

### Circuits in Blazor Server
A **circuit** represents the connection between a Blazor Server application and the client. Each user session maintains its own circuit to track state and interactions.

## Features of Blazor Server

### Pros
- **Small Initial Download**: Minimal resources are downloaded to the client, making initial page load times fast.
- **Server-Side Processing**: All logic executes on the server, so no application code is exposed to the client.
- **Efficient DOM Updates**: Only differential changes between the current DOM and the new DOM are sent to the client, optimizing bandwidth usage.

### Cons
- **Constant Server Connection**: Requires a stable, constant network connection. Poor network quality directly impacts user experience.
- **No Offline Support**: Applications cannot run offline as they depend on the server for all logic and state management.
- **Scalability**: High user volumes demand careful server resource planning since every connected client consumes server memory and processing power.
- **Switching Hosting Models**: While switching between Blazor Server and WebAssembly is possible, it’s not recommended due to architectural differences.

## Host File
In Blazor Server applications, the entry point is `_Host.html` (instead of `index.html` in Blazor WebAssembly). This file defines the root layout for the application and initializes the server-side Blazor environment.

### Example `_Host.html`:
```html
<!DOCTYPE html>
<html>
<head>
    <title>Blazor Server App</title>
    <base href="/">
    <link href="css/app.css" rel="stylesheet">
</head>
<body>
    <app>
        Loading...
    </app>
    <script src="_framework/blazor.server.js"></script>
</body>
</html>
```

## How DOM Updates Work
Blazor Server only sends updates for parts of the DOM that have changed. This is achieved through a **diffing algorithm** that compares the current DOM state with the desired new state, ensuring only the minimal changes are sent to the client.

### Example
Consider a button click that increments a counter. The server computes the new value and sends only the updated portion of the DOM (e.g., the new counter value) to the client.

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

When `IncrementCount` is triggered, only the updated `@currentCount` is sent to the client.

## Notes
- **Scalability**: Scaling to a large number of users requires careful planning, such as load balancing and optimizing server resources.
- **No Application Code on Client**: This ensures better security since no application logic is exposed to the client.
- **Network Dependency**: The quality of the user experience depends heavily on network stability.

