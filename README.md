# Image-Gallery

<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Responsive Image Gallery</title>
  <link rel="stylesheet" href="style.css" />
</head>
<body>

  <header>
    <h1>Image Gallery</h1>
    <div class="filters">
      <button onclick="filterImages('all')">All</button>
      <button onclick="filterImages('nature')">Nature</button>
      <button onclick="filterImages('city')">City</button>
    </div>
  </header>

  <main class="gallery">
    <!-- Images with categories -->
    <div class="image nature">
      <img src="images/nature1.jpg" alt="Nature 1" onclick="openLightbox(this)" />
    </div>
    <div class="image city">
      <img src="images/city1.jpg" alt="City 1" onclick="openLightbox(this)" />
    </div>
    <!-- Add more images here with class 'nature' or 'city' -->
  </main>

  <!-- Lightbox view -->
  <div id="lightbox" class="lightbox" onclick="closeLightbox()">
    <span class="close">&times;</span>
    <img class="lightbox-content" id="lightbox-img" />
    <div class="nav">
      <button onclick="prevImage(event)">❮</button>
      <button onclick="nextImage(event)">❯</button>
    </div>
  </div>

  <script src="script.js"></script>
</body>
</html>

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  font-family: sans-serif;
  background: #f4f4f4;
  color: #333;
}

header {
  text-align: center;
  padding: 20px;
  background-color: #222;
  color: white;
}

.filters {
  margin-top: 10px;
}

.filters button {
  padding: 8px 16px;
  margin: 0 5px;
  background: #fff;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  transition: 0.3s;
}

.filters button:hover {
  background: #ddd;
}

.gallery {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  gap: 15px;
  padding: 20px;
}

.image img {
  width: 100%;
  height: auto;
  border-radius: 10px;
  cursor: pointer;
  transition: transform 0.3s ease;
}

.image img:hover {
  transform: scale(1.05);
}

/* Lightbox */
.lightbox {
  display: none;
  position: fixed;
  z-index: 100;
  top: 0; left: 0; right: 0; bottom: 0;
  background: rgba(0, 0, 0, 0.9);
  justify-content: center;
  align-items: center;
  flex-direction: column;
}

.lightbox-content {
  max-width: 90%;
  max-height: 80vh;
  margin: 20px;
  border-radius: 10px;
}

.close {
  position: absolute;
  top: 20px;
  right: 40px;
  font-size: 30px;
  color: white;
  cursor: pointer;
}

.nav {
  display: flex;
  gap: 20px;
}

.nav button {
  padding: 10px 20px;
  font-size: 24px;
  background: white;
  border: none;
  border-radius: 5px;
  cursor: pointer;
}

@media (max-width: 600px) {
  .filters {
    display: flex;
    flex-direction: column;
    align-items: center;
  }

  .filters button {
    margin: 5px 0;
  }
}

const lightbox = document.getElementById("lightbox");
const lightboxImg = document.getElementById("lightbox-img");
let currentIndex = 0;
let images = [];

document.addEventListener("DOMContentLoaded", () => {
  images = Array.from(document.querySelectorAll(".gallery .image img"));
});

// Lightbox
function openLightbox(img) {
  lightbox.style.display = "flex";
  lightboxImg.src = img.src;
  currentIndex = images.findIndex(i => i.src === img.src);
}

function closeLightbox() {
  lightbox.style.display = "none";
}

function nextImage(event) {
  event.stopPropagation();
  currentIndex = (currentIndex + 1) % images.length;
  lightboxImg.src = images[currentIndex].src;
}

function prevImage(event) {
  event.stopPropagation();
  currentIndex = (currentIndex - 1 + images.length) % images.length;
  lightboxImg.src = images[currentIndex].src;
}

// Filtering
function filterImages(category) {
  const allImages = document.querySelectorAll(".gallery .image");
  allImages.forEach(img => {
    if (category === 'all' || img.classList.contains(category)) {
      img.style.display = "block";
    } else {
      img.style.display = "none";
    }
  });
}
