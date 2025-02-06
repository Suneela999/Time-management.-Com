<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Time Management App</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            text-align: center;
            background-color: #f4f4f4;
            padding: 20px;
        }
        #task-container {
            max-width: 400px;
            margin: auto;
            background: white;
            padding: 20px;
            border-radius: 10px;
            box-shadow: 0px 0px 10px rgba(0, 0, 0, 0.1);
        }
        input, button {
            padding: 10px;
            margin: 5px;
        }
        .task {
            display: flex;
            justify-content: space-between;
            align-items: center;
            background: #e0e0e0;
            padding: 10px;
            margin-top: 5px;
            border-radius: 5px;
        }
        .completed {
            text-decoration: line-through;
            color: gray;
        }
    </style>
</head>
<body>

    <h2>Time Management To-Do List</h2>

    <div id="task-container">
        <input type="text" id="task-input" placeholder="Enter Task">
        <input type="number" id="task-time" placeholder="Minutes" min="1">
        <button onclick="addTask()">Add Task</button>

        <ul id="task-list"></ul>
    </div>

    <script>
        function addTask() {
            let taskText = document.getElementById("task-input").value;
            let taskTime = document.getElementById("task-time").value;
            
            if (taskText === "" || taskTime === "") {
                alert("Please enter a task and time.");
                return;
            }

            let taskList = document.getElementById("task-list");

            let li = document.createElement("li");
            li.classList.add("task");
            li.innerHTML = `
                <span>${taskText} - <b><span class="time">${taskTime}</span> min</b></span>
                <button onclick="startTimer(this)">Start</button>
                <button onclick="completeTask(this)">✔</button>
                <button onclick="deleteTask(this)">❌</button>
            `;

            taskList.appendChild(li);
            document.getElementById("task-input").value = "";
            document.getElementById("task-time").value = "";
        }

        function startTimer(button) {
            let timeElement = button.parentElement.querySelector(".time");
            let time = parseInt(timeElement.innerText);

            if (time > 0) {
                button.disabled = true;
                let interval = setInterval(() => {
                    time--;
                    timeElement.innerText = time;
                    if (time <= 0) {
                        clearInterval(interval);
                        button.disabled = false;
                        alert("Task time completed!");
                    }
                }, 60000); // 1 minute per decrement
            }
        }

        function completeTask(button) {
            button.parentElement.classList.toggle("completed");
        }

        function deleteTask(button) {
            button.parentElement.remove();
        }
    </script>

</body>
</html># Time-management.-Com
