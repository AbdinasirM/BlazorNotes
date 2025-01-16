# Blazor Layouts

Blazor Layouts allow you to define a consistent structure for your application, such as headers, navigation menus, and footers, which can be reused across multiple pages. Layouts are a key feature to create a uniform look and feel for your application.

---

## Key Concepts

### 1. **`@inherits LayoutComponentBase`**
- A layout in Blazor is a component that inherits from the base class **`LayoutComponentBase`**.
- This class provides the structure and functionality required to render the content of pages within the layout.

---

### 2. **`@layout` Directive**
- The **`@layout`** directive is used to specify which layout a page or component should use.
- You can define the layout for:
  - Individual pages.
  - All pages in a specific folder.
  - All pages in the application (via `_Imports.razor`).

---

### 3. **`@Body`**
- The **`@Body`** directive is used within the layout to specify where the content of a page should be rendered.
- This is the placeholder for the content of the routed page.

---

## Example: Using Blazor Layouts

### Step 1: Create a Layout Component

Create a new layout file, for example, `MainLayout.razor`:

```razor
@inherits LayoutComponentBase

<div class="main-layout">
    <header>
        <h1>My Application</h1>
    </header>

    <nav>
        <ul>
            <li><a href="/">Home</a></li>
            <li><a href="/about">About</a></li>
        </ul>
    </nav>

    <main>
        @Body
    </main>

    <footer>
        <p>&copy; 2025 My Application</p>
    </footer>
</div>
```

- **`@inherits LayoutComponentBase`**: Specifies that this is a layout component.
- **`@Body`**: Placeholder for the content of the routed page.

---

### Step 2: Assign the Layout to a Page

In a page component (e.g., `Index.razor`):

```razor
@page "/"
@layout MainLayout

<h2>Welcome to My Application</h2>
<p>This is the home page.</p>
```

- **`@layout MainLayout`**: Specifies that the `Index.razor` page uses the `MainLayout` component.

---

### Step 3: Apply a Layout Globally

To set a layout for all pages in a folder or the entire application, use `_Imports.razor`.

**File:** `_Imports.razor`
```razor
@layout MainLayout
```

- Placing this file in the root of the project applies the layout to all pages.

---

## Real-Life Example: Layout with Sidebar Navigation

### Layout Component (`SidebarLayout.razor`)
```razor
@inherits LayoutComponentBase

<div class="sidebar-layout">
    <aside>
        <ul>
            <li><a href="/">Dashboard</a></li>
            <li><a href="/reports">Reports</a></li>
            <li><a href="/settings">Settings</a></li>
        </ul>
    </aside>

    <section>
        @Body
    </section>
</div>
```

### Using the Layout in a Page (`Reports.razor`)
```razor
@page "/reports"
@layout SidebarLayout

<h2>Reports</h2>
<p>Here you can view all the reports.</p>
```

### Output Structure:
```html
<div class="sidebar-layout">
    <aside>
        <ul>
            <li><a href="/">Dashboard</a></li>
            <li><a href="/reports">Reports</a></li>
            <li><a href="/settings">Settings</a></li>
        </ul>
    </aside>

    <section>
        <h2>Reports</h2>
        <p>Here you can view all the reports.</p>
    </section>
</div>
```

---

## Summary

### Key Points:
1. **`@inherits LayoutComponentBase`**:
   - Used to define a layout component.
   - Enables layouts to act as containers for page content.

2. **`@layout` Directive**:
   - Assigns a layout to a page.
   - Can be applied globally using `_Imports.razor`.

3. **`@Body`**:
   - Placeholder for rendering the routed page content within the layout.

### Benefits of Layouts:
- Ensure a consistent look and feel across pages.
- Simplify UI updates by centralizing shared elements like headers and footers.

