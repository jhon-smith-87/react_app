# react_app
## multi level grid react code

Here’s a React implementation for your described custom expandable table grid without using any external libraries, just plain React + CSS.


---

✅ Features Implemented:

Level 1 rows (click to expand)

Level 2 rows nested inside Level 1

Click on a Level 2 row → collapse everything into a left sidebar and show a new dummy panel/grid on the right



---

💻 Prompt for Office VSCode with Copilot:

Use this prompt in your office laptop with GitHub Copilot enabled (not ChatGPT):

Create a React component with nested expandable rows. The top-level grid shows Level 1 records. When a Level 1 record is clicked, it expands to show Level 2 records in the same layout. When a Level 2 record is clicked, the entire grid collapses into a left sidebar (showing only hierarchy), and a new panel opens on the right showing a dummy component (like detail grid). Do not use any UI libraries, only plain CSS and JSX. Make the layout responsive and structured with Flexbox.


---

✅ React Code Example
```
// CustomExpandableGrid.jsx
import React, { useState } from 'react';
import './CustomExpandableGrid.css';

const data = [
  {
    id: 'L1-1',
    name: 'Model Development Plan',
    children: [
      { id: 'L2-1', name: '2LoD Review' },
      { id: 'L2-2', name: '1LoD Review' },
      { id: 'L2-3', name: 'Model Development Plan submission' },
    ],
  },
  {
    id: 'L1-2',
    name: 'Model Monitoring Plan',
    children: [],
  },
  {
    id: 'L1-3',
    name: 'Model Tiering Assessment',
    children: [],
  },
];

const CustomExpandableGrid = () => {
  const [expandedL1, setExpandedL1] = useState(null);
  const [selectedL2, setSelectedL2] = useState(null);

  const handleL1Click = (id) => {
    setExpandedL1(expandedL1 === id ? null : id);
    setSelectedL2(null); // reset detail view if L1 is toggled
  };

  const handleL2Click = (record) => {
    setSelectedL2(record);
  };

  const renderSidebar = () => (
    <div className="sidebar">
      {data.map((item) => (
        <div key={item.id}>
          <div
            className={`row l1 ${expandedL1 === item.id ? 'active' : ''}`}
            onClick={() => handleL1Click(item.id)}
          >
            {item.name}
          </div>
          {expandedL1 === item.id &&
            item.children.map((child) => (
              <div
                key={child.id}
                className={`row l2 ${selectedL2?.id === child.id ? 'selected' : ''}`}
                onClick={() => handleL2Click(child)}
              >
                └ {child.name}
              </div>
            ))}
        </div>
      ))}
    </div>
  );

  return (
    <div className="container">
      {renderSidebar()}
      {selectedL2 && (
        <div className="right-panel">
          <h3>Details for: {selectedL2.name}</h3>
          <p>This is dummy content for the selected level 2 item.</p>
        </div>
      )}
    </div>
  );
};

export default CustomExpandableGrid;
```

---

✅ CSS for Styling
```
/* CustomExpandableGrid.css */
.container {
  display: flex;
  width: 100%;
  height: 100vh;
  font-family: Arial, sans-serif;
}

.sidebar {
  width: 100%;
  max-width: 400px;
  min-width: 250px;
  background: #f4f4f4;
  border-right: 1px solid #ccc;
  padding: 10px;
}

.right-panel {
  flex: 1;
  padding: 20px;
  background-color: #fff;
}

.row {
  padding: 8px 12px;
  border-bottom: 1px solid #ddd;
  cursor: pointer;
  transition: background 0.2s ease;
}

.row:hover {
  background-color: #eee;
}

.l1 {
  font-weight: bold;
  background-color: #e0e0e0;
}

.l2 {
  padding-left: 24px;
  font-style: italic;
}

.active {
  background-color: #d1d1f1;
}

.selected {
  background-color: #c8e6c9;
}
```

---

📝 How to Use:

1. Save the above React code in a file like CustomExpandableGrid.jsx.


2. Save the CSS as CustomExpandableGrid.css in the same folder.


3. Import and render <CustomExpandableGrid /> in your app.




---

Would you like me to:

Add support for dynamic data fetching?

Convert it to TypeScript?

Or add a back button when a Level 2 item is opened?


Let me know and I’ll extend it.


