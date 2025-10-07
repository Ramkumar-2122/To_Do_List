# Ex03 To-Do List using JavaScript
## Date:
07-10-2025
## AIM
To create a To-do Application with all features using JavaScript.

## ALGORITHM
### STEP 1
Build the HTML structure (index.html).

### STEP 2
Style the App (style.css).

### STEP 3
Plan the features the To-Do App should have.

### STEP 4
Create a To-do application using Javascript.

### STEP 5
Add functionalities.

### STEP 6
Test the App.

### STEP 7
Open the HTML file in a browser to check layout and functionality.

### STEP 8
Fix styling issues and refine content placement.

### STEP 9
Deploy the website.

### STEP 10
Upload to GitHub Pages for free hosting.

## PROGRAM
```
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Smart To-Do List</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background: var(--bg, #f5f5f5);
      color: var(--text, #222);
      margin: 0;
      padding: 0;
      display: flex;
      justify-content: center;
    }
    .container {
      width: 90%;
      max-width: 600px;
      margin: 20px auto;
      padding: 20px;
      background: var(--card, #fff);
      border-radius: 12px;
      box-shadow: 0 4px 10px rgba(0,0,0,0.1);
    }
    h1 {
      text-align: center;
    }
    .controls {
      display: flex;
      gap: 5px;
      flex-wrap: wrap;
    }
    input, select, button {
      padding: 10px;
      border-radius: 8px;
      border: 1px solid #ccc;
      flex: 1;
    }
    button {
      background: #007bff;
      color: white;
      cursor: pointer;
    }
    button:hover { background: #0056b3; }
    ul { list-style: none; padding: 0; }
    li {
      background: var(--item, #fafafa);
      margin: 8px 0;
      padding: 10px;
      border-radius: 8px;
      display: flex;
      justify-content: space-between;
      align-items: center;
    }
    li.completed span { text-decoration: line-through; color: gray; }
    .progress {
      margin: 15px 0;
      background: #e0e0e0;
      border-radius: 8px;
      overflow: hidden;
      height: 15px;
    }
    .progress-bar {
      height: 100%;
      background: #28a745;
      width: 0%;
      transition: width 0.3s;
    }
    .dark {
      --bg: #1e1e1e;
      --text: #eee;
      --card: #2a2a2a;
      --item: #333;
    }
  </style>
</head>
<body>
  <div class="container">
    <h1>✨ Smart To-Do List</h1>
    <div class="controls">
      <input type="text" id="taskInput" placeholder="Enter new task">
      <input type="date" id="dueDate">
      <select id="priority">
        <option value="Low">Low</option>
        <option value="Medium" selected>Medium</option>
        <option value="High">High</option>
      </select>
      <button onclick="addTask()">Add</button>
    </div>
    <div class="controls">
      <input type="text" id="search" placeholder="Search tasks" oninput="renderTasks()">
      <select id="filter" onchange="renderTasks()">
        <option value="all">All</option>
        <option value="completed">Completed</option>
        <option value="pending">Pending</option>
        <option value="high">High Priority</option>
      </select>
      <button onclick="toggleTheme()">🌙/☀️</button>
    </div>

    <div class="progress"><div class="progress-bar" id="progressBar"></div></div>
    <ul id="taskList"></ul>
  </div>

  <script>
    let tasks = JSON.parse(localStorage.getItem("tasks")) || [];
    let darkMode = false;

    function addTask() {
      const taskInput = document.getElementById("taskInput");
      const dueDate = document.getElementById("dueDate").value;
      const priority = document.getElementById("priority").value;

      if (taskInput.value.trim() === "") return alert("Enter a task!");

      tasks.push({
        text: taskInput.value,
        dueDate,
        priority,
        completed: false
      });
      taskInput.value = "";
      saveTasks();
      renderTasks();
    }

    function toggleComplete(index) {
      tasks[index].completed = !tasks[index].completed;
      saveTasks();
      renderTasks();
    }

    function deleteTask(index) {
      tasks.splice(index, 1);
      saveTasks();
      renderTasks();
    }

    function editTask(index) {
      const newText = prompt("Edit task:", tasks[index].text);
      if (newText) tasks[index].text = newText;
      saveTasks();
      renderTasks();
    }

    function renderTasks() {
      const list = document.getElementById("taskList");
      list.innerHTML = "";
      const search = document.getElementById("search").value.toLowerCase();
      const filter = document.getElementById("filter").value;

      let filtered = tasks.filter(t =>
        t.text.toLowerCase().includes(search)
      );
      if (filter === "completed") filtered = filtered.filter(t => t.completed);
      if (filter === "pending") filtered = filtered.filter(t => !t.completed);
      if (filter === "high") filtered = filtered.filter(t => t.priority === "High");

      filtered.forEach((task, i) => {
        const li = document.createElement("li");
        li.className = task.completed ? "completed" : "";
        li.innerHTML = `
          <span>
            ${task.text} 
            <small>[${task.priority}] ${task.dueDate ? "📅 " + task.dueDate : ""}</small>
          </span>
          <div>
            <button onclick="toggleComplete(${i})">✔</button>
            <button onclick="editTask(${i})">✏️</button>
            <button onclick="deleteTask(${i})">🗑</button>
          </div>`;
        list.appendChild(li);
      });

      updateProgress();
    }

    function updateProgress() {
      const completed = tasks.filter(t => t.completed).length;
      const total = tasks.length;
      const percent = total ? (completed / total) * 100 : 0;
      document.getElementById("progressBar").style.width = percent + "%";
    }

    function saveTasks() {
      localStorage.setItem("tasks", JSON.stringify(tasks));
    }

    function toggleTheme() {
      darkMode = !darkMode;
      document.body.className = darkMode ? "dark" : "";
    }

    renderTasks();
  </script>
</body>
</html>
```

## OUTPUT

<img width="1365" height="708" alt="image" src="https://github.com/user-attachments/assets/c503f5fa-a701-43af-9ad0-151298dcb5e1" />


## RESULT
The program for creating To-do list using JavaScript is executed successfully.
