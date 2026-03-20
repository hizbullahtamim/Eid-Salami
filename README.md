
<html lang="bn">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Tamim's Eid Salami 2026</title>
    <script src="https://cdn.jsdelivr.net/npm/canvas-confetti@1.6.0/dist/confetti.browser.min.js"></script>
    <style>
        :root { --bg: #0f172a; --card: #1e293b; --gold: #f59e0b; }
        body { font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif; background: var(--bg); color: white; text-align: center; margin: 0; padding: 20px; }
        .card { max-width: 420px; margin: auto; background: var(--card); padding: 30px; border-radius: 25px; box-shadow: 0 20px 50px rgba(0,0,0,0.5); border: 1px solid #334155; }
        .wheel-box { position: relative; width: 300px; height: 300px; margin: 25px auto; }
        #wheel { width: 100%; height: 100%; border-radius: 50%; border: 8px solid #475569; transition: transform 5s cubic-bezier(0.15, 0, 0.15, 1); 
            background: conic-gradient(#ef4444 0% 9%, #3b82f6 9% 18%, #10b981 18% 27%, #f59e0b 27% 36%, #8b5cf6 36% 45%, #ec4899 45% 54%, #06b6d4 54% 63%, #f97316 63% 72%, #84cc16 72% 81%, #6366f1 81% 90%, #64748b 90% 100%); 
        }
        .pointer { position: absolute; top: -15px; left: 50%; transform: translateX(-50%); width: 0; height: 0; border-left: 15px solid transparent; border-right: 15px solid transparent; border-top: 30px solid #ef4444; z-index: 10; }
        button { background: linear-gradient(135deg, #f59e0b, #d97706); color: white; border: none; padding: 15px 40px; font-size: 20px; border-radius: 50px; cursor: pointer; font-weight: bold; box-shadow: 0 4px 15px rgba(245, 158, 11, 0.4); }
        button:disabled { background: #475569; box-shadow: none; cursor: not-allowed; }
        
        /* Modal Popup */
        #overlay { display: none; position: fixed; top: 0; left: 0; width: 100%; height: 100%; background: rgba(0,0,0,0.9); z-index: 100; align-items: center; justify-content: center; }
        .modal { background: white; color: #1e293b; padding: 40px; border-radius: 25px; width: 85%; max-width: 350px; animation: bounce 0.6s ease; }
        @keyframes bounce { 0% { transform: scale(0.5); } 100% { transform: scale(1); } }
        .prize { font-size: 35px; font-weight: 900; color: #ef4444; margin: 15px 0; }
    </style>
</head>
<body>

    <div class="card">
        <h1 style="color: var(--gold); margin-bottom: 0;">🌙 ঈদ সালামি ২০২৬</h1>
        <p style="color: #94a3b8; margin-top: 5px;">স্পিন করে আপনার সালামি বুঝে নিন!</p>
        
        <div class="wheel-box">
            <div class="pointer"></div>
            <div id="wheel"></div>
        </div>

        <button id="spinBtn" onclick="spin()">ভাগ্য পরীক্ষা করুন!</button>
        <p style="font-size: 11px; color: #64748b; margin-top: 20px;">শুধুমাত্র একবার স্পিন করার সুযোগ পাবেন।</p>
    </div>

    <div id="overlay">
        <div class="modal">
            <h2 style="margin: 0;">অভিনন্দন! 🎉</h2>
            <div id="msg"></div>
            <p style="font-size: 13px; color: #666;">এই স্ক্রিনশটটি <b>তামিমকে</b> পাঠিয়ে সালামি সংগ্রহ করুন।</p>
            <div id="ts" style="font-size: 10px; color: #aaa; margin-top: 15px;"></div>
        </div>
    </div>

    <script>
        const nums = [4, 21, 3, 2, 50, 11, 5, 8, 7, 9, 26];
        const max = Math.max(...nums);
        const prizes = nums.map(n => ({ val: n, weight: (max + 5) - n }));

        function getPrize() {
            let total = prizes.reduce((s, p) => s + p.weight, 0);
            let r = Math.random() * total;
            for (let p of prizes) {
                if (r < p.weight) return p;
                r -= p.weight;
            }
        }

        function spin() {
            document.getElementById('spinBtn').disabled = true;
            const winIdx = nums.indexOf(getPrize().val);
            const deg = (360 / nums.length);
            const rotation = (3600) + (360 - (winIdx * deg)) - (deg / 2);

            document.getElementById('wheel').style.transform = `rotate(${rotation}deg)`;

            setTimeout(() => {
                confetti({ particleCount: 200, spread: 80, origin: { y: 0.6 } });
                const now = new Date();
                document.getElementById('msg').innerHTML = `আপনি তামিমের কাছ থেকে জিতেছেন<div class="prize">${nums[winIdx]} টাকা</div>`;
                document.getElementById('ts').innerText = `ID: ${Math.floor(Math.random()*10000)} | ${now.toLocaleString('bn-BD')}`;
                document.getElementById('overlay').style.display = 'flex';
            }, 5200);
        }
    </script>
</body>
</html>
