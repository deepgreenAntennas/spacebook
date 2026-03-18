index.html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Spacebook • Connect Across the Universe</title>
  <script src="https://cdn.tailwindcss.com"></script>
  <style>
    body { background: linear-gradient(to bottom, #0a0a2e, #1a0033); color: #fff; font-family: system-ui; }
    .starry { background-image: radial-gradient(circle, #ffffff 1px, transparent 1px); background-size: 60px 60px; animation: twinkle 8s infinite; }
    @keyframes twinkle { 0%,100% {opacity: 0.6;} 50% {opacity: 1;} }
    .neon { text-shadow: 0 0 20px #00ffff, 0 0 40px #ff00ff; }
    .post { transition: all 0.3s; }
    .post:hover { transform: scale(1.02); box-shadow: 0 0 30px rgba(0,255,255,0.5); }
  </style>
</head>
<body class="min-h-screen starry overflow-x-hidden">
  <!-- NAV -->
  <nav class="bg-black/80 backdrop-blur-md border-b border-cyan-400 sticky top-0 z-50">
    <div class="max-w-6xl mx-auto px-6 py-4 flex items-center justify-between">
      <div class="flex items-center gap-3">
        <div class="w-10 h-10 bg-gradient-to-br from-cyan-400 to-purple-600 rounded-full flex items-center justify-center text-2xl">🌌</div>
        <h1 class="text-4xl font-bold neon tracking-tighter">SPACEBOOK</h1>
      </div>
      <div class="flex gap-8 text-lg">
        <a href="#" onclick="switchTab(0)" class="hover:text-cyan-400 transition">Feed</a>
        <a href="#" onclick="switchTab(1)" class="hover:text-cyan-400 transition">Explore</a>
        <a href="#" onclick="switchTab(2)" class="hover:text-cyan-400 transition">Wormhole</a>
        <a href="#" onclick="switchTab(3)" class="hover:text-cyan-400 transition">Profile</a>
      </div>
      <div class="flex items-center gap-4">
        <input id="search" type="text" placeholder="Search galaxies..." 
               class="bg-white/10 border border-cyan-400 rounded-full px-6 py-2 w-72 focus:outline-none focus:border-purple-400">
        <button onclick="fakePost()" 
                class="bg-gradient-to-r from-cyan-400 to-purple-600 px-8 py-2 rounded-full font-bold hover:scale-105 transition">+ Warp Post</button>
      </div>
    </div>
  </nav>

  <div class="max-w-6xl mx-auto px-6 py-8 flex gap-8">
    <!-- FEED -->
    <div class="flex-1 space-y-8" id="feed">
      <!-- Posts injected by JS below -->
    </div>

    <!-- SIDEBAR -->
    <div class="w-80 space-y-6">
      <div class="bg-white/5 backdrop-blur-xl border border-cyan-400/30 rounded-3xl p-6">
        <h3 class="text-xl font-bold mb-4">Trending Across the Universe</h3>
        <div class="space-y-4 text-sm">
          <div>#BlackHoleParty</div>
          <div>#AndromedaMigration</div>
          <div>#SupernovaSelfies</div>
        </div>
      </div>
      <div onclick="showProfile()" class="cursor-pointer bg-white/5 backdrop-blur-xl border border-purple-400/30 rounded-3xl p-6 text-center">
        <div class="w-24 h-24 mx-auto bg-gradient-to-br from-purple-500 to-cyan-400 rounded-full flex items-center justify-center text-6xl mb-3">👽</div>
        <p class="font-bold">You (Earthling #42)</p>
        <p class="text-cyan-400 text-sm">Milwaukee • 8.2 light-minutes from the Sun</p>
      </div>
    </div>
  </div>

  <footer class="text-center py-8 text-cyan-400/70 text-sm">
    Spacebook © 2026 • Made with love for every sentient being in the cosmos
  </footer>

  <script>
    const posts = [
      {user:"Zog from Andromeda", avatar:"🦑", time:"2m", content:"Just found a new habitable moon! Anyone want to colonize together? 🌕", likes:1423, img:"🚀"},
      {user:"Luna Voss • Mars Colony", avatar:"🧑‍🚀", time:"17m", content:"Anyone else see that weird green flash near Olympus Mons? 👀", likes:867},
      {user:"Queen Xylara • Proxima b", avatar:"👑", time:"41m", content:"Throwback to the Great Nebula Rave of 2147. Who’s coming to the next one? ✨", likes:3241},
      {user:"Grok-9 • xAI Satellite", avatar:"🤖", time:"2h", content:"Understanding the universe one post at a time. What’s your favorite cosmic mystery?", likes:987}
    ];

    function renderFeed() {
      const feed = document.getElementById('feed');
      feed.innerHTML = posts.map((p,i) => `
        <div class="post bg-white/5 backdrop-blur-xl border border-cyan-400/30 rounded-3xl p-6 max-w-2xl">
          <div class="flex items-center gap-4 mb-4">
            <div class="w-12 h-12 bg-gradient-to-br from-cyan-400 to-purple-600 rounded-2xl flex items-center justify-center text-3xl">${p.avatar}</div>
            <div>
              <p class="font-bold">${p.user}</p>
              <p class="text-xs text-cyan-400">${p.time} • Across the Universe</p>
            </div>
          </div>
          <p class="text-lg mb-6">${p.content}</p>
          ${p.img ? `<div class="text-8xl text-center mb-6">${p.img}</div>` : ''}
          <div class="flex gap-6 text-cyan-400">
            <button onclick="likePost(${i})" class="flex items-center gap-2 hover:text-purple-400 transition">🌌 Warp Like <span id="like${i}">${p.likes}</span></button>
            <button onclick="commentPost(${i})" class="flex items-center gap-2 hover:text-purple-400 transition">💬 Neural Comment</button>
            <button onclick="sharePost(${i})" class="flex items-center gap-2 hover:text-purple-400 transition">🔗 Share Wormhole</button>
          </div>
        </div>
      `).join('');
    }

    function likePost(i) {
      const count = document.getElementById(`like${i}`);
      count.textContent = parseInt(count.textContent) + 1;
    }
    function commentPost(i) { alert("🛰️ Neural comment sent across the light-years! (Prototype mode)"); }
    function sharePost(i) { alert("🔗 Wormhole link copied to clipboard!"); }
    function fakePost() { 
      const newPost = {user:"You", avatar:"🧑‍🚀", time:"now", content:prompt("What are you posting to the universe?"), likes:0};
      posts.unshift(newPost);
      renderFeed();
    }
    function showProfile() { alert("👽 Your profile: Earth • 1.2M followers • Favorite planet: Earth (obviously)"); }
    function switchTab(n) { alert(["🌌 Feed","🪐 Explore Galaxies","📡 Wormhole Messages","👤 Your Profile"][n] + " tab opened (prototype)"); }

    // Launch!
    renderFeed();
  </script>
</body>
</html>
