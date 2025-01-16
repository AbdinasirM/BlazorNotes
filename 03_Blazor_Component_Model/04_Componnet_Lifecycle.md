# Blazor Component Lifecycle

Blazor components go through a series of lifecycle events from creation to destruction. Understanding these events helps you manage state, parameters, and rendering efficiently.

---

## Component Lifecycle Overview

Blazor components are **created** and **destroyed** regularly. When a top-level component is routed to, it is instantiated along with all its child components. The lifecycle consists of several methods that allow you to hook into key moments of a component’s life.

---

## Lifecycle Methods

### 1. **`SetParametersAsync`**
- **When It Runs**: Called when the component receives parameters.
- **What It Does**: Initializes the component with the parameters passed to it.
- **Key Use Case**: Handle parameter values before rendering.

**Example:**
```razor
@code {
    [Parameter]
    public string Title { get; set; }

    public override async Task SetParametersAsync(ParameterView parameters)
    {
        await base.SetParametersAsync(parameters);
        Console.WriteLine($"Parameter Title: {Title}");
    }
}
```

---

### 2. **`OnInitialized` and `OnInitializedAsync`**
- **When It Runs**: Called once when the component is created.
- **What It Does**: Used to initialize the component, such as setting default values or making initial API calls.
- **Key Use Case**: Setup data or configuration for the component.

**Example:**
```razor
@code {
    private string message;

    protected override void OnInitialized()
    {
        message = "Component Initialized!";
    }
}
```

**Async Version:**
```razor
@code {
    private string data;

    protected override async Task OnInitializedAsync()
    {
        data = await GetDataAsync();
    }

    private Task<string> GetDataAsync() => Task.FromResult("Async Data Loaded!");
}
```

---

### 3. **`OnParametersSet` and `OnParametersSetAsync`**
- **When It Runs**: Invoked when the parameters are set or updated.
- **What It Does**: Confirms that parameters are ready and allows you to respond to changes.
- **Key Use Case**: Handle parameter updates and trigger side effects if necessary.

**Example:**
```razor
@code {
    [Parameter]
    public string Username { get; set; }

    protected override void OnParametersSet()
    {
        Console.WriteLine($"Parameters set: Username = {Username}");
    }
}
```

---

### 4. **`ShouldRender`**
- **When It Runs**: Called before rendering.
- **What It Does**: Determines if the component should re-render.
- **Key Use Case**: Optimize rendering by returning `false` when no updates are needed.

**Example:**
```razor
@code {
    private bool shouldRender = true;

    protected override bool ShouldRender()
    {
        return shouldRender;
    }

    public void PreventReRender()
    {
        shouldRender = false;
    }
}
```

---

### 5. **`OnAfterRender` and `OnAfterRenderAsync`**
- **When It Runs**: Called after the component’s HTML has been rendered.
- **What It Does**: Perform actions that depend on the rendered DOM.
- **Key Use Case**: Interact with JavaScript or trigger animations.

**Example:**
```razor
@inject IJSRuntime JS

protected override async Task OnAfterRenderAsync(bool firstRender)
{
    if (firstRender)
    {
        await JS.InvokeVoidAsync("console.log", "Component rendered for the first time!");
    }
}
```

---

### 6. **`IDisposable`**
- **When It Runs**: When the component is about to be removed and garbage collected.
- **What It Does**: Clean up resources like event handlers or streams.
- **Key Use Case**: Free unmanaged resources to avoid memory leaks.

**Example:**
```razor
@implements IDisposable

@code {
    private Timer timer;

    protected override void OnInitialized()
    {
        timer = new Timer(_ => Console.WriteLine("Timer tick"), null, 0, 1000);
    }

    public void Dispose()
    {
        timer?.Dispose();
        Console.WriteLine("Component disposed!");
    }
}
```

---

## Key Points to Remember

1. **One-Time for the Life of the Component:**
   - **`OnInitialized(Async)`**: Runs only once when the component is created.
   - **`SetParametersAsync`**: Sets parameters only when the component is instantiated or updated.

2. **Lifecycle Recap:**
   - **Create:** `OnInitialized(Async)`, `SetParametersAsync`.
   - **Render:** `ShouldRender`, `OnAfterRender(Async)`.
   - **Destroy:** `IDisposable`.

3. **Top-Level Components:**
   - When routed to, the top-level component is created, and all its child components are instantiated as well.

---

## Summary Table

| Method                  | Description                                  | Runs When                                        | Common Use Case                                    |
|-------------------------|----------------------------------------------|-------------------------------------------------|--------------------------------------------------|
| `SetParametersAsync`    | Initializes parameters                      | Component receives parameters                   | Initialize or validate input parameters          |
| `OnInitialized(Async)`  | Initializes the component                   | Component is created                            | Fetch data or set default values                 |
| `OnParametersSet(Async)`| Parameters are updated                      | Parameters change                               | Handle parameter changes                         |
| `ShouldRender`          | Decides if the component should re-render   | Before every render                             | Optimize rendering performance                   |
| `OnAfterRender(Async)`  | Actions after rendering to HTML             | After the DOM is updated                        | JavaScript calls or DOM-dependent logic          |
| `IDisposable`           | Cleanup resources before garbage collection | Component is removed                            | Free unmanaged resources                         |

