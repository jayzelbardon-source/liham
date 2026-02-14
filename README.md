<html lang="tl">
<head>
<meta charset="UTF-8">
<title>Aking Liham</title>

<link href="https://fonts.googleapis.com/css2?family=Great+Vibes&family=Playfair+Display:ital,wght@0,400;0,600;1,400&display=swap" rel="stylesheet">

<style>
*{
    margin:0;
    padding:0;
    box-sizing:border-box;
}

body{
    min-height:100vh;
    display:flex;
    justify-content:center;
    align-items:center;
    background:#c2b092;
    font-family:'Playfair Display', serif;
}

/* VINTAGE BACKGROUND */
body::before{
    content:"";
    position:fixed;
    inset:0;
    background:
        radial-gradient(rgba(0,0,0,.12) 1px, transparent 1px),
        radial-gradient(rgba(0,0,0,.08) 1px, transparent 1px);
    background-size:40px 40px;
    opacity:.35;
    z-index:-1;
}

/* ENVELOPE */
#envelope{
    width:420px;
    height:280px;
    background:linear-gradient(#caa472,#b28a58);
    border:1px solid #7a4f26;
    box-shadow:0 18px 35px rgba(0,0,0,.6);
    position:relative;
    cursor:pointer;
}

#flap{
    position:absolute;
    top:0;
    left:0;
    width:100%;
    height:50%;
    background:linear-gradient(#b99361,#9e7543);
    clip-path:polygon(0 0,100% 0,50% 70%);
    transform-origin:top;
    transition:transform 1s ease;
}

#envelope.open #flap{
    transform:rotateX(180deg);
}

/* LETTER */
#letter{
    display:none;
    max-width:900px;
    padding:70px;
    background:#f9f1e6;
    box-shadow:0 30px 60px rgba(0,0,0,.5);
    animation:appear 1.2s ease forwards;
}

@keyframes appear{
    from{
        opacity:0;
        transform:translateY(40px) rotate(-2deg);
    }
    to{
        opacity:1;
        transform:translateY(0) rotate(-1deg);
    }
}

.greeting{
    font-family:'Great Vibes', cursive;
    font-size:54px;
    text-align:left;
    margin-bottom:30px;
}

.message{
    font-size:22px;
    line-height:1.9;
    white-space:pre-wrap; /* IMPORTANT: keeps your text exactly */
}

.closing{
    margin-top:40px;
    text-align:left;
    font-size:24px;
    font-style:italic;
}
</style>
</head>

<body>

<!-- ENVELOPE -->
<div id="envelope" onclick="openLetter()">
    <div id="flap"></div>
</div>

<!-- LETTER -->
<div id="letter">
    <div class="greeting">Aking Iniirog,</div>

    <div class="message">
Aking Iniirog, mula pa lamang nang ika'y unang nasilayan ng mga mata ko, isang himala ang naganap sa kaibuturan ng aking puso. Hindi ko sukat akalain na sa isang sulyap lamang, ang aking kaluluwa'y mabibihag ng iyong kariktan. Tila ba sa bawat panaginip, sa bawat pagtatagpo ng mga bituin, ang ating mga palad ay nakatakdang maghawak, ang ating mga puso ay nakatakdang magsanib. Sa bawat sansinukob, sa bawat pagkakataon, ang ating mga kaluluwa'y nakatakdang magtagpo at sa iyo'y humaling.
 
Sa araw ng mga puso, isang panaginip na ika'y kapiling ko, habang ginugunita natin ang ika-pitong buwan ng ating pagmamahalan. Hindi ko akalain na ang panahon ay kay bilis lumipas, sapagkat una pa lamang, ikaw ay akin lamang pinapangarap. Ako'y lubos na nagpapasalamat sa Poong Maykapal sa pagbibigay sa akin ng isang anghel na katulad mo, at sa bawat araw na ikaw ay aking kapiling, ang puso ko'y napupuno ng walang kapantay na ligaya.
 
Sabihin mang dumating ang araw na hindi ko na muling mamamasdan ang iyong ganda, asahan mong hindi ako titigil sa paghahanap, sa paghihintay. Sapagkat kahit ang mundo'y magunaw, ang pag-ibig ko sa iyo'y mananatili magpakailanman. At kung sakali mang ang aking mga mata'y magdilim, hindi ako mangangamba, sapagkat batid ng aking puso kung saan ito titibok, tanda ko pa rin ang iyong tinig at ang iyong bango. At kahit pa ang alaala'y maglaho, ang damdamin ko'y hindi magbabago, sapagkat ikaw ang tanda ng aking puso. Sa aking paningin, ika'y walang kapintasan, bagkus ang bawat di-kasakdalan mo'y siyang nagpapatibay sa aking pagmamahal, sapagkat sa iyong mga pagkakamali, nakikita ko ang iyong tunay na puso. Kaya't sa bawat tibok ng puso ko, ang pangalan mo ang siyang sinasambit, aking Iniirog.

    </div>
</div>

<script>
function openLetter(){
    document.getElementById("envelope").classList.add("open");

    setTimeout(()=>{
        document.getElementById("envelope").style.display="none";
        document.getElementById("letter").style.display="block";
    },1000);
}
</script>

</body>
</html>
