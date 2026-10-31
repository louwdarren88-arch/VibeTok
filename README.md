
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>VibeTok</title>

<style>
* {
  box-sizing: border-box;
}

body {
  margin: 0;
  background: #101010;
  color: white;
  font-family: Arial, sans-serif;
  text-align: center;
}

header {
  padding: 20px;
  color: #ff286b;
  font-size: 32px;
  font-weight: bold;
}

button {
  background: #ff286b;
  color: white;
  border: none;
  padding: 14px 25px;
  border-radius: 25px;
  font-size: 17px;
  cursor: pointer;
  margin: 10px;
}

#welcome {
  padding: 70px 20px;
}

#app {
  display: none;
  padding-bottom: 40px;
}

.video {
  margin: 20px auto;
  max-width: 420px;
  min-height: 300px;
  background: #222;
  border-radius: 15px;
  padding: 15px;
}

video {
  width: 100%;
  max-height: 500px;
  border-radius: 12px;
  background: black;
}

input {
  display: none;
}

#videoList {
  padding: 10px;
}
</style>
</head>

<body>

<header>❤️ VibeTok</header>

<div id="welcome">
  <h1>Welcome to VibeTok!</h1>
  <p>Share your world. Share your vibe.</p>
  <button onclick="startApp()">Get Started</button>
</div>

<div id="app">

  <h2>Your Video Feed</h2>

  <button onclick="document.getElementById('upload').click()">
    + Upload Video
  </button>

  <input
    type="file"
    id="upload"
    accept="video/*"
    onchange="playVideo(event)"
  >

  <div id="videoList"></div>

  <button onclick="backHome()">Home</button>

</div>

<script>

function startApp() {
  document.getElementById("welcome").style.display = "none";
  document.getElementById("app").style.display = "block";
}

function playVideo(event) {
  const file = event.target.files[0];

  if (!file) return;

  if (!file.type.startsWith("video/")) {
    alert("Please choose a video.");
    return;
  }

  const videoURL = URL.createObjectURL(file);

  const container = document.createElement("div");
  container.className = "video";

  const video = document.createElement("video");
  video.src = videoURL;
  video.controls = true;
  video.autoplay = true;

  const like = document.createElement("button");
  like.textContent = "❤️ Like";

  let liked = false;

  like.onclick = function() {
    liked = !liked;
    like.textContent = liked ? "❤️ Liked" : "❤️ Like";
  };

  container.appendChild(video);
  container.appendChild(like);

  document.getElementById("videoList")
    .prepend(container);

  event.target.value = "";
}

function backHome() {
  document.getElementById("app").style.display = "none";
  document.getElementById("welcome").style.display = "block";
}

</script>

</body>
</html>

