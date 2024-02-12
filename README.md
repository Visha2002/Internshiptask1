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
    </div>

    <script src="script.js"></script>
</body>
</html>

