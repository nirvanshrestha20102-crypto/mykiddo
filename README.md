<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Be My Valentine?</title>

<link href="https://fonts.googleapis.com/css2?family=Poppins:wght@400;600&display=swap" rel="stylesheet">

<style>
  body {
    margin: 0;
    height: 100vh;
    background: #800020;
    display: flex;
    justify-content: center;
    align-items: center;
    font-family: 'Poppins', sans-serif;
    overflow: hidden;
  }

  .card {
    background: #fff;
    padding: 40px 50px;
    border-radius: 20px;
    text-align: center;
    box-shadow: 0 20px 40px rgba(0,0,0,0.3);
    width: 320px;
    z-index: 2;
  }

  h1 {
    color: #800020;
    margin-bottom: 30px;
  }

  .buttons {
    position: relative;
    height: 80px;
  }

  button {
    padding: 12px 28px;
    border: none;
    border-radius: 30px;
    font-size: 18px;
    cursor: pointer;
    position: absolute;
    transition: transform 0.25s ease;
  }

  #yesBtn {
    background: #800020;
    color: white;
    left: 50%;
    transform: translateX(-120%);
  }

  #noBtn {
    background: #ddd;
    left: 50%;
    transform: translateX(20%);
  }

  .heart {
    position: absolute;
    bottom: -20px;
    animation: floatUp linear infinite;
    opacity: 0.9;
    pointer-events: none;
  }

  @keyframes floatUp {
    from {
      transform: translateY(0) scale(1);
      opacity: 1;
    }
    to {
      transform: translateY(-110vh) scale(1.5);
      opacity: 0;
    }
  }
</style>
</head>

<body>

<div class="card">
  <h1>Will you be my Valentine? 🥺</h1>
  <div class="buttons">
    <button id="yesBtn">Yes 💘</button>
    <button id="noBtn">No 😭</button>
  </div>
</div>

<audio id="crySound">
  <source src="cry.mp3" type="audio/mpeg">
</audio>

<script>
  const noBtn = document.getElementById("noBtn");
  const yesBtn = document.getElementById("yesBtn");
  const crySound = document.getElementById("crySound");

  let noScale = 1;
  let yesScale = 1;

  let baseNoX = 20;
  let baseNoY = 0;

  function moveNoButton() {
    const x = Math.random() * 220 - 110;
    const y = Math.random() * 120 - 60;

    baseNoX = x;
    baseNoY = y;

    noBtn.style.transform = `translate(${x}px, ${y}px) scale(${noScale})`;
  }

  noBtn.addEventListener("mouseenter", moveNoButton);
  noBtn.addEventListener("touchstart", moveNoButton);

  noBtn.addEventListener("click", () => {
    crySound.currentTime = 0;
    crySound.play();

    noScale = Math.max(0.4, noScale - 0.15);
    yesScale += 0.15;

    noBtn.style.transform = `translate(${baseNoX}px, ${baseNoY}px) scale(${noScale})`;
    yesBtn.style.transform = `translateX(-120%) scale(${yesScale})`;
  });

  yesBtn.addEventListener("click", () => {
    document.body.innerHTML = `
      <div style="
        height:100vh;
        width:100%;
        display:flex;
        flex-direction:column;
        justify-content:center;
        align-items:center;
        background:#800020;
        text-align:center;
        color:black;
        font-family:Poppins;
        overflow:hidden;">
       
        <h1 style="font-size:3rem; background:white; padding:30px; border-radius:20px;">
          YAYYY 💖🥰<br><br>
          My Kiddoo!!!🎀<br>
          You’re my Valentineee!!! 💝💕
        </h1>
      </div>
    `;

    createHearts();
  });

  function createHearts() {
    setInterval(() => {
      const heart = document.createElement("div");
      heart.className = "heart";
      heart.innerHTML = "❤️";
      heart.style.left = Math.random() * 100 + "vw";
      heart.style.fontSize = Math.random() * 20 + 20 + "px";
      heart.style.animationDuration = Math.random() * 3 + 4 + "s";
      document.body.appendChild(heart);

      setTimeout(() => heart.remove(), 7000);
    }, 300);
  }
</script>

</body>
</html>
