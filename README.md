<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Synced Multiple Screens</title>
  <style>
    .container {
      display: grid;
      grid-template-columns: repeat(2, 1fr);
      gap: 10px;
      padding: 20px;
    }
    video {
      width: 100%;
      border: 2px solid black;
    }
  </style>
</head>
<body>

  <!-- Hidden original video -->
  <video id="mainVideo" src="your-video.mp4" muted autoplay loop playsinline style="display:none;"></video>

  <!-- Clone displays -->
  <div class="container">
    <video id="v1" muted autoplay loop playsinline></video>
    <video id="v2" muted autoplay loop playsinline></video>
    <video id="v3" muted autoplay loop playsinline></video>
    <video id="v4" muted autoplay loop playsinline></video>
  </div>

  <script>
    const mainVideo = document.getElementById("mainVideo");

    const clones = [
      document.getElementById("v1"),
      document.getElementById("v2"),
      document.getElementById("v3"),
      document.getElementById("v4")
    ];

    // Wait for main video to be ready
    mainVideo.addEventListener('canplay', () => {
      clones.forEach(clone => {
        clone.srcObject = mainVideo.captureStream();
        clone.play();
      });
    });
  </script>
</body>
</html>
