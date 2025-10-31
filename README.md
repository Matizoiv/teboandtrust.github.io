<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>Tebo & Tshephang — GitHub Basics</title>
  <style>
    :root{--bg:#0f1724;--card:#0b1220;--accent:#06b6d4;--muted:#94a3b8;color-scheme:dark}
    html,body{height:100%;margin:0;font-family:Inter,system-ui,Segoe UI,Roboto,'Helvetica Neue',Arial}
    body{background:linear-gradient(180deg,#071024 0%,#07122a 60%);display:flex;align-items:center;justify-content:center;padding:32px}
    .site{width:100%;max-width:1100px;background:linear-gradient(180deg,rgba(255,255,255,0.02),transparent);border-radius:12px;padding:24px;box-shadow:0 10px 30px rgba(2,6,23,0.6)}
    header{display:flex;align-items:center;gap:16px}
    .logo{width:64px;height:64px;border-radius:8px;background:linear-gradient(135deg,var(--accent),#7c3aed);display:flex;align-items:center;justify-content:center;color:#021124;font-weight:700}
    h1{margin:0;font-size:20px}
    .meta{color:var(--muted);font-size:13px}
    .viewer{display:grid;grid-template-columns:1fr 320px;gap:20px;margin-top:20px}
    .slide{background:var(--card);border-radius:10px;padding:28px;min-height:420px;color:#e6eef8;display:flex;flex-direction:column;justify-content:center;align-items:flex-start}
    .slide h2{margin:0 0 12px 0;font-size:28px}
    .slide p{margin:0 0 8px 0;color:var(--muted)}
    .controls{display:flex;gap:8px;margin-top:16px}
    button{background:transparent;border:1px solid rgba(255,255,255,0.06);color:#e6eef8;padding:8px 12px;border-radius:8px;cursor:pointer}
    button.primary{background:var(--accent);border:none;color:#021124}
    aside{background:rgba(255,255,255,0.02);padding:18px;border-radius:10px;color:var(--muted)}
    aside h3{margin-top:0;color:#e6eef8}
    .slide-list{display:flex;flex-direction:column;gap:8px;margin-top:8px}
    .thumb{padding:8px;border-radius:8px;background:rgba(0,0,0,0.25);cursor:pointer}
    footer{margin-top:16px;color:var(--muted);font-size:13px;text-align:center}
    a.link{color:var(--accent);text-decoration:none}
    @media(max-width:900px){.viewer{grid-template-columns:1fr;}.logo{display:none}}
  </style>
</head>
<body>
  <div class="site">
    <header>
      <div class="logo">T&T</div>
      <div>
        <h1>GitHub Basics — Presentation</h1>
        <div class="meta">Group: Tebo & Tshephang · Date: 30 / 10 / 2025</div>
      </div>
    </header>

    <div class="viewer">
      <main>
        <div id="slide" class="slide" role="document" aria-live="polite"></div>

        <div class="controls">
          <button id="prev">◀ Previous</button>
          <button id="next">Next ▶</button>
          <button id="start" class="primary">Start Slideshow</button>
        </div>
      </main>

      <aside>
        <h3>Slides</h3>
        <div class="slide-list" id="slideList"></div>
        <hr style="margin:12px 0;border:none;border-top:1px solid rgba(255,255,255,0.04)">
        <h3>Publish</h3>
        <p>To publish on GitHub Pages: create a repository named <code>teboandtrust.github.io</code>, push these files to the main branch and enable Pages under repository settings.</p>
        <p><strong>Quick commands (git):</strong></p>
        <pre style="background:#071124;padding:8px;border-radius:6px;color:var(--muted);font-size:13px">git init
git add .
git commit -m "initial site"
git branch -M main
git remote add origin &lt;your-repo-url&gt;
git push -u origin main</pre>
        <p class="meta">Site demo address (if repo named properly): <a class="link" href="https://teboandtrust.github.io" target="_blank" rel="noreferrer">teboandtrust.github.io</a></p>
      </aside>
    </div>

    <footer>
      Built from: <strong>Tshephang_and_TeboPPTChallenge.pptx</strong>. Use the canvas file panel to download the site files or copy the code into an <code>index.html</code> file.
    </footer>
  </div>

  <script>
    // Slide data (derived from uploaded PPT)
    const slides = [
      {title: 'Title', lines: ['GitHub Basics','Group: Tebo, Tshephang','Date: 30 / 10 / 2025']},
      {title: 'A Website', lines: ['A Website containing these slides was created and published through GitHub, so we can easily explain it in a more relatable manner.','Accessible through: teboandtrust.github.io']},
      {title: 'What is GitHub?', lines: ['GitHub is a web-based platform for version control using Git.','Hosts repositories (projects) and facilitates collaboration.','Offers features: pull requests, issues, actions, and project boards.']},
      {title: 'What is a Repository?', lines: ['A repository is a storage space for your project.','Contains code, documentation, and history.']},
      {title: 'Why Use Version Control?', lines: ['Track changes, collaborate easily, revert mistakes, and maintain history.']},
      {title: 'Thank You!', lines: ['Q&A','teboandtrust.github.io']}
    ];

    let current = 0;
    const slideEl = document.getElementById('slide');
    const slideList = document.getElementById('slideList');

    function renderSlide(i){
      const s = slides[i];
      slideEl.innerHTML = `<h2>${s.title}</h2>` + s.lines.map(l=>`<p>${l}</p>`).join('');
      document.querySelectorAll('.thumb').forEach((t,idx)=>{t.style.outline = idx===i? '2px solid rgba(6,182,212,0.12)':'none'});
    }

    function buildThumbs(){
      slides.forEach((s,idx)=>{
        const d = document.createElement('div');
        d.className='thumb';
        d.tabIndex = 0;
        d.innerHTML = `<strong>${idx+1}. ${s.title}</strong><div style="font-size:12px;color:var(--muted)">${s.lines[0]||''}</div>`;
        d.addEventListener('click',()=>{current=idx;renderSlide(current)});
        d.addEventListener('keydown',(e)=>{if(e.key==='Enter'){current=idx;renderSlide(current)}});
        slideList.appendChild(d);
      })
    }

    document.getElementById('prev').addEventListener('click',()=>{current = (current-1+slides.length)%slides.length; renderSlide(current)});
    document.getElementById('next').addEventListener('click',()=>{current = (current+1)%slides.length; renderSlide(current)});
    let slideInterval=null;
    document.getElementById('start').addEventListener('click',()=>{
      if(slideInterval){clearInterval(slideInterval);slideInterval=null;document.getElementById('start').textContent='Start Slideshow';return}
      slideInterval=setInterval(()=>{current=(current+1)%slides.length;renderSlide(current)},3000);
      document.getElementById('start').textContent='Stop Slideshow';
    });

    buildThumbs();
    renderSlide(0);

    // Accessibility: keyboard left/right
    document.addEventListener('keydown',(e)=>{
      if(e.key==='ArrowLeft'){current = (current-1+slides.length)%slides.length; renderSlide(current)}
      if(e.key==='ArrowRight'){current = (current+1)%slides.length; renderSlide(current)}
    });
  </script>
</body>
</html>
