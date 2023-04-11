---
layout: page
title: "Generator"
permalink: /generator
---

<!DOCTYPE html>
<html>
<head>
    <style>
        ul {
            list-style-type: none;
            padding: 0;
        }

        li {
            padding: 10px;
            border: 1px solid #ccc;
            margin-bottom: 5px;
            background-color: #f9f9f9;
            cursor: move;
        }
    </style>
    <script>
        document.addEventListener("DOMContentLoaded", function() {
            var sortableList = document.getElementById("sortableList");

            // Add event listeners for drag and drop events
            sortableList.addEventListener("dragstart", handleDragStart);
            sortableList.addEventListener("dragenter", handleDragEnter);
            sortableList.addEventListener("dragover", handleDragOver);
            sortableList.addEventListener("dragleave", handleDragLeave);
            sortableList.addEventListener("drop", handleDrop);
            sortableList.addEventListener("dragend", handleDragEnd);

            function handleDragStart(event) {
                event.dataTransfer.setData("text/plain", event.target.id);
                event.target.classList.add("dragged");
            }

            function handleDragEnter(event) {
                event.preventDefault();
                event.target.classList.add("over");
            }

            function handleDragOver(event) {
                event.preventDefault();
            }

            function handleDragLeave(event) {
                event.target.classList.remove("over");
            }

            function handleDrop(event) {
                event.preventDefault();
                var draggedScenarioId = event.dataTransfer.getData("text/plain");
                var draggedScenario = document.getElementById(draggedScenarioId);
                var droppedScenario = event.target.closest("li");

                if (draggedScenario && droppedScenario) {
                    if (draggedScenario !== droppedScenario) {
                        sortableList.insertBefore(draggedScenario, droppedScenario);
                    }
                }

                event.target.classList.remove("over");
            }

            function handleDragEnd(event) {
                event.target.classList.remove("dragged");
            }

            function addScenario() {
                var scenarioCount = sortableList.getElementsByTagName("li").length + 1;
                var newScenario = document.createElement("li");
                newScenario.className = "scenario-field";
                newScenario.draggable = true;
                newScenario.id = "scenario" + scenarioCount;
                newScenario.innerHTML = `
                    <label for="scenario${scenarioCount}">Scenario ${scenarioCount}</label>
                    <input type="text" id="scenario${scenarioCount}" name="scenario${scenarioCount}" value="">
                    <button class="deleteBtn" onclick="deleteScenario(this)">Delete</button>
                `;
                sortableList.appendChild(newScenario);
            }

            function deleteScenario(button) {
                var scenario = button.closest("li");
                scenario.parentNode.removeChild(scenario);
            }
        });
    </script>
</head>
<body>
    <h1>Scenarios</h1>
    <p>Drag and drop to reorder scenarios:</p>
    <ul id="sortableList">
        <li class="scenario-field" draggable="true" id="scenario1">
            <label for="scenario1">Scenario 1</label>
            <input type="text" id="scenario1" name="scenario1" value="">
            <button class="deleteBtn" onclick="deleteScenario(this)">Delete</button>
        </li>
        <li class="scenario-field" draggable="true" id="scenario2">
            <label for="scenario2">Scenario 2</label>
            <input type="text" id="scenario2"
            name="scenario2" value="">
            <button class="deleteBtn" onclick="deleteScenario(this)">Delete</button>
        </li>
        <li class="scenario-field" draggable="true" id="scenario3">
            <label for="scenario3">Scenario 3</label>
            <input type="text" id="scenario3" name="scenario3" value="">
            <button class="deleteBtn" onclick="deleteScenario(this)">Delete</button>
        </li>
    </ul>
    <button onclick="addScenario()">Add Scenario</button>

    <script>
        // Function to delete a scenario
        function deleteScenario(button) {
            var scenario = button.closest("li");
            scenario.parentNode.removeChild(scenario);
        }

        // Function to add a new scenario
        function addScenario() {
            var scenarioCount = document.getElementById("sortableList").getElementsByTagName("li").length + 1;
            var newScenario = document.createElement("li");
            newScenario.className = "scenario-field";
            newScenario.draggable = true;
            newScenario.id = "scenario" + scenarioCount;
            newScenario.innerHTML = `
                <label for="scenario${scenarioCount}">Scenario ${scenarioCount}</label>
                <input type="text" id="scenario${scenarioCount}" name="scenario${scenarioCount}" value="">
                <button class="deleteBtn" onclick="deleteScenario(this)">Delete</button>
            `;
            document.getElementById("sortableList").appendChild(newScenario);
        }
    </script>
</body>
</html>
