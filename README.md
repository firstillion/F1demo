<?xml version="1.0" encoding="UTF-8" ?>
<html xmlns='http://www.w3.org/1999/xhtml' xmlns:b='http://www.google.com/2005/gml/b' xmlns:data='http://www.google.com/2005/gml/data' xmlns:expr='http://www.google.com/2005/gml/expr'>
<head>
<meta charset='UTF-8'/>
<meta content='width=device-width, initial-scale=1.0, viewport-fit=cover' name='viewport'/>
<title><data:blog.pageTitle/></title>
<link href='https://fonts.googleapis.com/css2?family=Fraunces:ital,opsz,wght@0,9..144,600;0,9..144,700;1,9..144,600&amp;family=Work+Sans:wght@400;500;600;700&amp;display=swap' rel='stylesheet'/>
<b:skin><![CDATA[
body{margin:0;padding:0;}
]]></b:skin>
<style>
  :root{
    --bg:#0a0a0e;
    --panel:#141319;
    --ink:#f2eee6;
    --dim:#9a93a6;
    --accent:#e8a34c;
  }
  *{box-sizing:border-box;-webkit-tap-highlight-color:transparent;}
  html,body{height:100%;background:var(--bg);color:var(--ink);font-family:'Work Sans',sans-serif;overscroll-behavior:none;}
  .app{max-width:480px;margin:0 auto;position:relative;height:100dvh;overflow:hidden;background:var(--bg);}

  /* top bar */
  .topbar{position:absolute;top:0;left:0;right:0;z-index:30;display:flex;align-items:center;
    justify-content:space-between;padding:14px 18px;background:linear-gradient(180deg,rgba(10,10,14,.92),transparent);}
  .logo{font-family:'Fraunces',serif;font-weight:700;font-size:1.2rem;display:flex;align-items:center;gap:7px;}
  .logo .dot{width:7px;height:7px;border-radius:50%;background:var(--accent);}

  /* tab panels */
  .panels{position:absolute;top:0;left:0;right:0;bottom:58px;overflow:hidden;}
  .panel{position:absolute;inset:0;display:none;overflow-y:auto;}
  .panel.active{display:block;}

  /* ---------- SHORTS (vertical snap feed) ---------- */
  #shorts-feed{height:100%;overflow-y:auto;scroll-snap-type:y mandatory;scroll-behavior:smooth;touch-action:pan-y;}
  .story{height:100%;min-height:100%;scroll-snap-align:start;position:relative;display:flex;flex-direction:column;}
  .carousel{flex:1;display:flex;overflow-x:auto;scroll-snap-type:x mandatory;touch-action:pan-x;-webkit-overflow-scrolling:touch;scrollbar-width:none;}
  .carousel::-webkit-scrollbar{display:none;}
  .slide{min-width:100%;scroll-snap-align:start;position:relative;display:flex;align-items:center;padding:0 26px;
    background:linear-gradient(165deg,#241a10,#0e0b08);}
  .slide .vign{position:absolute;inset:0;background:linear-gradient(180deg,rgba(0,0,0,.05),rgba(0,0,0,.55) 100%);}
  .slide .txt{position:relative;z-index:2;font-family:'Fraunces',serif;font-weight:600;font-size:1.25rem;line-height:1.4;max-width:88%;}
  .dots{position:absolute;bottom:118px;left:0;right:0;display:flex;justify-content:center;gap:6px;z-index:6;}
  .dots i{width:16px;height:3px;border-radius:3px;background:rgba(255,255,255,.28);}
  .dots i.on{background:var(--accent);}
  .rail{position:absolute;right:12px;bottom:132px;z-index:8;display:flex;flex-direction:column;align-items:center;gap:16px;}
  .rail button{background:none;border:none;color:#fff;display:flex;flex-direction:column;align-items:center;gap:3px;cursor:pointer;}
  .rail .circle{width:42px;height:42px;border-radius:50%;background:rgba(255,255,255,.08);display:flex;align-items:center;justify-content:center;}
  .rail svg{width:20px;height:20px;fill:#fff;}
  .rail .count{font-size:.66rem;color:#e8e3f0;}
  .rail button.liked svg{fill:var(--accent);}
  .caption{position:absolute;left:0;right:0;bottom:0;z-index:7;padding:14px 70px 18px 18px;
    background:linear-gradient(0deg,rgba(0,0,0,.7) 20%,transparent 100%);}
  .catchip{display:inline-block;font-size:.6rem;letter-spacing:.08em;text-transform:uppercase;padding:3px 9px;
    border-radius:20px;background:var(--accent);color:#100c06;font-weight:700;margin-bottom:6px;}
  .caption h2{font-family:'Fraunces',serif;font-weight:700;font-size:1.08rem;margin:0;}

  /* ---------- COMICS (YouTube-home style rows) ---------- */
  #comics-panel{padding:18px 16px 30px;}
  .row-title{font-family:'Fraunces',serif;font-weight:700;font-size:1.05rem;margin:18px 2px 10px;}
  .rowscroll{display:flex;gap:12px;overflow-x:auto;scrollbar-width:none;padding-bottom:4px;}
  .rowscroll::-webkit-scrollbar{display:none;}
  .comic-card{min-width:130px;width:130px;flex-shrink:0;}
  .comic-cover{width:100%;aspect-ratio:2/3;border-radius:10px;background:linear-gradient(160deg,#2a2018,#120e0a);
    position:relative;display:flex;align-items:flex-end;padding:8px;overflow:hidden;}
  .comic-cover .ep{font-size:.62rem;background:rgba(0,0,0,.5);padding:2px 7px;border-radius:20px;}
  .comic-cover .audio{position:absolute;top:8px;right:8px;width:22px;height:22px;border-radius:50%;
    background:rgba(0,0,0,.5);display:flex;align-items:center;justify-content:center;}
  .comic-cover .audio svg{width:11px;height:11px;fill:var(--accent);}
  .comic-title{font-size:.82rem;font-weight:600;margin-top:7px;line-height:1.3;}
  .comic-sub{font-size:.7rem;color:var(--dim);margin-top:2px;}

  /* ---------- DISCOVER ---------- */
  #discover-panel{padding:18px 16px 30px;}
  .discover-grid{display:grid;grid-template-columns:1fr 1fr;gap:12px;margin-top:12px;}
  .disc-tile{background:var(--panel);border-radius:14px;padding:16px 14px;position:relative;overflow:hidden;}
  .disc-tile .bar{position:absolute;left:0;top:0;bottom:0;width:4px;background:var(--accent);}
  .disc-tile h3{font-family:'Fraunces',serif;font-size:.95rem;margin:0 0 3px;}
  .disc-tile p{font-size:.72rem;color:var(--dim);margin:0;}
  .creator-cta{margin-top:20px;background:linear-gradient(135deg,#2a1f10,#141013);border:1px solid rgba(232,163,76,.3);
    border-radius:14px;padding:18px;text-align:center;}
  .creator-cta h3{font-family:'Fraunces',serif;font-size:1rem;margin:0 0 6px;}
  .creator-cta p{font-size:.78rem;color:var(--dim);margin:0 0 12px;}
  .creator-cta button{background:var(--accent);border:none;color:#100c06;font-weight:700;padding:9px 20px;
    border-radius:30px;font-size:.82rem;}

  /* ---------- bottom nav ---------- */
  .bottomnav{position:absolute;left:0;right:0;bottom:0;height:58px;z-index:40;display:flex;
    background:#0d0c11;border-top:1px solid rgba(255,255,255,.06);}
  .navbtn{flex:1;display:flex;flex-direction:column;align-items:center;justify-content:center;gap:3px;
    background:none;border:none;color:var(--dim);font-family:'Work Sans',sans-serif;font-size:.66rem;cursor:pointer;}
  .navbtn svg{width:20px;height:20px;fill:none;stroke:var(--dim);stroke-width:1.8;}
  .navbtn.active{color:var(--accent);}
  .navbtn.active svg{stroke:var(--accent);}
</style>
</head>
<body>

<b:section id='firstillion-app' class='main' maxwidgets='1' showaddelement='no'>
<b:widget id='HTML1' locked='false' title='Firstillion App' type='HTML' visible='true'>
<b:includable id='main'>

<div class="app">
  <div class="topbar">
    <div class="logo"><span class="dot"></span>Firstillion</div>
  </div>

  <div class="panels">
    <!-- ============ TAB 1: SHORTS ============ -->
    <div class="panel active" id="panel-shorts">
      <div id="shorts-feed"></div>
    </div>

    <!-- ============ TAB 2: COMICS ============ -->
    <div class="panel" id="panel-comics">
      <div id="comics-panel"></div>
    </div>

    <!-- ============ TAB 3: DISCOVER ============ -->
    <div class="panel" id="panel-discover">
      <div id="discover-panel"></div>
    </div>
  </div>

  <div class="bottomnav">
    <button class="navbtn active" data-tab="shorts">
      <svg viewBox="0 0 24 24"><path d="M13 2 3 14h7l-1 8 10-12h-7l1-8z"/></svg>
      Shorts
    </button>
    <button class="navbtn" data-tab="comics">
      <svg viewBox="0 0 24 24"><path d="M4 4h11a3 3 0 0 1 3 3v13H7a3 3 0 0 1-3-3V4z"/><path d="M18 7h2v13a2 2 0 0 1-2 2H7"/></svg>
      Comics
    </button>
    <button class="navbtn" data-tab="discover">
      <svg viewBox="0 0 24 24"><circle cx="12" cy="12" r="9"/><path d="m15 9-2 6-6 2 2-6z"/></svg>
      Discover
    </button>
  </div>
</div>

</b:includable>
</b:widget>
</b:section>

<script>
/* =================================================================
   FIRSTILLION — data goes here. Replace/extend these arrays with
   real content. Structure only — everything below is placeholder demo.
   ================================================================= */

// ---- SHORTS: each item = one vertical story with slide-scenes ----
var shortsData = [
  { title:"Demo Short 1", tag:"Category", slides:[
      "Yahan pehla scene ka text aayega.",
      "Yahan doosra scene.",
      "Yahan teesra / aakhri scene."
    ]},
  { title:"Demo Short 2", tag:"Category", slides:[
      "Scene ek.",
      "Scene do."
    ]}
];

// ---- COMICS: rows of long-form comic series ----
var comicsRows = [
  { rowTitle:"Continue Reading", items:[
      { title:"Demo Comic 1", sub:"Ep 12 · Ongoing", audio:true },
      { title:"Demo Comic 2", sub:"Ep 4 · Ongoing", audio:false },
      { title:"Demo Comic 3", sub:"Ep 20 · Complete", audio:true }
    ]},
  { rowTitle:"New Episodes", items:[
      { title:"Demo Comic 4", sub:"Ep 1 · New", audio:false },
      { title:"Demo Comic 5", sub:"Ep 7 · Ongoing", audio:true }
    ]}
];

// ---- DISCOVER: category tiles ----
var discoverTiles = [
  { title:"Romance", sub:"Short stories" },
  { title:"Mystery", sub:"Short stories" },
  { title:"Action Comics", sub:"Long form" },
  { title:"Slice of Life", sub:"Long form" }
];

/* ================= rendering — no need to touch below ================= */

const audioSVG = `<svg viewBox="0 0 24 24"><path d="M3 10v4h4l5 5V5L7 10H3z"/></svg>`;
const heartSVG = `<svg viewBox="0 0 24 24"><path d="M12 21s-6.7-4.35-9.3-8.2C1 10.2 1.6 6.7 4.6 5.2 7 4 9.7 4.9 12 7.4c2.3-2.5 5-3.4 7.4-2.2 3 1.5 3.6 5 1.9 7.6C18.7 16.65 12 21 12 21z"/></svg>`;
const shareSVG = `<svg viewBox="0 0 24 24"><path d="M18 16.1c-.8 0-1.5.3-2 .8L8.9 13a3 3 0 0 0 0-2L16 7.1c.5.5 1.2.8 2 .8a3 3 0 1 0-3-3c0 .3 0 .6.1.9L8 9.8a3 3 0 1 0 0 4.4l7.1 4.1c-.1.3-.1.5-.1.8a3 3 0 1 0 3-3z"/></svg>`;

function renderShorts(){
  const feed = document.getElementById('shorts-feed');
  feed.innerHTML = '';
  shortsData.forEach((p,i)=>{
    const el = document.createElement('div');
    el.className = 'story';
    let slidesHTML = '';
    p.slides.forEach(s=>{ slidesHTML += `<div class="slide"><div class="vign"></div><div class="txt">${s}</div></div>`; });
    let dotsHTML = '';
    p.slides.forEach((_,si)=>{ dotsHTML += `<i class="${si===0?'on':''}"></i>`; });
    const likeBase = 20 + Math.floor(Math.random()*400);
    el.innerHTML = `
      <div class="carousel">${slidesHTML}</div>
      <div class="dots">${dotsHTML}</div>
      <div class="rail">
        <button class="likebtn"><span class="circle">${heartSVG}</span><span class="count">${likeBase}</span></button>
        <button class="sharebtn" data-i="${i}"><span class="circle">${shareSVG}</span><span class="count">Share</span></button>
      </div>
      <div class="caption"><span class="catchip">${p.tag}</span><h2>${p.title}</h2></div>`;
    feed.appendChild(el);
  });

  document.querySelectorAll('#shorts-feed .carousel').forEach(car=>{
    const dots = car.parentElement.querySelectorAll('.dots i');
    car.addEventListener('scroll', ()=>{
      requestAnimationFrame(()=>{
        const idx = Math.round(car.scrollLeft / car.clientWidth);
        dots.forEach((d,i)=> d.classList.toggle('on', i===idx));
      });
    }, {passive:true});
  });

  feed.addEventListener('click', (e)=>{
    const likeBtn = e.target.closest('.likebtn');
    if(likeBtn){
      const countEl = likeBtn.querySelector('.count');
      const liked = likeBtn.classList.toggle('liked');
      let n = parseInt(countEl.textContent,10);
      countEl.textContent = liked ? n+1 : n-1;
      return;
    }
    const shareBtn = e.target.closest('.sharebtn');
    if(shareBtn){
      const p = shortsData[shareBtn.dataset.i];
      const msg = `"${p.title}" on Firstillion\n${window.location.href}`;
      window.open('https://wa.me/?text=' + encodeURIComponent(msg), '_blank');
    }
  });
}

function renderComics(){
  const wrap = document.getElementById('comics-panel');
  wrap.innerHTML = '';
  comicsRows.forEach(row=>{
    const title = document.createElement('div');
    title.className='row-title';
    title.textContent = row.rowTitle;
    wrap.appendChild(title);
    const scroller = document.createElement('div');
    scroller.className='rowscroll';
    row.items.forEach(item=>{
      const card = document.createElement('div');
      card.className='comic-card';
      card.innerHTML = `
        <div class="comic-cover">
          ${item.audio? `<div class="audio">${audioSVG}</div>` : ''}
          <span class="ep">${item.sub.split('·')[0].trim()}</span>
        </div>
        <div class="comic-title">${item.title}</div>
        <div class="comic-sub">${item.sub}</div>`;
      scroller.appendChild(card);
    });
    wrap.appendChild(scroller);
  });
}

function renderDiscover(){
  const wrap = document.getElementById('discover-panel');
  let html = '<div class="row-title">Discover</div><div class="discover-grid">';
  discoverTiles.forEach(t=>{
    html += `<div class="disc-tile"><div class="bar"></div><h3>${t.title}</h3><p>${t.sub}</p></div>`;
  });
  html += '</div>';
  html += `<div class="creator-cta">
      <h3>Become a Firstillion Creator</h3>
      <p>Apni stories aur comics publish karne ka mauka jald aa raha hai.</p>
      <button>Notify Me</button>
    </div>`;
  wrap.innerHTML = html;
}

// tab switching
document.querySelectorAll('.navbtn').forEach(btn=>{
  btn.addEventListener('click', ()=>{
    document.querySelectorAll('.navbtn').forEach(b=>b.classList.remove('active'));
    document.querySelectorAll('.panel').forEach(p=>p.classList.remove('active'));
    btn.classList.add('active');
    document.getElementById('panel-'+btn.dataset.tab).classList.add('active');
  });
});

renderShorts();
renderComics();
renderDiscover();
</script>

</body>
</html>
