<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Al-Joker Net</title>
  <style>
    body { margin:0; font-family:Tahoma, sans-serif; background:#0b0b0d; color:#fff; }
    header { background:#1a1a24; padding:1rem 2rem; display:flex; justify-content:space-between; align-items:center; flex-wrap:wrap; }
    header h1 { color:#a64ca6; margin:0; font-size:1.5rem; }
    nav { display:flex; align-items:center; gap:0.5rem; }
    nav a { color:#fff; margin:0 0.5rem; text-decoration:none; }
    nav a:hover { color:#a64ca6; }
    .search-box { position:relative; }
    .search-box input { padding:0.4rem 0.8rem; border-radius:6px; border:none; outline:none; }
    .search-box button { position:absolute; top:0; right:0; bottom:0; background:#a64ca6; color:#fff; border:none; border-radius:0 6px 6px 0; padding:0 0.8rem; cursor:pointer; }
    .search-box button:hover { background:#832d83; }

    .section { padding:1rem 2rem; }
    .section h2 { color:#a64ca6; margin-bottom:0.5rem; }
    .cards { display:grid; grid-template-columns:repeat(auto-fill,minmax(150px,1fr)); gap:1rem; }
    .card { background:#1e1e29; border-radius:12px; overflow:hidden; box-shadow:0 2px 8px rgba(0,0,0,0.5); cursor:pointer; }
    .card img { width:100%; display:block; }
    .card .info { padding:0.5rem; }
    .about { padding:2rem; background:#1a1a24; text-align:center; line-height:1.8; }
    footer { text-align:center; padding:1rem; background:#1a1a24; font-size:0.9rem; color:#aaa; }

    /* مشغّل الفيديو */
    .overlay { position:fixed; top:0; left:0; width:100%; height:100%; background:rgba(0,0,0,0.9); display:none; align-items:center; justify-content:center; flex-direction:column; z-index:1000; }
    .overlay video { width:80%; max-width:800px; border:4px solid #a64ca6; border-radius:12px; margin-bottom:1rem; }
    .overlay .close { position:absolute; top:20px; right:30px; font-size:2rem; color:#fff; cursor:pointer; }
    .overlay .controls { display:flex; gap:1rem; flex-wrap:wrap; justify-content:center; }
    .overlay .btn { background:#a64ca6; color:#fff; padding:0.5rem 1rem; border:none; border-radius:8px; cursor:pointer; text-decoration:none; font-size:1rem; }
    .overlay .btn:hover { background:#832d83; }

    /* إخفاء البطاقات غير المطابقة للبحث */
    .hidden { display:none !important; }
  </style>
</head>
<body>
  <header>
    <h1>🎬 Al-Joker Net</h1>
    <nav>
      <a href="#home">الرئيسية</a>
      <a href="#movies">أفلام</a>
      <a href="#series">مسلسلات</a>
      <a href="#about">حول</a>
      <div class="search-box">
        <input type="text" id="searchInput" placeholder="ابحث عن فيلم أو مسلسل...">
        <button onclick="searchContent()">🔍</button>
      </div>
    </nav>
  </header>

  <main>
    <section id="home" class="section">
      <h2>الأكثر مشاهدة</h2>
      <div class="cards">
        <div class="card" data-title="فيلم الأكشن 1" onclick="openPlayer(['sample1.mp4','backup1.mp4'])">
          <img src="https://via.placeholder.com/200x300" alt="Movie 1">
          <div class="info">فيلم الأكشن 1</div>
        </div>
        <div class="card" data-title="مسلسل الدراما 2" onclick="openPlayer(['sample2.mp4','backup2.mp4'])">
          <img src="https://via.placeholder.com/200x300" alt="Movie 2">
          <div class="info">مسلسل الدراما 2</div>
        </div>
      </div>
    </section>

    <section class="section">
      <h2>جديد على الموقع</h2>
      <div class="cards">
        <div class="card" data-title="فيلم الكوميديا 3" onclick="openPlayer(['sample3.mp4','backup3.mp4'])">
          <img src="https://via.placeholder.com/200x300" alt="Movie 3">
          <div class="info">فيلم الكوميديا 3</div>
        </div>
        <div class="card" data-title="مسلسل الأكشن 4" onclick="openPlayer(['sample4.mp4','backup4.mp4'])">
          <img src="https://via.placeholder.com/200x300" alt="Movie 4">
          <div class="info">مسلسل الأكشن 4</div>
        </div>
      </div>
    </section>

    <section id="movies" class="section">
      <h2>أفلام</h2>
      <div class="cards">
        <div class="card" data-title="فيلم إثارة" onclick="openPlayer(['sample5.mp4','backup5.mp4'])">
          <img src="https://via.placeholder.com/200x300" alt="Movie 5">
          <div class="info">فيلم إثارة</div>
        </div>
      </div>
    </section>

    <section id="series" class="section">
      <h2>مسلسلات</h2>
      <div class="cards">
        <div class="card" data-title="مسلسل خيال علمي" onclick="openPlayer(['sample6.mp4','backup6.mp4'])">
          <img src="https://via.placeholder.com/200x300" alt="Series 1">
          <div class="info">مسلسل خيال علمي</div>
        </div>
      </div>
    </section>

    <section id="about" class="about">
      <h2>حول Al-Joker Net</h2>
      <p>
        مرحبًا بك في <strong>Al-Joker Net</strong> — منصتك لمشاهدة أحدث وأفضل الأفلام والمسلسلات بجودة عالية.
        هدفنا هو توفير تجربة سلسة، ممتعة، وسهلة الاستخدام لكل عشاق السينما والتلفاز.
      </p>
    </section>
  </main>

  <!-- نافذة المشغّل -->
  <div id="videoOverlay" class="overlay">
    <span class="close" onclick="closePlayer()">&times;</span>
    <video id="videoPlayer" controls>
      <source id="videoSource" src="" type="video/mp4">
      متصفحك لا يدعم تشغيل الفيديو.
    </video>
    <div id="serverButtons" class="controls"></div>
    <div class="controls">
      <a id="downloadLink" href="#" download class="btn">⬇️ تحميل</a>
    </div>
  </div>

  <footer>
    © 2025 Al-Joker Net - جميع الحقوق محفوظة
  </footer>

  <script>
    function openPlayer(sources) {
      document.getElementById('videoSource').src = sources[0];
      document.getElementById('videoPlayer').load();
      document.getElementById('downloadLink').href = sources[0];

      const serverButtons = document.getElementById('serverButtons');
      serverButtons.innerHTML = '';
      sources.forEach((src, i) => {
        const btn = document.createElement('button');
        btn.innerText = 'السيرفر ' + (i+1);
        btn.className = 'btn';
        btn.onclick = () => switchServer(src);
        serverButtons.appendChild(btn);
      });

      document.getElementById('videoOverlay').style.display = 'flex';
    }

    function switchServer(src) {
      document.getElementById('videoSource').src = src;
      document.getElementById('videoPlayer').load();
      document.getElementById('downloadLink').href = src;
      document.getElementById('videoPlayer').play();
    }

    function closePlayer() {
      document.getElementById('videoOverlay').style.display = 'none';
      document.getElementById('videoPlayer').pause();
    }

    function searchContent() {
      const query = document.getElementById('searchInput').value.toLowerCase();
      const cards = document.querySelectorAll('.card');
      cards.forEach(card => {
        const title = card.getAttribute('data-title').toLowerCase();
        if(title.includes(query) || query === '') {
          card.classList.remove('hidden');
        } else {
          card.classList.add('hidden');
        }
      });
    }
  </script>
</body>
</html>
