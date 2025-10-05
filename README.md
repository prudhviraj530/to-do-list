# to-do-list

Got it 👍 — you want:

1. A **step-by-step explanation** of how to build a **To-Do List project**, and
2. A ready-to-use **README.md** file for your GitHub repository.

Let’s do both 👇

---

## 🧠 How You Can Build a To-Do List Project

### 🏗️ 1. Project Setup

* **Create a new folder** → e.g. `to-do-list`
* Inside it, create three files:

  ```
  index.html
  style.css
  script.js
  ```

### 🧩 2. Build the HTML Structure (`index.html`)

This file contains the layout of the to-do list — a title, input box, add button, and a list area.

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>To-Do List</title>
  <link rel="stylesheet" href="style.css">
</head>
<body>
  <div class="container">
    <h1>My To-Do List</h1>
    <div class="input-section">
      <input type="text" id="taskInput" placeholder="Enter a new task">
      <button id="addBtn">Add</button>
    </div>
    <ul id="taskList"></ul>
  </div>

  <script src="script.js"></script>
</body>
</html>
```

---

### 🎨 3. Style It (`style.css`)

Make it look clean and centered:

```css
body {
  font-family: Arial, sans-serif;
  background: #f7f8fa;
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
}

.container {
  background: white;
  padding: 20px;
  border-radius: 10px;
  box-shadow: 0 0 10px rgba(0,0,0,0.1);
  width: 300px;
}

h1 {
  text-align: center;
}

.input-section {
  display: flex;
  gap: 5px;
}

input {
  flex: 1;
  padding: 5px;
}

button {
  padding: 5px 10px;
  cursor: pointer;
}

ul {
  list-style: none;
  padding: 0;
  margin-top: 10px;
}

li {
  background: #f1f1f1;
  margin-bottom: 5px;
  padding: 8px;
  border-radius: 5px;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

li.completed {
  text-decoration: line-through;
  color: gray;
}
```

---

### ⚙️ 4. Add Functionality (`script.js`)

This adds, removes, and marks tasks as done — and saves them in local storage.

```javascript
const addBtn = document.getElementById('addBtn');
const taskInput = document.getElementById('taskInput');
const taskList = document.getElementById('taskList');

addBtn.addEventListener('click', addTask);
document.addEventListener('DOMContentLoaded', loadTasks);

function addTask() {
  const taskText = taskInput.value.trim();
  if (taskText === '') return;

  const li = document.createElement('li');
  li.textContent = taskText;

  li.addEventListener('click', () => {
    li.classList.toggle('completed');
    saveTasks();
  });

  const delBtn = document.createElement('button');
  delBtn.textContent = '❌';
  delBtn.addEventListener('click', () => {
    li.remove();
    saveTasks();
  });

  li.appendChild(delBtn);
  taskList.appendChild(li);
  taskInput.value = '';
  saveTasks();
}

function saveTasks() {
  const tasks = [];
  document.querySelectorAll('#taskList li').forEach(li => {
    tasks.push({ text: li.firstChild.textContent, completed: li.classList.contains('completed') });
  });
  localStorage.setItem('tasks', JSON.stringify(tasks));
}

function loadTasks() {
  const tasks = JSON.parse(localStorage.getItem('tasks')) || [];
  tasks.forEach(task => {
    const li = document.createElement('li');
    li.textContent = task.text;
    if (task.completed) li.classList.add('completed');

    li.addEventListener('click', () => {
      li.classList.toggle('completed');
      saveTasks();
    });

    const delBtn = document.createElement('button');
    delBtn.textContent = '❌';
    delBtn.addEventListener('click', () => {
      li.remove();
      saveTasks();
    });

    li.appendChild(delBtn);
    taskList.appendChild(li);
  });
}
```

---

