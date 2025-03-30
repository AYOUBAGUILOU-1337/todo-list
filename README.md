<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Color-Coded Todo List</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 0;
            padding: 20px;
            background-color: #f5f5f5;
        }
        
        h1 {
            text-align: center;
            color: #333;
            margin-bottom: 20px;
        }
        
        .container {
            max-width: 1000px;
            margin: 0 auto;
            background-color: white;
            border-radius: 8px;
            box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
            padding: 20px;
        }
        
        .task-form {
            display: flex;
            flex-wrap: wrap;
            gap: 10px;
            margin-bottom: 20px;
            padding: 15px;
            background-color: #f9f9f9;
            border-radius: 8px;
        }
        
        .form-group {
            flex: 1;
            min-width: 200px;
        }
        
        input, select, textarea {
            width: 100%;
            padding: 10px;
            border: 1px solid #ddd;
            border-radius: 4px;
            font-size: 14px;
        }
        
        textarea {
            resize: vertical;
            min-height: 60px;
        }
        
        label {
            display: block;
            margin-bottom: 5px;
            font-weight: bold;
            color: #555;
        }
        
        button {
            padding: 10px 15px;
            background-color: #4CAF50;
            color: white;
            border: none;
            border-radius: 4px;
            cursor: pointer;
            font-size: 15px;
        }
        
        button:hover {
            background-color: #45a049;
        }
        
        .add-btn {
            margin-top: 24px;
            height: 40px;
        }
        
        table {
            width: 100%;
            border-collapse: collapse;
            margin-top: 20px;
        }
        
        th, td {
            border: 1px solid #ddd;
            padding: 12px;
            text-align: left;
        }
        
        th {
            background-color: #f2f2f2;
            font-weight: bold;
        }
        
        .task-item {
            position: relative;
            padding: 10px;
            border-radius: 4px;
            margin-bottom: 5px;
        }
        
        .task-content {
            margin-bottom: 5px;
        }
        
        .task-time {
            font-size: 14px;
            font-weight: bold;
        }
        
        .task-title {
            font-size: 16px;
            font-weight: bold;
            margin: 5px 0;
        }
        
        .task-description {
            font-size: 14px;
            color: #555;
        }
        
        .task-location {
            font-size: 13px;
            font-style: italic;
            color: #777;
        }
        
        .task-actions {
            margin-top: 10px;
            display: flex;
            gap: 5px;
        }
        
        .edit-btn {
            background-color: #2196F3;
        }
        
        .delete-btn {
            background-color: #f44336;
        }
        
        .complete-btn {
            background-color: #ff9800;
        }
        
        /* Category colors */
        .category-work { background-color: #bbdefb; }
        .category-study { background-color: #c8e6c9; }
        .category-personal { background-color: #ffccbc; }
        .category-health { background-color: #e1bee7; }
        .category-errands { background-color: #fff9c4; }
        .category-other { background-color: #dcedc8; }
        
        .completed {
            opacity: 0.6;
        }
        
        .completed .task-title {
            text-decoration: line-through;
        }
        
        .filter-controls {
            display: flex;
            gap: 10px;
            margin-bottom: 20px;
            flex-wrap: wrap;
        }
        
        .clear-all {
            margin-left: auto;
            background-color: #f44336;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>Color-Coded Todo List</h1>
        
        <form id="task-form" class="task-form">
            <div class="form-group">
                <label for="task-title">Task Title</label>
                <input type="text" id="task-title" placeholder="Enter task title" required>
            </div>
            
            <div class="form-group">
                <label for="task-category">Category</label>
                <select id="task-category" required>
                    <option value="work">Work</option>
                    <option value="study">Study</option>
                    <option value="personal">Personal</option>
                    <option value="health">Health</option>
                    <option value="errands">Errands</option>
                    <option value="other">Other</option>
                </select>
            </div>
            
            <div class="form-group">
                <label for="task-date">Date</label>
                <input type="date" id="task-date" required>
            </div>
            
            <div class="form-group">
                <label for="task-time">Time</label>
                <input type="time" id="task-time">
            </div>
            
            <div class="form-group">
                <label for="task-location">Location</label>
                <input type="text" id="task-location" placeholder="Where?">
            </div>
            
            <div class="form-group" style="flex: 2; min-width: 300px;">
                <label for="task-description">Description</label>
                <textarea id="task-description" placeholder="Task details..."></textarea>
            </div>
            
            <button type="submit" class="add-btn">Add Task</button>
        </form>
        
        <div class="filter-controls">
            <select id="category-filter">
                <option value="all">All Categories</option>
                <option value="work">Work</option>
                <option value="study">Study</option>
                <option value="personal">Personal</option>
                <option value="health">Health</option>
                <option value="errands">Errands</option>
                <option value="other">Other</option>
            </select>
            
            <select id="date-filter">
                <option value="all">All Dates</option>
                <option value="today">Today</option>
                <option value="tomorrow">Tomorrow</option>
                <option value="week">This Week</option>
                <option value="month">This Month</option>
            </select>
            
            <button id="clear-all" class="clear-all">Clear All</button>
        </div>
        
        <table id="task-table">
            <thead>
                <tr>
                    <th style="width: 15%;">Date & Time</th>
                    <th style="width: 15%;">Category</th>
                    <th style="width: 50%;">Task</th>
                    <th style="width: 20%;">Actions</th>
                </tr>
            </thead>
            <tbody id="task-list">
                <!-- Tasks will be added here -->
            </tbody>
        </table>
    </div>
    
    <script>
        // DOM elements
        const taskForm = document.getElementById('task-form');
        const taskTitle = document.getElementById('task-title');
        const taskCategory = document.getElementById('task-category');
        const taskDate = document.getElementById('task-date');
        const taskTime = document.getElementById('task-time');
        const taskLocation = document.getElementById('task-location');
        const taskDescription = document.getElementById('task-description');
        const taskList = document.getElementById('task-list');
        const categoryFilter = document.getElementById('category-filter');
        const dateFilter = document.getElementById('date-filter');
        const clearAllBtn = document.getElementById('clear-all');
        
        // Set default date to today
        const today = new Date();
        const formattedDate = today.toISOString().split('T')[0];
        taskDate.value = formattedDate;
        
        // Load tasks from localStorage
        let tasks = JSON.parse(localStorage.getItem('colorTasks')) || [];
        let editIndex = -1;
        
        // Render tasks
        function renderTasks() {
            taskList.innerHTML = '';
            
            const filteredTasks = filterTasks();
            
            // Sort tasks by date and time
            filteredTasks.sort((a, b) => {
                const dateA = new Date(a.date + 'T' + (a.time || '00:00'));
                const dateB = new Date(b.date + 'T' + (b.time || '00:00'));
                return dateA - dateB;
            });
            
            if (filteredTasks.length === 0) {
                const emptyRow = document.createElement('tr');
                emptyRow.innerHTML = `
                    <td colspan="4" style="text-align: center; padding: 20px;">
                        No tasks found. Add a new task to get started!
                    </td>
                `;
                taskList.appendChild(emptyRow);
                return;
            }
            
            filteredTasks.forEach((task, index) => {
                const row = document.createElement('tr');
                
                // Format date for display
                const taskDate = new Date(task.date);
                const formattedDate = taskDate.toLocaleDateString('en-US', {
                    weekday: 'short',
                    month: 'short',
                    day: 'numeric'
                });
                
                row.innerHTML = `
                    <td>
                        <div class="task-time">${formattedDate}</div>
                        ${task.time ? `<div>${task.time}</div>` : ''}
                    </td>
                    <td>
                        <div class="task-item category-${task.category} ${task.completed ? 'completed' : ''}">
                            ${task.category.charAt(0).toUpperCase() + task.category.slice(1)}
                        </div>
                    </td>
                    <td>
                        <div class="task-content ${task.completed ? 'completed' : ''}">
                            <div class="task-title">${task.title}</div>
                            ${task.description ? `<div class="task-description">${task.description}</div>` : ''}
                            ${task.location ? `<div class="task-location">📍 ${task.location}</div>` : ''}
                        </div>
                    </td>
                    <td>
                        <div class="task-actions">
                            <button class="complete-btn" onclick="toggleComplete(${tasks.indexOf(task)})">
                                ${task.completed ? 'Undo' : 'Complete'}
                            </button>
                            <button class="edit-btn" onclick="editTask(${tasks.indexOf(task)})">Edit</button>
                            <button class="delete-btn" onclick="deleteTask(${tasks.indexOf(task)})">Delete</button>
                        </div>
                    </td>
                `;
                
                taskList.appendChild(row);
            });
            
            // Save to localStorage
            saveTasks();
        }
        
        // Filter tasks based on selected filters
        function filterTasks() {
            const categoryValue = categoryFilter.value;
            const dateValue = dateFilter.value;
            
            return tasks.filter(task => {
                // Category filter
                if (categoryValue !== 'all' && task.category !== categoryValue) {
                    return false;
                }
                
                // Date filter
                if (dateValue !== 'all') {
                    const taskDate = new Date(task.date);
                    const today = new Date();
                    today.setHours(0, 0, 0, 0);
                    
                    const tomorrow = new Date(today);
                    tomorrow.setDate(tomorrow.getDate() + 1);
                    
                    const weekEnd = new Date(today);
                    weekEnd.setDate(weekEnd.getDate() + 7);
                    
                    const monthEnd = new Date(today);
                    monthEnd.setMonth(monthEnd.getMonth() + 1);
                    
                    if (dateValue === 'today' && taskDate.toDateString() !== today.toDateString()) {
                        return false;
                    } else if (dateValue === 'tomorrow' && taskDate.toDateString() !== tomorrow.toDateString()) {
                        return false;
                    } else if (dateValue === 'week' && (taskDate < today || taskDate >= weekEnd)) {
                        return false;
                    } else if (dateValue === 'month' && (taskDate < today || taskDate >= monthEnd)) {
                        return false;
                    }
                }
                
                return true;
            });
        }
        
        // Add or update task
        function addOrUpdateTask(e) {
            e.preventDefault();
            
            const task = {
                title: taskTitle.value.trim(),
                category: taskCategory.value,
                date: taskDate.value,
                time: taskTime.value,
                location: taskLocation.value.trim(),
                description: taskDescription.value.trim(),
                completed: false
            };
            
            if (editIndex >= 0) {
                // Update existing task
                task.completed = tasks[editIndex].completed;
                tasks[editIndex] = task;
                editIndex = -1;
            } else {
                // Add new task
                tasks.push(task);
            }
            
            // Reset form
            taskForm.reset();
            taskDate.value = formattedDate;
            
            renderTasks();
        }
        
        // Toggle complete status
        function toggleComplete(index) {
            tasks[index].completed = !tasks[index].completed;
            renderTasks();
        }
        
        // Edit task
        function editTask(index) {
            const task = tasks[index];
            taskTitle.value = task.title;
            taskCategory.value = task.category;
            taskDate.value = task.date;
            taskTime.value = task.time || '';
            taskLocation.value = task.location || '';
            taskDescription.value = task.description || '';
            
            editIndex = index;
        }
        
        // Delete task
        function deleteTask(index) {
            if (confirm('Are you sure you want to delete this task?')) {
                tasks.splice(index, 1);
                renderTasks();
            }
        }
        
        // Clear all tasks
        function clearAllTasks() {
            if (confirm('Are you sure you want to delete all tasks? This cannot be undone.')) {
                tasks = [];
                renderTasks();
            }
        }
        
        // Save tasks to localStorage
        function saveTasks() {
            localStorage.setItem('colorTasks', JSON.stringify(tasks));
        }
        
        // Event listeners
        taskForm.addEventListener('submit', addOrUpdateTask);
        categoryFilter.addEventListener('change', renderTasks);
        dateFilter.addEventListener('change', renderTasks);
        clearAllBtn.addEventListener('click', clearAllTasks);
        
        // Make functions available globally for onclick handlers
        window.toggleComplete = toggleComplete;
        window.editTask = editTask;
        window.deleteTask = deleteTask;
        
        // Initial render
        renderTasks();
    </script>
</body>
</html>
