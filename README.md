<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Aimers Test Series | Exam Mode</title>
    <style>
        body { font-family: sans-serif; background: #ececec; padding: 20px; user-select: none; }
        .container { max-width: 700px; background: white; margin: auto; padding: 25px; border-radius: 12px; box-shadow: 0 5px 15px rgba(0,0,0,0.2); }
        .header { text-align: center; border-bottom: 2px solid #333; margin-bottom: 20px; }
        #timer { font-size: 24px; color: red; font-weight: bold; position: fixed; top: 10px; right: 10px; background: white; padding: 10px; border: 2px solid red; border-radius: 10px; }
        .question { margin-bottom: 20px; padding: 15px; border: 1px solid #ddd; border-radius: 8px; }
        .btn { width: 100%; padding: 15px; background: #007bff; color: white; border: none; border-radius: 8px; cursor: pointer; font-size: 18px; }
        .warning { color: red; font-weight: bold; text-align: center; display: none; }
    </style>
</head>
<body oncontextmenu="return false;">

    <div id="timer">60:00</div>

    <div class="container">
        <div class="header">
            <h1>Aimers Test Series</h1>
            <p>Subject: Math (Log & Diff) | Time: 60 Mins</p>
        </div>

        <input type="text" id="studentName" placeholder="Enter Full Name" style="width:96%; padding:10px; margin-bottom:20px;">

        <div id="quiz-area">
            <div class="question" data-ans="A">
                <p><b>Q1. Find the derivative of x sin x:</b></p>
                <input type="radio" name="q1" value="A"> sin x + x cos x <br>
                <input type="radio" name="q1" value="B"> cos x <br>
                <input type="radio" name="q1" value="C"> sin x - x cos x <br>
            </div>

            <p style="text-align: center; color: gray;">... [Add all 20 questions here] ...</p>
            
            <button class="btn" onclick="submitTest()">Finish & Send Report</button>
        </div>
    </div>

    <script>
        let timeLeft = 3600; // 60 minutes
        let cheatCount = 0;
        let timerInterval = setInterval(updateTimer, 1000);

        // 1. Timer Logic
        function updateTimer() {
            let mins = Math.floor(timeLeft / 60);
            let secs = timeLeft % 60;
            document.getElementById('timer').innerText = `${mins}:${secs < 10 ? '0' : ''}${secs}`;
            if (timeLeft <= 0) submitTest("Time Up!");
            timeLeft--;
        }

        // 2. Anti-Cheat Logic (Visibility Change)
        document.addEventListener("visibilitychange", function() {
            if (document.hidden) {
                cheatCount++;
                if (cheatCount >= 2) {
                    alert("Test Terminated! You switched apps too many times.");
                    submitTest("Cheating Detected (Tab Switched)");
                } else {
                    alert("WARNING: Do not switch apps or tabs! Your test will logout.");
                }
            }
        });

        // 3. Submit Logic
        function submitTest(reason = "Manual Submit") {
            clearInterval(timerInterval);
            let score = 0;
            let name = document.getElementById('studentName').value || "Unknown";
            
            // Score count (Example for Q1)
            if(document.querySelector('input[name="q1"]:checked')?.value === "A") score++;

            let finalMsg = `*Aimers Test Report*%0A*Student:* ${name}%0A*Score:* ${score}/20%0A*Status:* ${reason}`;
            
            // Result sending to your WhatsApp
            let myNumber = "91XXXXXXXXXX"; // APNA WHATSAPP NUMBER YAHAN DALO (With 91)
            window.location.href = `https://wa.me/${myNumber}?text=${finalMsg}`;
            
            document.body.innerHTML = `<h1 style='text-align:center; margin-top:100px;'>Test Submitted! Result sent to teacher.</h1>`;
        }
    </script>
</body>
</html>
