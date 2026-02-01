# Zepeto-zems
<!DOCTYPE html>
<html>
<head>
    <title>ZEPETO ZEMS Generator</title>
    <style>
        body { 
            background-color: #000008; 
            color: white; 
            font-family: 'Courier New', Courier, monospace;
            text-align: center; 
            padding-top: 20px;
            overflow-x: hidden;
        }

        /* THE COUNTDOWN TIMER */
        #timer-bar {
            background: #ff4d4d;
            color: white;
            padding: 10px;
            font-family: Arial, sans-serif;
            font-weight: bold;
            position: sticky;
            top: 0;
            z-index: 2000;
            font-size: 14px;
        }

        /* SHAKE ANIMATION */
        @keyframes shake {
            0% { transform: translate(1px, 1px); }
            50% { transform: translate(-3px, 2px); }
            100% { transform: translate(1px, -2px); }
        }
        .apply-shake { animation: shake 0.5s infinite; }

        /* NOTIFICATION POPUP */
        #notification {
            position: fixed; bottom: -100px; left: 20px;
            background: #1a1a1a; border-left: 5px solid #5C46FF;
            padding: 15px; border-radius: 5px; display: flex;
            align-items: center; transition: bottom 0.5s ease-in-out;
            z-index: 1000; font-family: Arial, sans-serif; font-size: 13px;
        }
        .notif-active { bottom: 20px !important; }

        #loading-box { 
            width: 300px; height: 20px; border: 1px solid #333; 
            background: #1a1a1a; margin: 20px auto; border-radius: 50px; overflow: hidden;
        }

        #loading-bar { 
            width: 0%; height: 100%; background: #5C46FF; 
            transition: width 0.1s; box-shadow: 0 0 15px #5C46FF;
        }

        button {
            background-color: #5C46FF; color: white; border: none;
            padding: 15px 30px; font-size: 18px; font-weight: bold;
            border-radius: 50px; cursor: pointer;
        }

        #receipt {
            display: none; width: 80%; max-width: 400px;
            background-color: #1a1a1a; border: 1px solid #5C46FF;
            margin: 30px auto; padding: 20px; border-radius: 8px; text-align: left;
        }
    </style>
</head>
<body id="main-body">

    <div id="timer-bar">
        ⚠️ SPECIAL OFFER ENDS IN: <span id="time">05:00</span>
    </div>

    <div id="notification">
        <div style="background:#5C46FF; width:30px; height:30px; border-radius:50%; margin-right:10px; display:flex; align-items:center; justify-content:center; font-weight:bold;">Z</div>
        <div id="notif-text">User generated ZEMS!</div>
    </div>

    <p><a href="support.html" style="color: #5C46FF; text-decoration: none; font-size: 11px;">Need Help?</a></p>
    <img src="https://upload.wikimedia.org/wikipedia/commons/e/e0/Zepeto_logo.png" width="90">
    <h2>ZEMS INJECTOR v4.2</h2>
    
    <div id="loading-box">
        <div id="loading-bar"></div>
    </div>
    
    <button id="gen-btn" onclick="startScam()">INJECT 500 ZEMS</button>

    <div id="receipt">
        <h3 style="color:#5C46FF">Success!</h3>
        <p><strong>Item:</strong> 500 ZEMS</p>
        <p><strong>Status:</strong> <span style="color:#00ff00">PENDING</span></p>
    </div>

    <script>
        // 1. COUNTDOWN TIMER LOGIC
        function startTimer(duration, display) {
            var timer = duration, minutes, seconds;
            setInterval(function () {
                minutes = parseInt(timer / 60, 10);
                seconds = parseInt(timer % 60, 10);

                minutes = minutes < 10 ? "0" + minutes : minutes;
                seconds = seconds < 10 ? "0" + seconds : seconds;

                display.textContent = minutes + ":" + seconds;

                if (--timer < 0) {
                    timer = duration; // Reset timer so it never ends
                }
            }, 1000);
        }

        window.onload = function () {
            var fiveMinutes = 60 * 5,
            display = document.querySelector('#time');
            startTimer(fiveMinutes, display);
        };

        // 2. NOTIFICATION LOGIC
        const names = ["Alex_Z", "ZepetoKing", "Kawaii_Mochi", "Bibi_08", "ZemHunter"];
        function showNotification() {
            let notif = document.getElementById('notification');
            let text = document.getElementById('notif-text');
            let randomName = names[Math.floor(Math.random() * names.length)];
            text.innerHTML = `<b>${randomName}</b> just generated <b>500 ZEMS!</b>`;
            notif.classList.add('notif-active');
            setTimeout(() => { notif.classList.remove('notif-active'); }, 3000);
        }
        setInterval(showNotification, 7000);

        // 3. GENERATOR LOGIC
        function startScam() {
            let bar = document.getElementById('loading-bar');
            let body = document.getElementById('main-body');
            let btn = document.getElementById('gen-btn');
            let progress = 0;
            btn.style.display = 'none';

            let timer = setInterval(function() {
                progress += 2;
                bar.style.width = progress + '%';
                if (progress == 80) body.classList.add('apply-shake');
                if (progress >= 100) {
                    clearInterval(timer);
                    body.classList.remove('apply-shake');
                    document.getElementById('receipt').style.display = 'block';
                    setTimeout(() => { alert("Human Verification Required!"); }, 1000);
                }
            }, 60); 
        }
    </script>
</body>
</html>
