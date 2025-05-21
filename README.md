# To-do-List
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>To-Do List App</title>
    <style>
        :root {
            --primary-color: #4a6fa5;
            --secondary-color: #6b8cae;
            --accent-color: #ff7e5f;
            --light-color: #f8f9fa;
            --dark-color: #343a40;
            --success-color: #28a745;
            --warning-color: #ffc107;
            --danger-color: #dc3545;
        }
        
        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }
        
        body {
            background-color: #f5f7fa;
            color: var(--dark-color);
            line-height: 1.6;
            padding: 20px;
        }
        
        .container {
            max-width: 800px;
            margin: 0 auto;
            background: white;
            border-radius: 10px;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.1);
            padding: 30px;
        }
        
        h1 {
            text-align: center;
            margin-bottom: 30px;
            color: var(--primary-color);
        }
        
        .input-section {
            display: flex;
            gap: 10px;
            margin-bottom: 30px;
        }
        
        #task-input {
            flex: 1;
            padding: 12px 15px;
            border: 2px solid #ddd;
            border-radius: 5px;
            font-size: 16px;
            transition: border-color 0.3s;
        }
        
        #task-input:focus {
            outline: none;
            border-color: var(--primary-color);
        }
        
        #priority-select {
            padding: 12px 15px;
            border: 2px solid #ddd;
            border-radius: 5px;
            font-size: 16px;
            background-color: white;
            cursor: pointer;
        }
        
        button {
            padding: 12px 20px;
            background-color: var(--primary-color);
            color: white;
            border: none;
            border-radius: 5px;
            font-size: 16px;
            cursor: pointer;
            transition: background-color 0.3s;
        }
        
        button:hover {
            background-color: var(--secondary-color);
        }
        
        .filter-section {
            display: flex;
            justify-content: space-between;
            margin-bottom: 20px;
            flex-wrap: wrap;
            gap: 10px;
        }
        
        .filter-buttons {
            display: flex;
            gap: 10px;
        }
        
        .filter-btn {
            background-color: white;
            color: var(--dark-color);
            border: 1px solid #ddd;
        }
        
        .filter-btn.active {
            background-color: var(--primary-color);
            color: white;
        }
        
        .task-list {
            list-style-type: none;
        }
        
        .task-item {
            display: flex;
            align-items: center;
            padding: 15px;
            margin-bottom: 10px;
            background-color: white;
            border-radius: 5px;
            box-shadow: 0 2px 5px rgba(0, 0, 0, 0.05);
            transition: transform 0.2s;
            border-left: 4px solid #ddd;
        }
        
        .task-item:hover {
            transform: translateY(-2px);
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
        }
        
        .task-item.high {
            border-left-color: var(--danger-color);
        }
        
        .task-item.medium {
            border-left-color: var(--warning-color);
        }
        
        .task-item.low {
            border-left-color: var(--success-color);
        }
        
        .task-checkbox {
            margin-right: 15px;
            transform: scale(1.3);
            cursor: pointer;
        }
        
        .task-text {
            flex: 1;
            font-size: 16px;
        }
        
        .task-text.completed {
            text-decoration: line-through;
            color: #888;
        }
        
        .task-priority {
            padding: 5px 10px;
            border-radius: 20px;
            font-size: 12px;
            font-weight: bold;
            margin-right: 15px;
            text-transform: uppercase;
        }
        
        .priority-high {
            background-color: rgba(220, 53, 69, 0.1);
            color: var(--danger-color);
        }
        
        .priority-medium {
            background-color: rgba(255, 193, 7, 0.1);
            color: var(--warning-color);
        }
        
        .priority-low {
            background-color: rgba(40, 167, 69, 0.1);
            color: var(--success-color);
        }
        
        .task-actions {
            display: flex;
            gap: 10px;
        }
        
        .edit-btn, .delete-btn {
            padding: 5px 10px;
            font-size: 14px;
            border-radius: 3px;
        }
        
        .edit-btn {
            background-color: var(--warning-color);
        }
        
        .delete-btn {
            background-color: var(--danger-color);
        }
        
        .stats {
            margin-top: 30px;
            padding-top: 20px;
            border-top: 1px solid #eee;
            display: flex;
            justify-content: space-between;
        }
        
        @media (max-width: 600px) {
            .input-section {
                flex-direction: column;
            }
            
            .filter-section {
                flex-direction: column;
            }
            
            .filter-buttons {
                justify-content: space-between;
            }
            
            .task-item {
                flex-direction: column;
                align-items: flex-start;
            }
            
            .task-info {
                width: 100%;
                display: flex;
                justify-content: space-between;
                margin-bottom: 10px;
            }
            
            .task-actions {
                align-self: flex-end;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>My To-Do List</h1>
        
        <div class="input-section">
            <input type="text" id="task-input" placeholder="Add a new task...">
            <select id="priority-select">
                <option value="low">Low Priority</option>
                <option value="medium">Medium Priority</option>
                <option value="high">High Priority</option>
            </select>
            <button id="add-btn">Add Task</button>
        </div>
        
        <div class="filter-section">
            <h3>Tasks</h3>
            <div class="filter-buttons">
                <button class="filter-btn active" data-filter="all">All</button>
                <button class="filter-btn" data-filter="active">Active</button>
                <button class="filter-btn" data-filter="completed">Completed</button>
            </div>
        </div>
        
        <ul class="task-list" id="task-list">
            <!-- Tasks will be added here dynamically -->
        </ul>
        
        <div class="stats">
            <span id="total-tasks">Total: 0 tasks</span>
            <span id="completed-tasks">Completed: 0 tasks</span>
        </div>
    </div>

    <script>
        document.addEventListener('DOMContentLoaded', function() {
            // DOM Elements
            const taskInput = document.getElementById('task-input');
            const prioritySelect = document.getElementById('priority-select');
            const addBtn = document.getElementById('add-btn');
            const taskList = document.getElementById('task-list');
            const filterBtns = document.querySelectorAll('.filter-btn');
            const totalTasksSpan = document.getElementById('total-tasks');
            const completedTasksSpan = document.getElementById('completed-tasks');
            
            // Tasks array
            let tasks = JSON.parse(localStorage.getItem('tasks')) || [];
            
            // Initialize the app
            renderTasks();
            updateStats();
            
            // Event Listeners
            addBtn.addEventListener('click', addTask);
            taskInput.addEventListener('keypress', function(e) {
                if (e.key === 'Enter') addTask();
            });
            
            filterBtns.forEach(btn => {
                btn.addEventListener('click', filterTasks);
            });
            
            // Functions
            function addTask() {
                const taskText = taskInput.value.trim();
                const priority = prioritySelect.value;
                
                if (taskText) {
                    const newTask = {
                        id: Date.now(),
                        text: taskText,
                        priority: priority,
                        completed: false,
                        createdAt: new Date().toISOString()
                    };
                    
                    tasks.push(newTask);
                    saveTasks();
                    renderTasks();
                    updateStats();
                    
                    // Reset input
                    taskInput.value = '';
                    taskInput.focus();
                    prioritySelect.value = 'low';
                }
            }
            
            function renderTasks(filter = 'all') {
                taskList.innerHTML = '';
                
                let filteredTasks = tasks;
                
                if (filter === 'active') {
                    filteredTasks = tasks.filter(task => !task.completed);
                } else if (filter === 'completed') {
                    filteredTasks = tasks.filter(task => task.completed);
                }
                
                if (filteredTasks.length === 0) {
                    taskList.innerHTML = '<p style="text-align: center; color: #888;">No tasks found</p>';
                    return;
                }
                
                filteredTasks.forEach(task => {
                    const taskItem = document.createElement('li');
                    taskItem.className = `task-item ${task.priority}`;
                    taskItem.dataset.id = task.id;
                    
                    taskItem.innerHTML = `
                        <input type="checkbox" class="task-checkbox" ${task.completed ? 'checked' : ''}>
                        <span class="task-text ${task.completed ? 'completed' : ''}">${task.text}</span>
                        <span class="task-priority priority-${task.priority}">${task.priority}</span>
                        <div class="task-actions">
                            <button class="edit-btn">Edit</button>
                            <button class="delete-btn">Delete</button>
                        </div>
                    `;
                    
                    taskList.appendChild(taskItem);
                    
                    // Add event listeners to the new elements
                    const checkbox = taskItem.querySelector('.task-checkbox');
                    const editBtn = taskItem.querySelector('.edit-btn');
                    const deleteBtn = taskItem.querySelector('.delete-btn');
                    
                    checkbox.addEventListener('change', toggleTask);
                    editBtn.addEventListener('click', editTask);
                    deleteBtn.addEventListener('click', deleteTask);
                });
            }
            
            function toggleTask(e) {
                const taskId = parseInt(e.target.closest('.task-item').dataset.id);
                const task = tasks.find(task => task.id === taskId);
                
                if (task) {
                    task.completed = e.target.checked;
                    saveTasks();
                    renderTasks(document.querySelector('.filter-btn.active').dataset.filter);
                    updateStats();
                }
            }
            
            function editTask(e) {
                const taskItem = e.target.closest('.task-item');
                const taskId = parseInt(taskItem.dataset.id);
                const task = tasks.find(task => task.id === taskId);
                const taskText = taskItem.querySelector('.task-text');
                
                if (task) {
                    const newText = prompt('Edit your task:', task.text);
                    if (newText !== null && newText.trim() !== '') {
                        task.text = newText.trim();
                        taskText.textContent = newText.trim();
                        saveTasks();
                    }
                }
            }
            
            function deleteTask(e) {
                if (confirm('Are you sure you want to delete this task?')) {
                    const taskId = parseInt(e.target.closest('.task-item').dataset.id);
                    tasks = tasks.filter(task => task.id !== taskId);
                    saveTasks();
                    renderTasks(document.querySelector('.filter-btn.active').dataset.filter);
                    updateStats();
                }
            }
            
            function filterTasks(e) {
                const filter = e.target.dataset.filter;
                
                filterBtns.forEach(btn => {
                    btn.classList.remove('active');
                });
                
                e.target.classList.add('active');
                renderTasks(filter);
            }
            
            function updateStats() {
                const totalTasks = tasks.length;
                const completedTasks = tasks.filter(task => task.completed).length;
                
                totalTasksSpan.textContent = `Total: ${totalTasks} task${totalTasks !== 1 ? 's' : ''}`;
                completedTasksSpan.textContent = `Completed: ${completedTasks} task${completedTasks !== 1 ? 's' : ''}`;
            }
            
            function saveTasks() {
                localStorage.setItem('tasks', JSON.stringify(tasks));
            }
        });
    </script>
</body>
</html>
