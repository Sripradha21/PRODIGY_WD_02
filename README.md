<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Stopwatch Web Application</title>
    <style>
        body, html {
            margin: 0;
            padding: 0;
            font-family: Arial, sans-serif;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            background-color: #f4f4f4;
        }

        .stopwatch-container {
            text-align: center;
            background: #333;
            padding: 30px;
            border-radius: 10px;
            color: white;
            box-shadow: 0px 0px 20px rgba(0, 0, 0, 0.1);
        }

        .time {
            font-size: 48px;
            margin-bottom: 20px;
        }

        .buttons {
            margin-bottom: 20px;
        }

        .buttons button {
            padding: 10px 20px;
            margin: 5px;
            font-size: 16px;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            transition: background-color 0.3s;
        }

        .buttons button:hover {
            background-color: #555;
        }

        .lap-times {
            max-height: 150px;
            overflow-y: auto;
            text-align: left;
            margin-top: 20px;
            padding: 10px;
            background: #444;
            border-radius: 5px;
        }

        .lap-times ul {
            list-style: none;
            padding: 0;
            margin: 0;
        }

        .lap-times li {
            padding: 5px 0;
            border-bottom: 1px solid #555;
        }
    </style>
</head>
<body>
    <div class="stopwatch-container">
        <h1>Stopwatch</h1>
        <div class="time" id="time">00:00:00</div>
        <div class="buttons">
            <button onclick="startStopwatch()">Start</button>
            <button onclick="pauseStopwatch()">Pause</button>
            <button onclick="resetStopwatch()">Reset</button>
            <button onclick="lapTime()">Lap</button>
        </div>
        <div class="lap-times" id="lap-times">
            <h3>Lap Times</h3>
            <ul id="laps"></ul>
        </div>
    </div>

    <script>
        let startTime, updatedTime, difference, tInterval;
        let running = false;
        let lapCount = 0;

        function startStopwatch() {
            if (!running) {
                startTime = new Date().getTime();
                tInterval = setInterval(updateTime, 1);
                running = true;
            }
        }

        function pauseStopwatch() {
            if (running) {
                clearInterval(tInterval);
                running = false;
            }
        }

        function resetStopwatch() {
            clearInterval(tInterval);
            running = false;
            document.getElementById('time').innerHTML = "00:00:00";
            document.getElementById('laps').innerHTML = "";
            lapCount = 0;
        }

        function lapTime() {
            if (running) {
                const lapList = document.getElementById('laps');
                const lapTime = document.getElementById('time').innerHTML;
                const lapItem = document.createElement('li');
                lapCount++;
                lapItem.textContent = `Lap ${lapCount}: ${lapTime}`;
                lapList.appendChild(lapItem);
            }
        }

        function updateTime() {
            updatedTime = new Date().getTime();
            difference = updatedTime - startTime;

            const hours = Math.floor((difference % (1000 * 60 * 60 * 24)) / (1000 * 60 * 60));
            const minutes = Math.floor((difference % (1000 * 60 * 60)) / (1000 * 60));
            const seconds = Math.floor((difference % (1000 * 60)) / 1000);

            document.getElementById('time').innerHTML = 
                (hours < 10 ? "0" + hours : hours) + ":" + 
                (minutes < 10 ? "0" + minutes : minutes) + ":" + 
                (seconds < 10 ? "0" + seconds : seconds);
        }
    </script>
</body>
</html>
