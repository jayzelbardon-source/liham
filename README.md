<html>
<head>
    <title>Aking Liham - Maria Clara by Sugarcane</title>
    <link href="https://fonts.googleapis.com/css2?family=Great+Vibes&family=Playfair+Display+SC:ital,wght@0,400;0,700;1,400&family=Sacramento&display=swap" rel="stylesheet">
    <style>
        * { margin: 0; padding: 0; box-sizing: border-box; }
        body {
            background: #d4c3a8;
            min-height: 100vh;
            display: flex;
            align-items: center;
            justify-content: center;
            padding: 20px;
            overflow-x: hidden;
            overflow-y: auto;
            position: relative;
        }

        /* BACKGROUND */
        .table-bg {
            position: fixed; top: 0; left: 0;
            width: 100%; height: 100%;
            background: url('https://images.unsplash.com/photo-1614563637806-840210fda001?ixlib=rb-4.0.3&auto=format&fit=crop&w=1920&q=80') center/cover;
            opacity: 0.7; mix-blend-mode: multiply;
            z-index: 0;
        }

        /* KRAFT ENVELOPE */
        #envelope {
            width: 420px; height: 280px;
            background: #c19a6b;
            border: 1px solid #8b5a2b;
            box-shadow: 0 15px 25px rgba(0,0,0,0.7);
            position: relative;
            cursor: pointer;
            z-index: 3;
            transform: rotate(-2deg) scale(1);
            transition: all 1.2s cubic-bezier(0.25, 0.46, 0.45, 0.94);
            display: block; /* Palaging nakikita hanggang sa ma-click */
        }
        #flap {
            position: absolute; top: 0; left: 0;
            width: 100%; height: 50%;
            background: #b08968;
            border-bottom: 1px solid #8b5a2b;
            transform-origin: top center;
            transition: transform 0.8s cubic-bezier(0.175, 0.885, 0.32, 1.275);
            z-index: 4;
            clip-path: polygon(0 0, 100% 0, 50% 60%);
        }
        #twine {
            position: absolute; top: 40%; left: 50%;
            transform: translate(-50%, -50%) rotate(-15deg);
            width: 70%; height: 6px;
            background: #8b5a2b;
            border-radius: 3px;
            z-index: 5;
            transition: all 0.6s ease-out;
        }
        #flowers {
            position: absolute; top: 35%; left: 50%;
            transform: translate(-50%, -50%);
            display: flex;
            gap: 5px;
            z-index: 6;
            transition: all 0.6s ease-out;
        }
        .flower {
            width: 8px; height: 15px;
            border-radius: 3px;
        }
        .f1 { background: #d4a017; }
        .f2 { background: #8fbc8f; }
        .f3 { background: #f5deb3; }
        .accent {
            position: absolute;
            width: 6px; height: 6px;
            background: #d4a017;
            border-radius: 50%;
            z-index: 4;
            transition: all 0.6s ease-out;
        }
        .acc1 { top: 25%; left: 30%; }
        .acc2 { top: 35%; left: 70%; }
        .acc3 { top: 65%; left: 25%; }
        .acc4 { top: 75%; left: 65%; }

        /* ENVELOPE TRANSFORMATION STATE */
        #envelope.transforming {
            opacity: 0; /* Mawawala nang dahan-dahan */
            visibility: hidden; /* Hindi na makikita pero nandiyan pa */
            position: absolute; /* Hindi makakasagabal sa papel */
        }

        /* FLOATING PAPER - PERMANENTLY VISIBLE */
        #full-letter {
            display: none;
            position: relative;
            max-width: 850px;
            width: 100%;
            padding: 60px 70px;
            background: #f9f1e6;
            background-image: 
                radial-gradient(#d4c3a8 1px, transparent 1px),
                radial-gradient(#d4c3a8 1px, transparent 1px);
            background-size: 50px 50px;
            background-position: 0 0, 25px 25px;
            border-radius: 2px;
            box-shadow: 0 20px 40px rgba(0,0,0,0.5);
            z-index: 3;
            animation: float 6s ease-in-out infinite;
            margin: 20px 0; /* Para hindi ma-cut sa maliit na screen */
        }
        @keyframes float {
            0% { transform: rotate(-1deg) translateY(0px); }
            25% { transform: rotate(0.5deg) translateY(-5px); }
            50% { transform: rotate(0deg) translateY(-10px); }
            75% { transform: rotate(0.5deg) translateY(-5px); }
            100% { transform: rotate(-1deg) translateY(0px); }
        }

        /* CALLIGRAPHY TEXT */
        .greeting {
            font-family: 'Sacramento', cursive;
            font-size: 55px; color: #4a2c2a;
            margin-bottom: 40px;
            text-align: center;
            line-height: 1.2;
            opacity: 0;
            animation: fadeIn 1s ease forwards 0.8s;
        }
        .message {
            font-family: 'Great Vibes', cursive;
            font-size: 28px; color: #4a2c2a;
            line-height: 1.8;
            text-align: justify;
            margin-bottom: 50px;
            opacity: 0;
            animation: fadeIn 1s ease forwards 1.2s;
        }
        .closing {
            font-family: 'Playfair Display SC', serif;
            font-size: 38px; color: #4a2c2a;
            text-align: right;
            font-style: italic;
            margin-right: 30px;
            opacity: 0;
            animation: fadeIn 1s ease forwards 1.6s;
        }
        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(15px); }
            to { opacity: 1; transform: translateY(0); }
        }

        /* PLAYER CONTAINER */
        .player-container {
            position: fixed; bottom: 20px; right: 20px;
            z-index: 4;
            opacity: 0;
            transition: opacity 0.8s ease 1s;
        }
        .player-container.active {
            opacity: 1;
        }
        #youtube-player {
            width: 150px; height: 90px;
            border: none;
            border-radius: 10px;
            box-shadow: 0 5px 15px rgba(0,0,0,0.5);
        }
        #backup-audio {
            display: none;
            width: 150px;
            margin-top: 10px;
            border-radius: 5px;
        }
    </style>
</head>
<body>
    <div class="table-bg"></div>

    <!-- ENVELOPE -->
    <div id="envelope" onclick="triggerAllActions()">
        <div class="accent acc1"></div>
        <div class="accent acc2"></div>
        <div class="accent acc3"></div>
        <div class="accent acc4"></div>
        <div id="flap"></div>
        <div id="twine"></div>
        <div id="flowers">
            <div class="flower f1"></div>
            <div class="flower f2"></div>
            <div class="flower f3"></div>
        </div>
    </div>

    <!-- FLOATING PAPER - PERMANENTLY VISIBLE AFTER CLICK -->
    <div id="full-letter">
        <p class="greeting">Aking Iniirog</p>
        <p class="message">
            mula pa lamang nang ika'y unang nasilayan ng mga mata ko, isang himala ang naganap sa kaibuturan ng aking puso. Hindi ko sukat akalain na sa isang sulyap lamang, ang aking kaluluwa'y mabibihag ng iyong kariktan. Tila ba sa bawat panaginip, sa bawat pagtatagpo ng mga bituin, ang ating mga palad ay nakatakdang maghawak, ang ating mga puso ay nakatakdang magsanib. Sa bawat sansinukob, sa bawat pagkakataon, ang ating mga kaluluwa'y nakatakdang magtagpo at sa iyo'y humaling.

            Sa aking paningin, ika'y walang kapintasan, bagkus ang bawat di-kasakdalan mo'y siyang nagpapatibay sa aking pagmamahal, sapagkat sa iyong mga pagkakamali, nakikita ko ang iyong tunay na ikaw. Kaya't sa bawat tibok ng puso ko, ang pangalan mo ang siyang sinasambit, aking Iniirog
 
            Sabihin mang dumating ang araw na hindi ko na muling mamamasdan ang iyong ganda, asahan mong hindi ako titigil sa paghahanap, sa paghihintay. Sapagkat kahit ang mundo'y magunaw, ang pag-ibig ko sa iyo'y mananatili magpakailanman. At kung sakali mang ang aking mga mata'y magdilim, hindi ako mangangamba, sapagkat batid ng aking puso kung saan ito titibok. At kahit pa ang alaala'y maglaho, ang damdamin ko'y hindi magbabago.
        </p>
        <p class="closing">
            Maligayang Araw ng mga Puso,<br>
            aking Mahal
        </p>
        p class="ps">
            P.S. Maaari kang manood ng mga video sa YouTube nang walang abala ng mga ad sa pamamagitan ng pag-subscribe sa YouTube Premium, o sa pamamagitan ng mga lehitimong paraan tulad ng paggamit ng embed mode para sa mga partikular na videos 
    </p>
    </div>
    
    <!-- AUDIO PLAYER -->
    <div class="player-container" id="player-container">
        <iframe id="youtube-player" src="" frameborder="0" allow="autoplay; encrypted-media; fullscreen"></iframe>
        <audio id="backup-audio" controls preload="auto">
            <source src="https://www.youtube.com/embed/-57OVjteEQw?autoplay=1" type="audio/mp4">
        
    </div>

    <script>
        // FIXED CODE - PAPEL HINDI NA MAWAWALA
        function triggerAllActions() {
            // Envelope mawawala nang dahan-dahan
            const envelope = document.getElementById('envelope');
            envelope.classList.add('transforming');

            // Ipakita ang sulat/papel PERMANENTE
            const fullLetter = document.getElementById('full-letter');
            fullLetter.style.display = 'block';
            fullLetter.style.position = 'relative'; // Hindi mawawala kahit mag-scroll
            fullLetter.style.zIndex = '10'; // Laging nasa itaas

            // Play song
            const playerContainer = document.getElementById('player-container');
            playerContainer.classList.add('active');
            const youtubePlayer = document.getElementById('youtube-player');
            youtubePlayer.src = 'https://www.youtube.com/embed/-57OVjteEQw?autoplay=1&enablejsapi=1&rel=0';
            
            // Force play commands
            setTimeout(() => {
                youtubePlayer.contentWindow.postMessage('{"event":"command","func":"playVideo","args":""}', '*');
            }, 200);

            // Backup audio
            setTimeout(() => {
                const backupAudio = document.getElementById('backup-audio');
                if (youtubePlayer.contentWindow.document.readyState !== 'complete') {
                    backupAudio.play();
                    youtubePlayer.style.display = 'none';
                    backupAudio.style.display = 'block';
                }
            }, 1000);
        }

        // Initial setup
        window.onload = () => {
            document.getElementById('full-letter').style.display = 'none';
            // Preload players
            document.addEventListener('click', () => {
                document.getElementById('youtube-player').load();
                document.getElementById('backup-audio').load();
            }, { once: true });
        };

        // Iwasan ang pagkawala ng papel kapag nag-scroll
        window.addEventListener('scroll', () => {
            const fullLetter = document.getElementById('full-letter');
            if (fullLetter.style.display === 'block') {
                fullLetter.style.top = '50%';
                fullLetter.style.transform = 'translateY(-50%)';
            }
        });
    </script>
</body>
</html>
