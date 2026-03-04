# Abem
design-assets-site
 ├── index.html
 ├── css/style.css
 └── js/
      ├── assets.js
      └── script.js
      <!DOCTYPE html>
<html>
<head>
  <meta charset="UTF-8">
  <title>Design Assets Hub</title>
  <link rel="stylesheet" href="css/style.css">
</head>
<body>

<header>
  <h1>Design Assets Hub</h1>
  <div class="header-right">
    <input type="text" id="searchInput" placeholder="Search assets...">
    <button id="themeToggle">🌙</button>
  </div>
</header>

<div class="categories">
  <button onclick="filterCategory('all')">All</button>
  <button onclick="filterCategory('ui')">UI Kits</button>
  <button onclick="filterCategory('icons')">Icons</button>
  <button onclick="filterCategory('mockups')">Mockups</button>
</div>

<div class="container" id="assetContainer">
</div>

<div class="ad-box">
  <p>Advertisement</p>
</div>

<script src="js/assets.js"></script>
<script src="js/script.js"></script>

</body>
</html>
const assets = [
  {
    id: 1,
    name: "Modern UI Kit",
    category: "ui",
    version: "1.2",
    downloads: 0,
    file: "#"
  },
  {
    id: 2,
    name: "Minimal Icon Pack",
    category: "icons",
    version: "2.0",
    downloads: 0,
    file: "#"
  },
  {
    id: 3,
    name: "Product Mockup Set",
    category: "mockups",
    version: "1.5",
    downloads: 0,
    file: "#"
  }
];
const container = document.getElementById("assetContainer");
const searchInput = document.getElementById("searchInput");
const themeToggle = document.getElementById("themeToggle");

// Render assets
function renderAssets(list) {
  container.innerHTML = "";
  list.forEach(asset => {
    container.innerHTML += `
      <div class="asset-card">
        <h2>${asset.name}</h2>
        <p>Version ${asset.version}</p>
        <p>Downloads: ${asset.downloads}</p>
        <button onclick="downloadAsset(${asset.id})">Download</button>
      </div>
    `;
  });
}

renderAssets(assets);

// Search
searchInput.addEventListener("input", function() {
  const value = this.value.toLowerCase();
  const filtered = assets.filter(asset =>
    asset.name.toLowerCase().includes(value)
  );
  renderAssets(filtered);
});

// Category filter
function filterCategory(category) {
  if (category === "all") {
    renderAssets(assets);
  } else {
    const filtered = assets.filter(asset =>
      asset.category === category
    );
    renderAssets(filtered);
  }
}

// Fake download counter (local)
function downloadAsset(id) {
  const asset = assets.find(a => a.id === id);
  asset.downloads++;
  renderAssets(assets);
}

// Dark mode
if (localStorage.getItem("theme") === "dark") {
  document.body.classList.add("dark");
}

themeToggle.addEventListener("click", () => {
  document.body.classList.toggle("dark");
  localStorage.setItem(
    "theme",
    document.body.classList.contains("dark") ? "dark" : "light"
  );
});
:root {
  --bg: #ffffff;
  --text: #111111;
  --card: #f2f2f2;
}

body.dark {
  --bg: #111111;
  --text: #ffffff;
  --card: #1e1e1e;
}

body {
  margin: 0;
  font-family: Arial, sans-serif;
  background: var(--bg);
  color: var(--text);
  transition: 0.3s;
}

header {
  display: flex;
  justify-content: space-between;
  padding: 20px;
  align-items: center;
}

.header-right {
  display: flex;
  gap: 10px;
}

input {
  padding: 8px;
  border-radius: 6px;
  border: 1px solid #ccc;
}

.categories {
  padding: 0 20px;
}

.categories button {
  margin-right: 10px;
  padding: 8px 12px;
  border-radius: 6px;
  border: none;
  cursor: pointer;
}

.container {
  padding: 20px;
}

.asset-card {
  background: var(--card);
  padding: 20px;
  border-radius: 12px;
  margin-bottom: 20px;
}

button {
  padding: 8px 12px;
  border: none;
  border-radius: 6px;
  cursor: pointer;
}

.ad-box {
  margin: 40px 20px;
  padding: 20px;
  text-align: center;
  background: #ececec;
}
