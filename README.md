<!DOCTYPE html>
<html>
<head>
    <title>Internet Speed Test</title>
    <meta charset="UTF-8">
    <style>
        body {
            font-family: Arial, sans-serif;
            text-align: center;
            padding-top: 50px;
            background-color: #f0f0f0;
        }
        h1 {
            color: #333;
        }
        #results {
            margin-top: 20px;
            font-size: 1.2em;
        }
        button {
            padding: 10px 20px;
            font-size: 16px;
            background-color: #0078d4;
            color: white;
            border: none;
            border-radius: 4px;
            cursor: pointer;
        }
    </style>
</head>
<body>
    <h1>Internet Speed Test</h1>
    <button onclick="startSpeedTest()">Start Test</button>
    <div id="results"></div>

    <script>
        function startSpeedTest() {
            const resultsDiv = document.getElementById('results');
            resultsDiv.innerHTML = 'Testing...';

            const image = new Image();
            const imageSize = 500000; // ~500KB
            const startTime = Date.now();
            const cacheBuster = '?nn=' + startTime;

            image.onload = () => {
                const endTime = Date.now();
                const duration = (endTime - startTime) / 1000;
                const bitsLoaded = imageSize * 8;
                const speedBps = (bitsLoaded / duration).toFixed(2);
                const speedKbps = (speedBps / 1024).toFixed(2);
                const speedMbps = (speedKbps / 1024).toFixed(2);

                resultsDiv.innerHTML = `
                    <p><strong>Download Speed:</strong> ${speedMbps} Mbps</p>
                    <p><small>Rough estimate, not 100% accurate</small></p>
                `;
            };

            image.onerror = () => {
                resultsDiv.innerHTML = 'Error testing speed. Please try again.';
            };

            image.src = 'https://upload.wikimedia.org/wikipedia/commons/3/3f/Fronalpstock_big.jpg' + cacheBuster;
        }
    </script>
</body>
</html>
