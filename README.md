<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>TYSON-AI-WINGO 30SEC</title>
    <link href="https://fonts.googleapis.com/css2?family=El+Messiri&display=swap" rel="stylesheet">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        :root {
            --gold: #FFD700;
            --red: #FF6B6B;
            --blue: #4ECDC4;
            --green: #76c776;
            --orange: #FFA500;
            --dark-bg: rgba(0, 0, 0, 0.85);
            --card-bg: rgba(30, 30, 40, 0.95);
            --border-light: rgba(255, 255, 255, 0.15);
        }
        
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        
        body {
            font-family: 'El Messiri', sans-serif;
            text-align: center;
            background: linear-gradient(135deg, #0f0c29, #302b63, #24243e);
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            padding: 20px;
            color: white;
            position: relative;
            overflow-x: hidden;
        }
        
        /* Animated background elements */
        .bg-elements {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            z-index: -1;
            overflow: hidden;
        }
        
        .bg-element {
            position: absolute;
            border-radius: 50%;
            background: rgba(255, 255, 255, 0.05);
            animation: float 15s infinite linear;
        }
        
        @keyframes float {
            0% { transform: translateY(0) translateX(0) rotate(0deg); }
            100% { transform: translateY(-1000px) translateX(1000px) rotate(720deg); }
        }
        
        /* Connection status */
        .connection-status {
            position: absolute;
            top: 15px;
            right: 15px;
            display: flex;
            align-items: center;
            gap: 8px;
            font-size: 14px;
            background: rgba(0,0,0,0.6);
            padding: 5px 10px;
            border-radius: 20px;
            z-index: 10;
        }
        
        .status-dot {
            width: 10px;
            height: 10px;
            border-radius: 50%;
            background-color: var(--green);
            box-shadow: 0 0 10px var(--green);
        }
        
        .status-dot.offline {
            background-color: var(--red);
            box-shadow: 0 0 10px var(--red);
        }
        
        .ping-display {
            margin-left: 10px;
            display: flex;
            align-items: center;
            gap: 4px;
        }
        
        .ping-value {
            font-weight: bold;
        }
        
        .ping-excellent { color: var(--green); }
        .ping-good { color: var(--blue); }
        .ping-fair { color: var(--orange); }
        .ping-poor { color: var(--red); }
        
        .container {
            background: var(--card-bg);
            backdrop-filter: blur(10px);
            padding: 30px 25px;
            border-radius: 20px;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.5);
            width: 100%;
            max-width: 450px;
            border: 1px solid var(--border-light);
            position: relative;
            overflow: hidden;
        }
        
        /* Header styles */
        .header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 20px;
        }
        
        .date-display {
            font-size: 15px;
            background: rgba(0,0,0,0.4);
            padding: 5px 10px;
            border-radius: 15px;
        }
        
        .telegram-link {
            background: #0088cc;
            color: white;
            text-decoration: none;
            padding: 5px 15px;
            border-radius: 20px;
            font-size: 14px;
            display: flex;
            align-items: center;
            gap: 5px;
            transition: all 0.3s ease;
        }
        
        .telegram-link:hover {
            background: #006699;
            transform: translateY(-2px);
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.3);
        }
        
        h1 {
            color: var(--gold);
            margin-bottom: 25px;
            font-size: 28px;
            text-shadow: 0 0 10px rgba(255, 215, 0, 0.7);
            position: relative;
        }
        
        h1::after {
            content: "LIVE";
            position: absolute;
            top: -12px;
            right: 0;
            background: var(--red);
            color: white;
            font-size: 12px;
            padding: 2px 8px;
            border-radius: 10px;
            animation: pulse 1.5s infinite;
        }
        
        /* Timer styles */
        .timer-container {
            height: 6px;
            background: rgba(255, 255, 255, 0.1);
            border-radius: 10px;
            margin: 20px 0;
            overflow: hidden;
            position: relative;
        }
        
        .timer-progress {
            height: 100%;
            width: 100%;
            background: linear-gradient(to right, var(--red), var(--blue));
            border-radius: 10px;
            animation: timerAnimation 30s linear forwards;
        }
        
        @keyframes timerAnimation {
            0% { width: 100%; }
            100% { width: 0%; }
        }
        
        /* Results display */
        .results-container {
            display: grid;
            grid-template-columns: repeat(2, 1fr);
            gap: 15px;
            margin-bottom: 20px;
        }
        
        .result-box {
            background: rgba(0, 0, 0, 0.3);
            padding: 15px;
            border-radius: 15px;
            border: 1px solid var(--border-light);
            transition: all 0.3s ease;
        }
        
        .result-box:hover {
            transform: translateY(-5px);
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.3);
        }
        
        .result-box h3 {
            font-size: 16px;
            margin-bottom: 10px;
            color: #aaa;
        }
        
        .result-value {
            font-size: 24px;
            font-weight: bold;
        }
        
        #resultNumber {
            color: var(--gold);
            text-shadow: 0 0 10px rgba(255, 215, 0, 0.7);
            font-size: 28px;
        }
        
        .red { color: var(--red); text-shadow: 0 0 10px rgba(255, 107, 107, 0.7); }
        .blue { color: var(--blue); text-shadow: 0 0 10px rgba(78, 205, 196, 0.7); }
        .big { color: var(--blue); }
        .small { color: var(--red); }
        
        /* History section */
        .history-section {
            margin-top: 25px;
            background: rgba(0, 0, 0, 0.3);
            border-radius: 15px;
            padding: 15px;
            border: 1px solid var(--border-light);
        }
        
        .history-section h2 {
            font-size: 18px;
            margin-bottom: 15px;
            color: var(--gold);
            text-align: left;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }
        
        .history-list {
            max-height: 200px;
            overflow-y: auto;
            padding-right: 5px;
        }
        
        .history-list::-webkit-scrollbar {
            width: 6px;
        }
        
        .history-list::-webkit-scrollbar-thumb {
            background: var(--gold);
            border-radius: 10px;
        }
        
        .history-item {
            display: flex;
            justify-content: space-between;
            padding: 10px 15px;
            background: rgba(255, 255, 255, 0.05);
            border-radius: 10px;
            margin-bottom: 8px;
            border: 1px solid var(--border-light);
            transition: all 0.3s ease;
        }
        
        .history-item:hover {
            background: rgba(255, 255, 255, 0.1);
            transform: translateX(5px);
        }
        
        .history-period {
            font-weight: bold;
            width: 35%;
            text-align: left;
        }
        
        .history-number {
            font-weight: bold;
            color: var(--gold);
            width: 15%;
        }
        
        .history-color, .history-size {
            width: 20%;
            font-weight: bold;
        }
        
        .history-time {
            width: 20%;
            font-size: 12px;
            opacity: 0.8;
        }
        
        /* Footer */
        .footer {
            margin-top: 25px;
            font-size: 13px;
            opacity: 0.8;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }
        
        .credits {
            text-align: left;
            font-size: 12px;
        }
        
        /* Ping stats */
        .ping-stats {
            display: flex;
            justify-content: space-between;
            margin-top: 10px;
            padding: 8px 15px;
            background: rgba(0,0,0,0.2);
            border-radius: 10px;
            font-size: 13px;
        }
        
        .ping-stat {
            display: flex;
            flex-direction: column;
            align-items: center;
        }
        
        .stat-value {
            font-weight: bold;
            font-size: 16px;
            margin-top: 3px;
        }
        
        /* Responsive design */
        @media (max-width: 480px) {
            .container {
                padding: 20px 15px;
            }
            
            .header {
                flex-direction: column;
                gap: 10px;
            }
            
            .results-container {
                grid-template-columns: 1fr;
            }
            
            h1 {
                font-size: 24px;
            }
            
            .result-value {
                font-size: 22px;
            }
            
            .history-period {
                width: 30%;
            }
            
            .history-number, .history-color, .history-size {
                width: 20%;
            }
            
            .history-time {
                width: 20%;
            }
        }
        
        /* Animations */
        @keyframes pulse {
            0% { 
                transform: scale(1); 
                opacity: 1;
            }
            50% { 
                transform: scale(1.05); 
                opacity: 0.8;
            }
            100% { 
                transform: scale(1); 
                opacity: 1;
            }
        }
        
        .pulse {
            animation: pulse 0.5s ease;
        }
        
        @keyframes pingPulse {
            0% { transform: scale(1); }
            50% { transform: scale(1.2); }
            100% { transform: scale(1); }
        }
        
        .ping-pulse {
            animation: pingPulse 0.5s ease;
        }
    </style>
</head>
<body>
    <!-- Background elements -->
    <div class="bg-elements">
        <div class="bg-element" style="width: 150px; height: 150px; top: 10%; left: 5%;"></div>
        <div class="bg-element" style="width: 100px; height: 100px; top: 70%; left: 80%;"></div>
        <div class="bg-element" style="width: 80px; height: 80px; top: 40%; left: 70%;"></div>
        <div class="bg-element" style="width: 120px; height: 120px; top: 60%; left: 10%;"></div>
    </div>
    
    <!-- Connection status with ping -->
    <div class="connection-status" id="connectionStatus">
        <span class="status-dot"></span>
        <span id="statusText">Online</span>
        <div class="ping-display">
            <i class="fas fa-signal"></i>
            <span id="pingValue" class="ping-value ping-excellent">-</span>
            <span>ms</span>
        </div>
    </div>
    
    <div class="container">
        <!-- Header with date and Telegram link -->
        <div class="header">
            <div class="date-display" id="currentDate">
                Loading date...
            </div>
            <a href="https://t.me/tyson_owner" class="telegram-link" target="_blank">
                <i class="fab fa-telegram"></i> @tyson_owner
            </a>
        </div>
        
        <h1>𝗧𝗬𝗦𝗢𝗡-𝗔𝗜-𝗪𝗜𝗡𝗚𝗢 𝟯𝟬𝗦𝗘𝗖</h1>
        
        <!-- Timer -->
        <div class="timer-container">
            <div class="timer-progress" id="timerProgress"></div>
        </div>
        
        <!-- Results display -->
        <div class="results-container">
            <div class="result-box">
                <h3>Period</h3>
                <div class="result-value" id="period">000000</div>
            </div>
            
            <div class="result-box">
                <h3>Timer</h3>
                <div class="result-value" id="timer">00:30</div>
            </div>
            
            <div class="result-box">
                <h3>Number</h3>
                <div class="result-value"><span id="resultNumber">-</span></div>
            </div>
            
            <div class="result-box">
                <h3>Color</h3>
                <div class="result-value" id="resultColor">-</div>
            </div>
            
            <div class="result-box">
                <h3>Big/Small</h3>
                <div class="result-value" id="resultSize">-</div>
            </div>
        </div>
        
        <!-- History section -->
        <div class="history-section">
            <h2>
                <span>Recent Results</span>
                <span id="pingQuality">Connection: Excellent</span>
            </h2>
            <div class="history-list" id="historyList">
                <!-- History items will be added here -->
            </div>
            
            <!-- Ping statistics -->
            <div class="ping-stats">
                <div class="ping-stat">
                    <span>Current Ping</span>
                    <span id="currentPingStat" class="stat-value ping-excellent">- ms</span>
                </div>
                <div class="ping-stat">
                    <span>Avg Ping</span>
                    <span id="avgPingStat" class="stat-value ping-excellent">- ms</span>
                </div>
                <div class="ping-stat">
                    <span>Best Ping</span>
                    <span id="bestPingStat" class="stat-value ping-excellent">- ms</span>
                </div>
            </div>
        </div>
        
        <!-- Footer -->
        <div class="footer">
            <div class="credits">
                Results update every 30 seconds<br>
                <!-- This Web Free By #enzo #dev -->
            </div>
            <div>
                <i class="fas fa-sync-alt"></i> Live Updates
            </div>
        </div>
    </div>

    <script>
        // Initialize variables
        let lastPeriod = "";
        let resultHistory = [];
        let pingHistory = [];
        const maxHistory = 15;
        let pingInterval;
        let pingCount = 0;
        let totalPing = 0;
        let bestPing = Infinity;
        
        // Update real-time date
        function updateDateTime() {
            const now = new Date();
            const dateStr = now.toLocaleDateString('en-GB', {
                day: '2-digit',
                month: '2-digit',
                year: 'numeric'
            }).replace(/\//g, '-');
            
            const timeStr = now.toLocaleTimeString('en-GB', {
                hour: '2-digit',
                minute: '2-digit',
                second: '2-digit'
            });
            
            document.getElementById('currentDate').textContent = `${dateStr} | ${timeStr}`;
        }
        
        // Update connection status
        function updateConnectionStatus() {
            const statusElement = document.getElementById('connectionStatus');
            const statusDot = statusElement.querySelector('.status-dot');
            const statusText = document.getElementById('statusText');
            
            if (navigator.onLine) {
                statusDot.classList.remove('offline');
                statusText.textContent = 'Online';
            } else {
                statusDot.classList.add('offline');
                statusText.textContent = 'Offline';
            }
        }
        
        // Measure ping
        function measurePing() {
            if (!navigator.onLine) {
                document.getElementById('pingValue').textContent = 'Offline';
                return;
            }
            
            const startTime = performance.now();
            
            // Use a reliable endpoint for ping measurement
            fetch('https://www.google.com/favicon.ico?' + new Date().getTime(), {
                method: 'HEAD',
                cache: 'no-cache',
                mode: 'no-cors'
            })
            .then(() => {
                const endTime = performance.now();
                const ping = Math.round(endTime - startTime);
                
                // Update ping display
                updatePingDisplay(ping);
                
                // Store ping for statistics
                pingHistory.push(ping);
                pingCount++;
                totalPing += ping;
                
                if (ping < bestPing) {
                    bestPing = ping;
                }
                
                // Update statistics
                updatePingStats();
            })
            .catch(() => {
                // If ping fails, show offline
                document.getElementById('pingValue').textContent = 'Error';
                document.getElementById('pingValue').className = 'ping-value ping-poor';
            });
        }
        
        // Update ping display with color coding
        function updatePingDisplay(ping) {
            const pingValueElement = document.getElementById('pingValue');
            pingValueElement.textContent = ping;
            pingValueElement.classList.add('ping-pulse');
            
            // Remove the animation class after it completes
            setTimeout(() => {
                pingValueElement.classList.remove('ping-pulse');
            }, 500);
            
            // Color code based on ping quality
            if (ping < 50) {
                pingValueElement.className = 'ping-value ping-excellent';
                document.getElementById('pingQuality').textContent = 'Connection: Excellent';
            } else if (ping < 100) {
                pingValueElement.className = 'ping-value ping-good';
                document.getElementById('pingQuality').textContent = 'Connection: Good';
            } else if (ping < 200) {
                pingValueElement.className = 'ping-value ping-fair';
                document.getElementById('pingQuality').textContent = 'Connection: Fair';
            } else {
                pingValueElement.className = 'ping-value ping-poor';
                document.getElementById('pingQuality').textContent = 'Connection: Poor';
            }
        }
        
        // Update ping statistics
        function updatePingStats() {
            const currentPing = pingHistory[pingHistory.length - 1];
            const avgPing = Math.round(totalPing / pingCount);
            
            document.getElementById('currentPingStat').textContent = `${currentPing} ms`;
            document.getElementById('avgPingStat').textContent = `${avgPing} ms`;
            document.getElementById('bestPingStat').textContent = `${bestPing} ms`;
            
            // Apply color classes
            applyPingColor('currentPingStat', currentPing);
            applyPingColor('avgPingStat', avgPing);
            applyPingColor('bestPingStat', bestPing);
        }
        
        // Apply color class based on ping value
        function applyPingColor(elementId, ping) {
            const element = document.getElementById(elementId);
            element.className = 'stat-value ';
            
            if (ping < 50) {
                element.classList.add('ping-excellent');
            } else if (ping < 100) {
                element.classList.add('ping-good');
            } else if (ping < 200) {
                element.classList.add('ping-fair');
            } else {
                element.classList.add('ping-poor');
            }
        }
        
        // Update period and timer
        function updatePeriodAndTimer() {
            const now = new Date();
            const startTime = new Date(now);
            startTime.setHours(5, 30, 0, 0); // 5:30 AM
            
            // Adjust if before start time
            if (now < startTime) {
                startTime.setDate(startTime.getDate() - 1);
            }
            
            const elapsedSeconds = Math.floor((now - startTime) / 1000);
            const totalPeriods = Math.floor(elapsedSeconds / 30);
            const upcomingPeriod = totalPeriods + 1;
            const formattedDate = new Intl.DateTimeFormat('en-GB', {
                year: 'numeric',
                month: '2-digit',
                day: '2-digit'
            }).format(now).replace(/\//g, '');
            
            const periodNumber = `100005${String(upcomingPeriod).padStart(4, '0')}`;
            const lastFourDigits = periodNumber.slice(-4);
            
            // Update period if changed
            if (periodNumber !== lastPeriod) {
                lastPeriod = periodNumber;
                generateResult(lastFourDigits);
            }
            
            // Update period display
            document.getElementById("period").textContent = formattedDate + periodNumber;
            
            // Update timer
            const remainingSeconds = 30 - (elapsedSeconds % 30);
            document.getElementById("timer").textContent = `00:${String(remainingSeconds).padStart(2, '0')}`;
            
            // Reset timer animation
            const timerProgress = document.getElementById('timerProgress');
            timerProgress.style.animation = 'none';
            setTimeout(() => {
                timerProgress.style.animation = 'timerAnimation 30s linear forwards';
            }, 10);
            
            // Schedule next update
            setTimeout(updatePeriodAndTimer, 1000);
        }
        
        // Generate result
        function generateResult(lastFourDigits) {
            const digits = lastFourDigits.split('').map(Number);
            const sum = digits.reduce((a, b) => a + b, 0);
            const product = digits.reduce((a, b) => a * b, 1);
            const predictionValue = (sum + product) % 10;
            
            // Determine results
            const size = predictionValue >= 5 ? "BIG" : "SMALL";
            const color = predictionValue % 2 === 0 ? "BLUE" : "RED";
            
            // Update result displays
            const resultNumber = document.getElementById("resultNumber");
            resultNumber.textContent = predictionValue;
            resultNumber.classList.add('pulse');
            setTimeout(() => resultNumber.classList.remove('pulse'), 500);
            
            const resultColor = document.getElementById("resultColor");
            resultColor.textContent = color;
            resultColor.className = color.toLowerCase();
            resultColor.classList.add('pulse');
            setTimeout(() => resultColor.classList.remove('pulse'), 500);
            
            const resultSize = document.getElementById("resultSize");
            resultSize.textContent = size;
            resultSize.className = size.toLowerCase();
            resultSize.classList.add('pulse');
            setTimeout(() => resultSize.classList.remove('pulse'), 500);
            
            // Add to history
            resultHistory.unshift({
                period: lastPeriod,
                number: predictionValue,
                color: color,
                size: size,
                time: new Date().toLocaleTimeString([], {hour: '2-digit', minute:'2-digit'})
            });
            
            // Limit history length
            if (resultHistory.length > maxHistory) {
                resultHistory.pop();
            }
            
            updateHistoryDisplay();
        }
        
        // Update history display
        function updateHistoryDisplay() {
            const historyList = document.getElementById("historyList");
            historyList.innerHTML = '';
            
            resultHistory.forEach((item, index) => {
                const historyItem = document.createElement('div');
                historyItem.className = 'history-item';
                
                historyItem.innerHTML = `
                    <div class="history-period">${item.period}</div>
                    <div class="history-number">${item.number}</div>
                    <div class="history-color ${item.color.toLowerCase()}">${item.color}</div>
                    <div class="history-size ${item.size.toLowerCase()}">${item.size}</div>
                    <div class="history-time">${item.time}</div>
                `;
                
                historyList.appendChild(historyItem);
            });
        }
        
        // Initialize when DOM is loaded
        document.addEventListener('DOMContentLoaded', function() {
            // Initial updates
            updateDateTime();
            updateConnectionStatus();
            updatePeriodAndTimer();
            
            // Update date/time every second
            setInterval(updateDateTime, 1000);
            
            // Start ping measurement
            measurePing();
            pingInterval = setInterval(measurePing, 3000);
            
            // Listen for online/offline events
            window.addEventListener('online', updateConnectionStatus);
            window.addEventListener('offline', updateConnectionStatus);
            
            // Add some initial history for demo
            setTimeout(() => {
                for (let i = 0; i < 5; i++) {
                    const mockPeriod = `100005${String(1000 + i).padStart(4, '0')}`;
                    const mockDigits = mockPeriod.slice(-4).split('').map(Number);
                    const mockSum = mockDigits.reduce((a, b) => a + b, 0);
                    const mockProduct = mockDigits.reduce((a, b) => a * b, 1);
                    const mockValue = (mockSum + mockProduct) % 10;
                    
                    resultHistory.push({
                        period: mockPeriod,
                        number: mockValue,
                        color: mockValue % 2 === 0 ? "BLUE" : "RED",
                        size: mockValue >= 5 ? "BIG" : "SMALL",
                        time: new Date().toLocaleTimeString([], {hour: '2-digit', minute:'2-digit'})
                    });
                }
                updateHistoryDisplay();
            }, 1000);
        });
    </script>
</body>
</html>
