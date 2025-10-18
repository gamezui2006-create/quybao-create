<!DOCTYPE html>
<html lang="vi">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Troll vui 😜</title>
<style>
  body {
    background: black;
    overflow: hidden;
    margin: 0;
  }
  .text {
    position: absolute;
    font-size: 40px;
    font-family: 'Comic Sans MS', sans-serif;
    animation: move 3s linear infinite;
  }
  @keyframes move {
    0% { transform: translate(0,0) rotate(0deg); color: red; }
    25% { transform: translate(50vw, 20vh) rotate(90deg); color: yellow; }
    50% { transform: translate(10vw, 60vh) rotate(180deg); color: lime; }
    75% { transform: translate(80vw, 30vh) rotate(270deg); color: cyan; }
    100% { transform: translate(0,0) rotate(360deg); color: magenta; }
  }
</style>
</head>
<body>
<script>
  alert("Troll nhẹ thôi nha 😆");
  const names = ["Minh Hưng", "Gia Hưng", "Quốc An"];
  for (let i = 0; i < names.length; i++) {
    const span = document.createElement("span");
    span.className = "text";
    span.style.top = Math.random() * 80 + "vh";
    span.style.left = Math.random() * 80 + "vw";
    span.textContent = names[i] + " bị troll 😜";
    span.style.animationDelay = i + "s";
    document.body.appendChild(span);
  }
</script>
</body>
</html>
