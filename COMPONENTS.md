# Component reference

### Layout

```html
<div class="wf-screen">   <!-- full-screen column container -->
<div class="wf-centered"> <!-- vertically + horizontally centered -->
<div class="wf-row">      <!-- horizontal flex row, gap: 12px -->
<div class="wf-col">      <!-- vertical flex column, gap: 12px -->
<div class="wf-layout">   <!-- side-by-side (sidebar + main) -->
<div class="wf-spacer">   <!-- flex spacer — pushes siblings apart -->
<div class="wf-grid cols-3"> <!-- 3-column grid. also: cols-2, cols-4 -->
```

### App shell

```html
<nav class="wf-nav">
  <span class="logo">APP</span>
  <span class="nav-link">Home</span>
  <span class="nav-link active">Dashboard</span>
  <div class="wf-spacer"></div>
  <div class="wf-avatar">IO</div>
</nav>

<div class="wf-layout">
  <aside class="wf-sidebar">             <!-- also: .wide, .narrow -->
    <div class="sidebar-section">Menu</div>
    <div class="sidebar-item active">Dashboard</div>
    <div class="sidebar-item">Settings</div>
  </aside>
  <main class="wf-main">
    <!-- content -->
  </main>
</div>
```

### Cards & panels

```html
<div class="wf-card">                    <!-- also: .compact -->
  <div class="wf-card-title">Title</div>
  <div class="wf-card-meta">metadata</div>
  <p class="wf-text">Body content here.</p>
  <div class="wf-card-footer">Footer</div>
</div>

<div class="wf-panel">
  <div class="wf-panel-header">
    <div class="wf-h3">Panel title</div>
    <button class="wf-btn sm">Action</button>
  </div>
  <!-- panel body -->
</div>

<!-- Stat card -->
<div class="wf-stat">
  <div class="stat-value">2,481</div>
  <div class="stat-label">Active users</div>
  <div class="stat-delta up">↑ 12% this week</div>
</div>
```

### Forms

```html
<div class="wf-field">
  <label class="wf-label">Email</label>
  <input class="wf-input" type="text" placeholder="you@example.com" />
  <span class="wf-field-error">Required field</span>
</div>

<div class="wf-field">
  <label class="wf-label">Message</label>
  <textarea class="wf-textarea" placeholder="Write something..."></textarea>
</div>

<!-- Input sizes -->
<input class="wf-input large" type="text" placeholder="Large input" />

<!-- Select -->
<select class="wf-select"><option>Option A</option></select>

<!-- Checkbox -->
<div class="wf-checkbox checked">
  <div class="box">✓</div>
  <span>Remember me</span>
</div>

<!-- Radio -->
<div class="wf-radio selected">
  <div class="dot"></div>
  <span>Option A</span>
</div>

<!-- Toggle -->
<div class="wf-toggle on">
  <div class="track"></div>
  <span>Enabled</span>
</div>
```

### Search

```html
<div class="wf-searchbar" style="width: 480px">
  <input type="text" placeholder="Search..." />
  <span class="search-icon">⌕</span>
</div>
```

### Buttons

```html
<button class="wf-btn">Default</button>
<button class="wf-btn primary">Primary</button>
<button class="wf-btn secondary">Secondary</button>
<button class="wf-btn ghost">Ghost</button>
<button class="wf-btn danger">Danger</button>
<button class="wf-btn sm">Small</button>
<button class="wf-btn lg">Large</button>
<button class="wf-btn full">Full width</button>

<!-- Button group -->
<div class="wf-btn-group">
  <button class="wf-btn">Day</button>
  <button class="wf-btn primary">Week</button>
  <button class="wf-btn">Month</button>
</div>
```

### Badges & labels

```html
<span class="wf-badge">Default</span>
<span class="wf-badge dark">Dark</span>
<span class="wf-badge outline">Outline</span>
<span class="wf-badge pill dot">Active</span>

<span class="wf-label">Section label</span>
<span class="wf-code">variable_name</span>
<span class="wf-annotation">This area handles auth</span>
```

### Tables

```html
<table class="wf-table">               <!-- also: .compact -->
  <thead>
    <tr><th>ID</th><th>Name</th><th>Status</th></tr>
  </thead>
  <tbody>
    <tr>
      <td>001</td>
      <td>Task name</td>
      <td><span class="wf-badge dark">Done</span></td>
    </tr>
  </tbody>
</table>
```

### Navigation patterns

```html
<!-- Tabs -->
<div class="wf-tabs">
  <div class="wf-tab-bar">
    <div class="tab active">Overview</div>
    <div class="tab">Activity</div>
    <div class="tab">Settings</div>
  </div>
  <div class="wf-tab-content">
    <!-- active tab content -->
  </div>
</div>

<!-- Breadcrumb -->
<div class="wf-breadcrumb">
  <span class="crumb">Home</span>
  <span class="sep">/</span>
  <span class="crumb">Projects</span>
  <span class="sep">/</span>
  <span class="crumb current">Sprint 1</span>
</div>

<!-- Pagination -->
<div class="wf-pagination">
  <div class="page disabled">←</div>
  <div class="page active">1</div>
  <div class="page">2</div>
  <div class="page">3</div>
  <div class="page">→</div>
</div>
```

### Feedback & status

```html
<!-- Alert -->
<div class="wf-alert info">            <!-- also: .warning, .error, .success -->
  <span class="alert-icon">ℹ</span>
  <div class="alert-body">
    <div class="alert-title">Heads up</div>
    <div class="alert-text">This action cannot be undone.</div>
  </div>
</div>

<!-- Progress bar -->
<div class="wf-progress">
  <div class="progress-label"><span>Progress</span><span>68%</span></div>
  <div class="track"><div class="fill" style="width: 68%"></div></div>
</div>

<!-- Stepper -->
<div class="wf-stepper">
  <div class="step done">
    <div class="step-circle">✓</div>
    <div class="step-label"><div class="step-title">Details</div></div>
  </div>
  <div class="step-line"></div>
  <div class="step active">
    <div class="step-circle">2</div>
    <div class="step-label"><div class="step-title">Review</div></div>
  </div>
  <div class="step-line pending"></div>
  <div class="step">
    <div class="step-circle">3</div>
    <div class="step-label"><div class="step-title">Confirm</div></div>
  </div>
</div>

<!-- Toast -->
<div class="wf-toast dark">✓ Changes saved</div>

<!-- Empty state -->
<div class="wf-empty">
  <div class="empty-icon">□</div>
  <div class="empty-title">No results found</div>
  <div class="empty-text">Try adjusting your search or filters.</div>
  <button class="wf-btn primary sm">Create one</button>
</div>
```

### Kanban board

```html
<div class="wf-kanban">
  <div class="wf-kanban-col">
    <div class="col-header">To Do <span class="wf-badge sm">3</span></div>
    <div class="col-body">
      <div class="wf-kanban-card">
        <div class="card-id">ISM-12</div>
        <div>Add search endpoint</div>
        <div class="wf-avatar sm">A</div>
      </div>
    </div>
  </div>
  <div class="wf-kanban-col">
    <div class="col-header">In Progress</div>
    <div class="col-body"></div>
  </div>
  <div class="wf-kanban-col">
    <div class="col-header">Done</div>
    <div class="col-body"></div>
  </div>
</div>
```

### Timeline

```html
<div class="wf-timeline">
  <div class="wf-timeline-item">
    <div class="wf-timeline-dot filled"></div>
    <div class="wf-timeline-body">
      <div class="wf-timeline-title">Ticket created</div>
      <div class="wf-timeline-time">2 hours ago</div>
      <div class="wf-timeline-text">ISM-14 assigned to developer agent.</div>
    </div>
  </div>
  <div class="wf-timeline-item">
    <div class="wf-timeline-dot"></div>
    <div class="wf-timeline-body">
      <div class="wf-timeline-title">Review pending</div>
      <div class="wf-timeline-time">just now</div>
    </div>
  </div>
</div>
```

### Modal

```html
<div class="wf-modal-backdrop">
  <div class="wf-modal">
    <div class="wf-modal-header">
      <div class="wf-modal-title">Confirm action</div>
      <span class="wf-modal-close">✕</span>
    </div>
    <div class="wf-modal-body">
      <p class="wf-text">Are you sure you want to delete this item?</p>
    </div>
    <div class="wf-modal-footer">
      <button class="wf-btn secondary">Cancel</button>
      <button class="wf-btn primary">Confirm</button>
    </div>
  </div>
</div>
```

### Media & avatars

```html
<div class="wf-img" style="width: 400px; min-height: 200px"><span>[ hero image ]</span></div>
<div class="wf-video" style="width: 400px; min-height: 220px">▶</div>

<div class="wf-avatar">IO</div>             <!-- default 36px -->
<div class="wf-avatar sm">A</div>           <!-- 24px -->
<div class="wf-avatar lg">IO</div>          <!-- 48px -->
<div class="wf-avatar xl square">IO</div>   <!-- 64px square -->

<div class="wf-avatar-group">
  <div class="wf-avatar sm">A</div>
  <div class="wf-avatar sm">B</div>
  <div class="wf-avatar sm">+3</div>
</div>
```
