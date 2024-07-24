<script>
    import { onMount } from "svelte";

    let tasks = [
        {
            id: 1,
            description: "Complete the project",
            startTime: "10:00 AM",
            endTime: "11:00 AM",
            priority: "High",
            status: "In Progress",
        },
        {
            id: 2,
            description: "Attend the meeting",
            startTime: "11:30 AM",
            endTime: "12:00 PM",
            priority: "Low",
            status: "Not Started",
        },
    ];

    let editingTaskId = null;
    let newDescription = "";
    let newTask = {
        description: "",
        startTime: "",
        endTime: "",
        priority: "Low",
        status: "Not Started",
    };
    let progress = 0;

    function calculateProgress() {
        const totalTasks = tasks.length;
        if (totalTasks === 0) return 0; // Avoid division by zero
        const completedTasks = tasks.filter(
            (task) => task.status === "Completed",
        ).length;
        return (completedTasks / totalTasks) * 100;
    }

    function startEditing(id, description) {
        editingTaskId = id;
        newDescription = description;
    }

    function saveDescription(id) {
        const task = tasks.find((task) => task.id === id);
        if (task) {
            task.description = newDescription;
            editingTaskId = null;
            newDescription = "";
        }
    }

    function updateStatus(id, newStatus) {
        const task = tasks.find((task) => task.id === id);
        if (task) {
            task.status = newStatus;
        }
    }

    function addTask() {
        if (newTask.description.trim()) {
            tasks = [...tasks, { ...newTask, id: tasks.length + 1 }];
            newTask = {
                description: "",
                startTime: "",
                endTime: "",
                priority: "Low",
                status: "Not Started",
            };
        }
    }

    function deleteTask(id) {
        tasks = tasks.filter((task) => task.id !== id);
        updateProgress();
    }

    function updateProgress() {
        progress = calculateProgress();
    }

    function getProgressColor(progress) {
        if (progress <= 30) {
            return 'red';
        } else if (progress <= 60) {
            return 'orange';
        } else if (progress <= 80) {
            return 'yellow';
        } else {
            return 'green';
        }
    }
</script>

<div class="todo-container">
    <div class="todo-card">
        <h2 class="animated-title">List of Tasks</h2>
        <div class="status">
            <p>Pending Tasks: {tasks.length}</p>
            <div class="priority">
                <div>High Priority</div>
                <div>Low Priority</div>
            </div>
        </div>

        <!-- Add Task Form -->
        <div class="add-task">
            <input
                type="text"
                bind:value={newTask.description}
                placeholder="Task Description"
            />
            <input
                type="time"
                bind:value={newTask.startTime}
                placeholder="Start Time"
            />
            <input
                type="time"
                bind:value={newTask.endTime}
                placeholder="End Time"
            />
            <select bind:value={newTask.priority}>
                <option value="High">High</option>
                <option value="Low">Low</option>
            </select>
            <button on:click={addTask}>Add Task</button>
        </div>

        <!-- Progress Bar Section -->
        <div class="progress-section">
            <p>Task Completion Progress</p>
            <div class="w3-light-grey">
                <div
                    class="w3-container w3-center"
                    style="width:{progress}%; background-color: {getProgressColor(progress)}"
                >
                    {progress.toFixed(1)}%
                </div>
            </div>
            <br />
            <button class="submit-button" on:click={updateProgress}>Submit</button>
        </div>

        <!-- Scrollable Table Section -->
        <div class="table-container">
            <table>
                <thead>
                    <tr>
                        <th>Task No.</th>
                        <th>Description</th>
                        <th>Start Time</th>
                        <th>End Time</th>
                        <th>Priority</th>
                        <th>Status</th>
                        <th>Actions</th>
                    </tr>
                </thead>
                <tbody>
                    {#each tasks as task, index (task.id)}
                        <tr>
                            <td>{index + 1}</td>
                            <td>
                                {#if editingTaskId === task.id}
                                    <input
                                        type="text"
                                        bind:value={newDescription}
                                        on:blur={() => saveDescription(task.id)}
                                    />
                                {:else}
                                    <span
                                        on:click={() =>
                                            startEditing(task.id, task.description)}
                                    >
                                        {task.description}
                                    </span>
                                {/if}
                            </td>
                            <td>{task.startTime}</td>
                            <td>{task.endTime}</td>
                            <td>{task.priority}</td>
                            <td>
                                <select
                                    on:change={(e) =>
                                        updateStatus(task.id, e.target.value)}
                                    bind:value={task.status}
                                >
                                    <option value="Not Started">Not Started</option>
                                    <option value="In Progress">In Progress</option>
                                    <option value="Completed">Completed</option>
                                </select>
                            </td>
                            <td class="action-buttons">
                                <button
                                    class="edit-button"
                                    on:click={() =>
                                        startEditing(task.id, task.description)}
                                    >&#x270E;</button>
                                <button
                                    class="delete-button"
                                    on:click={() => deleteTask(task.id)}
                                    >&#x1F5D1;</button>
                            </td>
                        </tr>
                    {/each}
                </tbody>
            </table>
        </div>
    </div>
</div>

<style>
    .todo-container {
        display: flex;
        justify-content: center;
        align-items: center;
        height: 100vh;
        background: url("path/to/your/background-image.jpg") no-repeat center
            center fixed;
        background-size: cover;
        padding: 1rem;
        box-sizing: border-box;
    }

    .todo-card {
        background: rgba(255, 255, 255, 0.9);
        padding: 2rem;
        border-radius: 12px;
        box-shadow: 0 6px 12px rgba(0, 0, 0, 0.2);
        width: 100%;
        max-width: 800px;
        font-family: "Roboto", sans-serif;
        transition:
            transform 0.3s ease,
            box-shadow 0.3s ease,
            background 0.3s ease;
        overflow: hidden;
    }

    .todo-card:hover {
        transform: translateY(-10px);
        box-shadow: 0 10px 20px rgba(0, 0, 0, 0.3);
    }

    .animated-title {
        margin-bottom: 1.5rem;
        font-size: 2rem;
        background: linear-gradient(45deg, #ff007f, #7f00ff, #00c9ff);
        -webkit-background-clip: text;
        -webkit-text-fill-color: transparent;
        background-clip: text;
        color: transparent;
        animation: colorChange 4s linear infinite;
    }

    @keyframes colorChange {
        0% {
            background-position: 0% 0%;
        }
        50% {
            background-position: 100% 100%;
        }
        100% {
            background-position: 0% 0%;
        }
    }

    .status {
        display: flex;
        justify-content: space-between;
        margin-bottom: 1rem;
    }

    .status {
        display: flex;
        justify-content: space-between;
        margin-bottom: 1rem;
    }

    .priority {
        display: flex;
        gap: 1rem;
    }

    .w3-light-grey {
        background-color: #f1f1f1;
        border-radius: 4px;
        overflow: hidden;
    }

    .w3-container {
        height: 24px;
        color: white;
        line-height: 24px;
    }

    table {
        width: 100%;
        border-collapse: collapse;
        margin-top: 1rem;
    }

    th,
    td {
        padding: 0.75rem;
        border: 1px solid #ccc;
        text-align: left;
    }

    th {
        background-color: #f4f4f4;
        position: sticky;
        top: 0;
        z-index: 1;
    }

    .action-buttons {
        display: flex;
        gap: 0.5rem;
    }

    .edit-button {
        padding: 0.5rem;
        border: none;
        border-radius: 4px;
        background: #007bff;
        color: white;
        cursor: pointer;
        transition: background 0.3s ease, transform 0.3s ease, box-shadow 0.3s ease;
    }

    .edit-button:hover {
        background: #0056b3;
        transform: translateY(-2px);
        box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
    }

    .edit-button:active {
        transform: translateY(1px);
        box-shadow: 0 2px 4px rgba(0, 0, 0, 0.2);
    }

    .delete-button {
        padding: 0.5rem;
        border: none;
        border-radius: 4px;
        background: #dc3545;
        color: white;
        cursor: pointer;
        transition: background 0.3s ease, transform 0.3s ease, box-shadow 0.3s ease;
    }

    .delete-button:hover {
        background: #c82333;
        transform: translateY(-2px);
        box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
    }

    .delete-button:active {
        transform: translateY(1px);
        box-shadow: 0 2px 4px rgba(0, 0, 0, 0.2);
    }

    .add-task {
        display: flex;
        gap: 0.5rem;
        margin-bottom: 1rem;
    }

    .add-task input,
    .add-task select {
        padding: 0.5rem;
        border: 1px solid #ccc;
        border-radius: 4px;
    }

    .add-task button {
        padding: 0.5rem 1rem;
        border: none;
        border-radius: 4px;
        background: #28a745;
        color: white;
        cursor: pointer;
        transition: background 0.3s ease, transform 0.3s ease, box-shadow 0.3s ease;
    }

    .add-task button:hover {
        background: #218838;
        transform: translateY(-2px);
        box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
    }

    .add-task button:active {
        transform: translateY(1px);
        box-shadow: 0 2px 4px rgba(0, 0, 0, 0.2);
    }

    .progress-section {
        margin: 1.5rem 0;
        text-align: center;
    }

    .progress-section p {
        margin-bottom: 0.5rem;
        font-size: 1rem;
    }

    .progress-section .submit-button {
        padding: 0.75rem 1.5rem;
        border: none;
        border-radius: 8px;
        background: #007bff;
        color: white;
        cursor: pointer;
        font-size: 1rem;
        transition: background 0.3s ease, transform 0.3s ease, box-shadow 0.3s ease;
    }

    .progress-section .submit-button:hover {
        background: #0056b3;
        transform: translateY(-2px);
        box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
    }

    .progress-section .submit-button:active {
        transform: translateY(1px);
        box-shadow: 0 2px 4px rgba(0, 0, 0, 0.2);
    }

    .table-container {
        max-height: 400px; /* Adjust this value as needed */
        overflow-y: auto;
    }
</style>
