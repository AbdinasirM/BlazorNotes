# Binding Between Blazor Components

Blazor allows seamless communication and data sharing between components. Understanding how to bind data between parent and child components is crucial for building dynamic and interactive applications.

---

## Binding Between Components

In Blazor, you can share data between a **parent component** and a **child component** using parameters and events. This is achieved using the following mechanisms:

1. **Passing Data from Parent to Child**
2. **Raising Events from Child to Parent**
3. **Using `EventCallback` for Two-Way Communication**

---

### 1. Passing Data from Parent to Child

You can pass data to a child component using **parameters**.

#### **Example:**
**Parent Component:**
```razor
<ChildComponent Title="Welcome to Blazor!" />
```

**Child Component (`ChildComponent.razor`):**
```razor
<h3>@Title</h3>

@code {
    [Parameter]
    public string Title { get; set; }
}
```

- **Explanation**:
  - The parent passes the value `"Welcome to Blazor!"` to the child.
  - The child component displays the value using the `Title` property.

---

### 2. Raising Events from Child to Parent

When a child component needs to notify its parent about an action, it can do so by raising an event.

#### **Example:**
**Parent Component:**
```razor
<ChildComponent OnButtonClick="HandleButtonClick" />

<p>Message from Child: @message</p>

@code {
    private string message;

    private void HandleButtonClick(string value)
    {
        message = value;
    }
}
```

**Child Component (`ChildComponent.razor`):**
```razor
<button @onclick="SendMessage">Click Me</button>

@code {
    [Parameter]
    public EventCallback<string> OnButtonClick { get; set; }

    private async Task SendMessage()
    {
        await OnButtonClick.InvokeAsync("Hello from Child Component!");
    }
}
```

- **Explanation**:
  - The child component raises the `OnButtonClick` event when the button is clicked.
  - The parent component handles the event using the `HandleButtonClick` method and updates its UI.

---

### 3. Using `EventCallback` for Two-Way Communication

`EventCallback` is a mechanism in Blazor for passing events and their associated data from a child component to its parent.

#### **Why Use `EventCallback`?**
- It’s type-safe and integrates well with asynchronous programming in Blazor.
- It ensures the parent is notified when the child triggers an action.

#### **Example:**
**Parent Component:**
```razor
<ChildComponent Value="@parentValue" ValueChanged="UpdateValue" />

<p>Parent Value: @parentValue</p>

@code {
    private string parentValue = "Initial Value";

    private void UpdateValue(string newValue)
    {
        parentValue = newValue;
    }
}
```

**Child Component (`ChildComponent.razor`):**
```razor
<input @bind="localValue" />
<button @onclick="NotifyParent">Update Parent</button>

@code {
    private string localValue = "";

    [Parameter]
    public string Value { get; set; }

    [Parameter]
    public EventCallback<string> ValueChanged { get; set; }

    private async Task NotifyParent()
    {
        await ValueChanged.InvokeAsync(localValue);
    }
}
```

- **Explanation**:
  - The parent component passes a value and a callback method (`ValueChanged`) to the child.
  - The child notifies the parent whenever the value changes, updating the parent’s state.

---

## Summary

### Key Concepts:
1. **Binding Between Components**:
   - Use `[Parameter]` to pass data from parent to child.
   - Use `EventCallback` to send events and data from child to parent.

2. **`EventCallback`**:
   - A type-safe way to handle events between components.
   - Supports asynchronous methods using `InvokeAsync`.

### Key Patterns:
- **Parent to Child**: Pass data using `[Parameter]`.
- **Child to Parent**: Notify the parent using `EventCallback`.
