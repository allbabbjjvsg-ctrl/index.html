<!DOCTYPE html>
<html lang="ro">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Camera Prank 😂</title>

  <style>
    body {
      margin: 0;
      min-height: 100vh;
      display: flex;
      justify-content: center;
      align-items: center;
      background: #111;
      color: white;
      font-family: Arial, sans-serif;
      text-align: center;
    }

    .box {
      width: 90%;
      max-width: 500px;
    }

    video {
      width: 100%;
      border-radius: 15px;
      display: none;
      margin-top: 20px;
    }

    button {
      padding: 15px 25px;
      border: 0;
      border-radius: 10px;
      background: #2196f3;
      color: white;
      font-size: 18px;
      cursor: pointer;
    }

    #result {
      display: none;
      font-size: 40px;
      font-weight: bold;
      margin-top: 30px;
    }
  </style>
</head>

<body>

<div class="box">

  <h1>📸 Camera Prank 😂</h1>

  <p id="text">Apasă butonul pentru a porni camera.</p>

  <button id="start">Pornește camera 📷</button>

  <video id="camera" autoplay playsinline></video>

  <div id="result">😂 TE-AM PRINS! 😂</div>

</div>

<script>
const button = document.getElementById("start");
const video = document.getElementById("camera");
const text = document.getElementById("text");
const result = document.getElementById("result");

button.addEventListener("click", async () => {

  try {
    const stream = await navigator.mediaDevices.getUserMedia({
      video: true
    });

    video.srcObject = stream;
    video.style.display = "block";

    button.style.display = "none";
    text.textContent = "Camera este pornită... 😈";

    setTimeout(() => {

      const canvas = document.createElement("canvas");

      canvas.width = video.videoWidth;
      canvas.height = video.videoHeight;

      const ctx = canvas.getContext("2d");
      ctx.drawImage(video, 0, 0);

      // Poza rămâne doar în browser.
      // Nu este încărcată pe niciun server.

      stream.getTracks().forEach(track => track.stop());

      video.style.display = "none";
      result.style.display = "block";
      text.textContent = "😂 Ai căzut în prank!";

    }, 3000);

  } catch (error) {

    text.textContent =
      "Camera nu a fost permisă. 😅";

    console.error(error);
  }
});
</script>

</body>
</html>
