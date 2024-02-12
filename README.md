<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Stopwatch</title>
    <link rel="stylesheet" href="style.css">
    <link rel="javascript" herf="bag.js">
</head>
<body>
    <div class="container">
        <div class="stopwatch">
            <h1 id="display">00:00:00</h1>
            <div class="controls">
                <button id="startStop" onclick="startStop()">Start</button>
                <button id="lapReset" onclick="lapReset()">Lap</button>
            </div>
            <ul id="laps"></ul>
        </div>
   body {
    font-family: Arial, sans-serif;
    background-color: #6309f3;
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
    margin: 0;
}

.container {
    text-align: center;
}

.stopwatch {
    background-color: #e48912;
    border-radius: 10px;
    padding: 20px;
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
    width: 300px;
}

#display {
    font-size: 2em;
    margin-bottom: 10px;
}

.controls button {
    padding: 10px 20px;
    margin: 5px;
    font-size: 1em;
}

#laps {
    list-style-type: none;
    padding: 0;
    text-align: left;
    margin-top: 20px;
}
let timer;
let isRunning = false;
let startTime;
let laps = [];

function startStop() {
    if (isRunning) {
        clearInterval(timer);
        document.getElementById("startStop").innerText = "Start";
        isRunning = false;
    } else {
        startTime = Date.now() - laps.reduce((acc, lap) => acc + lap, 0);
        timer = setInterval(updateDisplay, 10);
        document.getElementById("startStop").innerText = "Stop";
        isRunning = true;
    }
}

function lapReset() {
    if (isRunning) {
        let lapTime = Date.now() - startTime;
        laps.push(lapTime);
        displayLap(lapTime);
    } else {
        document.getElementById("display").innerText = "00:00:00";
        laps = [];
        document.getElementById("laps").innerHTML = "";
    }
}

function updateDisplay() {
    let elapsedTime = Date.now() - startTime;
    let formattedTime = formatTime(elapsedTime);
    document.getElementById("display").innerText = formattedTime;
}

function formatTime(time) {
    let hours = Math.floor(time / 3600000);
    let minutes = Math.floor((time % 3600000) / 60000);
    let seconds = Math.floor((time % 60000) / 1000);
    let milliseconds = Math.floor(time % 1000 / 10);
    
    return `${pad(hours)}:${pad(minutes)}:${pad(seconds)}.${pad(milliseconds)}`;
}

function pad(num) {
    return num.toString().padStart(2, "0");
}

function displayLap(lapTime) {
    let lapItem = document.createElement("li");
    lapItem.innerText = formatTime(lapTime);
    document.getElementById("laps").appendChild(lapItem);
}

