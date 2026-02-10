<html>
<head>
    <title>Aking Liham - Vintage Maria Clara</title>
    <link href="https://fonts.googleapis.com/css2?family=Great+Vibes&family=Playfair+Display+SC:ital,wght@0,400;0,700;1,400&family=Sacramento&display=swap" rel="stylesheet">
    <style>
        * { margin:0; padding:0; box-sizing:border-box; }
        body {
            background: #f5e6d1; /* soft vintage paper color */
            min-height: 100vh;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            font-family: serif;
            overflow-x: hidden;
        }

        /* ENVELOPE */
        #envelope {
            width: 420px;
            height: 280px;
            background: #c49f72;
            border: 1px solid #8b5a2b;
            border-radius: 8px;
            box-shadow: 0 15px 35px rgba(0,0,0,0.6);
            cursor: pointer;
            z-index: 2;
            position: relative;
            transition: transform 1s ease;
            background-image: 
                linear-gradient(rgba(255,255,255,0.03) 1px, transparent 1px),
                linear-gradient(90deg, rgba(255,255,255,0.03) 1px, transparent 1px);
            background-size: 20px 20px;
        }

        /* ENVELOPE FLAP */
        #flap {
            position: absolute;
            top: 0; left: 0;
            width: 100%; height: 50%;
            background: #b58d60;
            border-bottom: 1px solid #8b5a2b;
            border-radius: 8px 8px 0 0;
            transform-origin: top center;
            transition: transform 1s ease-in-out;
            clip-path: polygon(0 0, 100% 0, 50% 60%);
            box-shadow: inset -2px -2px 5px rgba(0,0,0,0.2);
        }

        #envelope.open #flap {
            transform: rotateX(180deg);
        }

        /* LETTER */
        #letter {
            display: none;
            max-width: 850px;
            width: 90%;
            padding: 50px 60px;
            background: #fcf4e5; /* antique paper color */
            border-radius: 4px;
            box-shadow: 0 25px 50px rgba(0,0,0,0.4);
            z-index: 3;
            position: relative;
            animation: floatPaper 6s ease-in-out infinite;
            font-size: 1.1em;
        }

        @keyframes floatPaper {
            0% { transform: translateY(0) rotate(-1deg); }
            25% { transform: translateY(-5px) rotate(0.5deg); }
            50% { transform: translateY(-10px) rotate(0deg); }
            75% { transform: translateY(-5px) rotate(0.5deg); }
            100% { transform: translateY(0) rotate(-1deg); }
        }

        /* CALLIGRAPHY TEXT */
        .greeting {
            font-family: 'Sacramento', cursive;
            font-size: 58px;
            color: #4a2c2a;
            text-align: center;
            margin-bottom: 35px;
        }
        .message {
            font-family: 'Great Vibes', cursive;
            font-size: 28px;
            line-height: 1.8;
            color: #4a2c2a;
            margin-bottom: 45px;
            text-align: justify;
        }
        .closing {
            font-family: 'Playfair Display SC', serif;
            font-size: 38px;
            text-align: right;
            color: #4a2c2a;
            font-style: italic;
        }

        /* HIDDEN AUDIO */
        #bg-music {
            display: none;
        }
    </style>
</head>
<body>

    <!-- ENVELOPE -->
    <div id="envelope" onclick="openLetter()">
        <div id="flap"></div>
    </div>

    <!-- LETTER CONTENT -->
    <div id="letter">
        <p class="greeting">Aking Iniirog</p>
        <p class="message">
            Mula pa lamang nang ika'y unang nasilayan ng aking mga mata, isang himala ang naganap sa kaibuturan ng aking puso. Hindi ko sukat akalain na sa isang sulyap lamang, ang aking kaluluwa'y mabibihag ng iyong kariktan. Tila ba sa bawat panaginip, sa bawat pagtatagpo ng mga bituin, ang ating mga palad ay nakatakdang maghawak, ang ating mga puso ay nakatakdang magsanib. Sa bawat sansinukob, sa bawat pagkakataon, ang ating mga kaluluwa'y nakatakdang magtagpo at sa iyo'y humaling.

            Sa aking paningin, ika'y walang kapintasan, bagkus ang bawat di-kasakdalan mo'y siyang nagpapatibay sa aking pagmamahal, sapagkat sa iyong mga pagkakamali, nakikita ko ang iyong tunay na ikaw. Kaya't sa bawat tibok ng puso ko, ang pangalan mo ang siyang sinasambit, aking Iniirog.

            Sabihin mang dumating ang araw na hindi ko na muling mamamasdan ang iyong ganda, asahan mong hindi ako titigil sa paghahanap, sa paghihintay. Sapagkat kahit ang mundo'y magunaw, ang pag-ibig ko sa iyo'y mananatili magpakailanman. At kung sakali mang ang aking mga mata'y magdilim, hindi ako mangangamba, sapagkat batid ng aking puso kung saan ito titibok. At kahit pa ang alaala'y maglaho, ang damdamin ko'y hindi magbabago.
        </p>
        <p class="closing">
            Maligayang Araw ng mga Puso,<br>aking Mahal
        </p>

        <!-- HIDDEN AUDIO -->
        <audio id="bg-music" src="https://freesound.org/data/previews/647/647856_12411833-lq.mp3" preload="auto"></audio>
    </div>

    <script>
        function openLetter() {
            document.getElementById('envelope').classList.add('open');
            setTimeout(() => {
                document.getElementById('envelope').style.display = 'none';
                document.getElementById('letter').style.display = 'block';

                // Play music only when envelope is clicked
                const audio = document.getElementById('bg-music');
                audio.play();
            }, 900);
        }
    </script>

</body>
</html>
