<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>Your Name — links</title>
  <!--
    Link‑in‑bio: single‑file project (HTML + CSS + JS)
    — Customize the CONFIG object below
    — Drop this file on any static host (Cloudflare Pages, GitHub Pages, Netlify, Vercel)
    — No external libraries; works offline

    Optional: set real URLs for avatar and social links.
  -->

  <!-- Open Graph / SEO (edit these) -->
  <meta name="description" content="All my links in one place." />
  <meta property="og:title" content="Your Name — links" />
  <meta property="og:description" content="All my links in one place." />
  <meta property="og:type" content="website" />
  <meta property="og:url" content="https://your-domain.example" />
  <meta property="og:image" content="https://your-cdn.example/preview.png" />
  <meta name="theme-color" content="#8A2BE2" id="theme-color-meta"/>

  <style>
    :root{
      --bg: 12 12 16;
      --bg2: 18 18 24;
      --fg: 245 245 255;
      --muted: 180 180 200;
      --card: 20 20 28/0.6;
      --border: 255 255 255/0.08;
      --accent: 138 43 226; /* default overwritten by JS */
      --radius: 18px;
    }
    *,*:before,*:after{box-sizing:border-box}
    html,body{height:100%}
    body{
      margin:0; font-family: ui-sans-serif, system-ui, -apple-system, Segoe UI, Roboto, "Helvetica Neue", Arial, "Noto Sans", "Apple Color Emoji", "Segoe UI Emoji";
      color: rgb(var(--fg));
      background: radial-gradient(1200px 800px at 20% -10%, rgba(var(--accent)/0.25), transparent),
                  radial-gradient(1200px 800px at 120% 10%, rgba(var(--accent)/0.15), transparent),
                  linear-gradient(180deg, rgb(var(--bg)), rgb(var(--bg2)));
      display:grid; place-items:center; padding:24px;
    }
    .wrap{ width:min(680px, 100%); }
    .card{
      background: color-mix(in oklab, rgba(var(--card)) 80%, rgba(var(--accent)/0.05));
      backdrop-filter: blur(12px);
      border: 1px solid rgba(var(--border));
      border-radius: var(--radius);
      padding: 24px; box-shadow: 0 10px 40px rgba(0,0,0,.35);
      animation: floatIn .6s cubic-bezier(.2,.8,.2,1) both;
    }
    @keyframes floatIn{from{opacity:0; transform: translateY(8px) scale(.98)} to{opacity:1; transform:none}}

    header{ display:flex; gap:16px; align-items:center; }
    .avatar{
      width:84px; height:84px; border-radius: 24px; overflow:hidden; flex:none;
      border:1px solid rgba(var(--border));
      box-shadow: 0 8px 24px rgba(0,0,0,.25);
    }
    .avatar img{ width:100%; height:100%; object-fit:cover; display:block }

    .headings{ flex:1; min-width:0 }
    h1{ font-size: clamp(22px, 3.4vw, 28px); margin: 2px 0 6px; display:flex; align-items:center; gap:8px; }
    .verified{ display:inline-flex; align-items:center; gap:6px; font-size:12px; padding:2px 8px; border-radius:999px; border:1px solid rgba(var(--border));
      background: linear-gradient(180deg, rgba(var(--accent)/.25), rgba(var(--accent)/.1));
    }
    .handle{ color: rgb(var(--muted)); font-size:14px; }
    .bio{ margin-top:8px; color: rgb(var(--muted)); line-height:1.5 }

    .badges{ margin-top:12px; display:flex; flex-wrap:wrap; gap:8px }
    .badge{ border:1px solid rgba(var(--border)); border-radius:999px; padding:6px 10px; font-size:12px; color: rgb(var(--muted)); }

    .links{ margin-top:20px; display:grid; gap:12px }
    .link{
      display:flex; align-items:center; gap:12px; padding:14px 16px; border-radius:14px;
      background: color-mix(in oklab, rgba(var(--card)) 75%, rgba(var(--accent)/0.05));
      border:1px solid rgba(var(--border));
      text-decoration:none; color: inherit; font-weight:600;
      transition: transform .08s ease, background .2s ease, border-color .2s ease;
    }
    .link:hover{ transform: translateY(-1px) scale(1.01); border-color: rgba(var(--accent)/.35); }
    .link:active{ transform: translateY(0) scale(.995) }
    .link .icon{ width:22px; height:22px; display:grid; place-items:center; flex:none }
    .link small{ margin-left:auto; font-weight:500; color: rgb(var(--muted)); }

    .row{ display:flex; gap:10px; flex-wrap:wrap; margin-top:18px }
    .btn{
      appearance:none; border:none; border-radius:12px; padding:10px 12px; font-weight:600;
      background: linear-gradient(180deg, rgba(var(--accent)/.22), rgba(var(--accent)/.06));
      border:1px solid rgba(var(--border)); color:inherit; cursor:pointer;
    }

    footer{ margin-top:18px; padding-top:14px; border-top:1px dashed rgba(var(--border)); display:flex; justify-content:space-between; gap:10px; color: rgb(var(--muted)); font-size:12px }

    .theme-toggle{ display:inline-flex; gap:8px; align-items:center }
    .pill{ display:inline-flex; align-items:center; gap:8px; border-radius:999px; padding:6px 10px; background: rgba(255,255,255,.04); border:1px solid rgba(var(--border)); }

    @media (max-width:420px){
      .avatar{ width:72px; height:72px; border-radius:18px }
    }
  </style>
</head>
<body>
  <div class="wrap">
    <main class="card" role="main">
      <header>
        <div class="avatar"><img id="avatar" alt="avatar" /></div>
        <div class="headings">
          <h1 id="name">
            <!-- filled by JS -->
          </h1>
          <div class="handle" id="handle"></div>
          <p class="bio" id="bio"></p>
          <div class="badges" id="badges"></div>
        </div>
      </header>

      <div class="links" id="links"></div>

      <div class="row">
        <button class="btn" id="copyBtn" title="Copy page link">Copy link</button>
        <button class="btn" id="shareBtn" title="Share">Share</button>
        <span class="pill theme-toggle"><input type="checkbox" id="themeSwitch"/> <label for="themeSwitch">Light mode</label></span>
      </div>

      <footer>
        <span id="footerText">© 2025 Your Name</span>
        <span id="viewCount"></span>
      </footer>
    </main>
  </div>

  <script>
  // ==========================
  // CONFIG — edit this object
  // ==========================
  const CONFIG = {
    name: "Your Name",
    handle: "@yourhandle",
    verified: true,
    bio: "Builder • scripter • open to commissions.",
    avatarUrl: "https://picsum.photos/200?random=3",
    accent: "#8A2BE2",
    badges: ["Developer", "Roblox", "Commissions open"],
    footer: "© 2025 Your Name",
    // Each link: { label, href, icon?, note? }
    links: [
      { label: "Discord", href: "https://discord.gg/yourcode", icon: "discord", note: "DMs open" },
      { label: "Roblox Profile", href: "https://www.roblox.com/users/1/profile", icon: "roblox" },
      { label: "YouTube", href: "https://youtube.com/@your", icon: "youtube" },
      { label: "GitHub", href: "https://github.com/your", icon: "github" },
      { label: "Donate", href: "https://ko-fi.com/your", icon: "donate", note: "thank you!" }
    ]
  }

  // =============
  // Icon library
  // =============
  const ICONS = {
    check: `<svg width="14" height="14" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg"><path d="M20 6L9 17l-5-5" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/></svg>`,
    discord: `<svg viewBox="0 0 24 24" width="22" height="22" aria-hidden="true"><path fill="currentColor" d="M20.317 4.369A19.791 19.791 0 0 0 16.558 3a14.043 14.043 0 0 0-.7 1.45 19.746 19.746 0 0 0-4.726 0A14.043 14.043 0 0 0 10.432 3c-1.32.24-2.64.6-3.76 1.11C3.25 7.08 2.7 9.64 2.88 12.16c1.58 1.18 3.1 1.9 4.62 2.38a10.85 10.85 0 0 0 .84-1.66c-.46-.17-.9-.38-1.32-.61.11-.08.22-.17.32-.26 2.53 1.18 5.27 1.18 7.8 0 .11.09.21.18.32.26-.42.23-.86.44-1.32.61.24.58.52 1.14.84 1.66 1.52-.48 3.04-1.2 4.62-2.38.3-3.08-.52-5.61-2.84-7.79Z"/></svg>`,
    youtube: `<svg viewBox="0 0 24 24" width="22" height="22"><path fill="currentColor" d="M23.5 6.2a3.5 3.5 0 0 0-2.46-2.47C18.9 3 12 3 12 3s-6.9 0-9.04.73A3.5 3.5 0 0 0 .5 6.2 36.6 36.6 0 0 0 0 12a36.6 36.6 0 0 0 .5 5.8 3.5 3.5 0 0 0 2.46 2.47C5.1 21 12 21 12 21s6.9 0 9.04-.73a3.5 3.5 0 0 0 2.46-2.47A36.6 36.6 0 0 0 24 12a36.6 36.6 0 0 0-.5-5.8ZM9.75 15.02V8.98L15.5 12l-5.75 3.02Z"/></svg>`,
    github: `<svg viewBox="0 0 24 24" width="22" height="22"><path fill="currentColor" d="M12 .5a12 12 0 0 0-3.79 23.39c.6.11.82-.26.82-.58v-2.18c-3.35.73-4.05-1.61-4.05-1.61a3.19 3.19 0 0 0-1.34-1.77c-1.09-.75.08-.74.08-.74a2.52 2.52 0 0 1 1.84 1.24 2.56 2.56 0 0 0 3.5 1 2.56 2.56 0 0 1 .76-1.6C7.2 16.89 4.38 15.87 4.38 11.5A4.64 4.64 0 0 1 5.59 8.3a4.31 4.31 0 0 1 .12-3.18s1.02-.33 3.34 1.26a11.55 11.55 0 0 1 6.09 0c2.31-1.59 3.33-1.26 3.33-1.26.44 1 .48 2.14.12 3.18a4.64 4.64 0 0 1 1.22 3.2c0 4.37-2.83 5.39-5.53 5.68a2.87 2.87 0 0 1 .82 2.23v3.31c0 .32.21.7.83.58A12 12 0 0 0 12 .5Z"/></svg>`,
    donate: `<svg viewBox="0 0 24 24" width="22" height="22"><path fill="currentColor" d="M12 21.35 10.55 20.03C5.4 15.36 2 12.28 2 8.5 2 5.42 4.42 3 7.5 3c1.74 0 3.41.81 4.5 2.09A5.98 5.98 0 0 1 16.5 3C19.58 3 22 5.42 22 8.5c0 3.78-3.4 6.86-8.55 11.54L12 21.35z"/></svg>`,
    roblox: `<svg viewBox='0 0 24 24' width='22' height='22'><path fill='currentColor' d='M3 3l18 3-3 15-18-3 3-15zm7.4 7.4a2.6 2.6 0 1 0 3.68 3.68 2.6 2.6 0 0 0-3.68-3.68z'/></svg>`,
    link: `<svg viewBox="0 0 24 24" width="22" height="22"><path fill="currentColor" d="M3.9 12a5 5 0 0 1 5-5h3v2h-3a3 3 0 1 0 0 6h3v2h-3a5 5 0 0 1-5-5Zm7-1h3a3 3 0 1 1 0 6h-3v-2h3a1 1 0 1 0 0-2h-3v-2Z"/></svg>`
  }

  // =====================
  // Simple view tracking
  // =====================
  const VIEW_KEY = "linkinbio_views";
  function incrementViews(){
    const n = Number(localStorage.getItem(VIEW_KEY) || 0) + 1;
    localStorage.setItem(VIEW_KEY, String(n));
    return n;
  }

  // ===========================
  // Render helpers / components
  // ===========================
  const $ = sel => document.querySelector(sel);
  function el(tag, attrs = {}, children = []){
    const node = document.createElement(tag);
    Object.entries(attrs).forEach(([k,v]) => {
      if(k === 'class') node.className = v;
      else if(k === 'html') node.innerHTML = v;
      else if(k.startsWith('on') && typeof v === 'function') node.addEventListener(k.slice(2), v);
      else node.setAttribute(k, v);
    });
    children.forEach(c => node.append(c));
    return node;
  }

  function icon(name){
    return el('span', { class: 'icon', html: ICONS[name] || ICONS.link });
  }

  function render(){
    // theme / accent
    const accent = CONFIG.accent || '#8A2BE2';
    document.documentElement.style.setProperty('--accent', hexToRgb(accent));
    $('#theme-color-meta').setAttribute('content', accent);

    // identity
    $('#avatar').src = CONFIG.avatarUrl;
    const nameEl = el('span', { html: escapeHtml(CONFIG.name) });
    $('#name').append(nameEl);
    if(CONFIG.verified){
      const v = el('span', { class: 'verified' }, [icon('check'), document.createTextNode('Verified')]);
      $('#name').append(v);
    }
    $('#handle').textContent = CONFIG.handle || '';
    $('#bio').textContent = CONFIG.bio || '';

    // badges
    const b = $('#badges'); b.innerHTML = '';
    (CONFIG.badges || []).forEach(txt => b.append(el('span', { class:'badge', html: escapeHtml(txt) })));

    // links
    const list = $('#links'); list.innerHTML = '';
    const clicks = JSON.parse(localStorage.getItem('clickCounts')||'{}');
    (CONFIG.links||[]).forEach((lnk, i) => {
      const a = el('a', { class:'link', href: lnk.href, target:'_blank', rel:'noopener noreferrer' }, [
        icon(lnk.icon),
        el('span', { html: escapeHtml(lnk.label) }),
        lnk.note ? el('small', { html: escapeHtml(lnk.note) }) : ''
      ]);
      a.addEventListener('click', () => {
        clicks[lnk.href] = (clicks[lnk.href]||0) + 1;
        localStorage.setItem('clickCounts', JSON.stringify(clicks));
      });
      list.append(a);
    });

    // footer
    $('#footerText').textContent = CONFIG.footer || '';
    const views = incrementViews();
    $('#viewCount').textContent = `Views (this device): ${views}`;
  }

  // =================
  // Utilities
  // =================
  function hexToRgb(hex){
    const h = hex.replace('#','');
    const bigint = parseInt(h.length===3 ? h.split('').map(x=>x+x).join('') : h, 16);
    const r = (bigint >> 16) & 255; const g = (bigint >> 8) & 255; const b = bigint & 255;
    return `${r} ${g} ${b}`;
  }
  function escapeHtml(str){
    return String(str).replace(/[&<>"']/g, s => ({'&':'&amp;','<':'&lt;','>':'&gt;','"':'&quot;','\'':'&#39;'}[s]));
  }

  // ======================
  // Actions / event wiring
  // ======================
  $('#copyBtn').addEventListener('click', async () => {
    try{
      await navigator.clipboard.writeText(location.href);
      flash('Link copied');
    }catch{ flash('Copy failed'); }
  });
  $('#shareBtn').addEventListener('click', async () => {
    const data = { title: document.title, text: CONFIG.bio, url: location.href };
    if(navigator.share){
      try{ await navigator.share(data); }catch(e){ /* user cancelled */ }
    } else {
      await navigator.clipboard.writeText(location.href);
      flash('Link copied');
    }
  });

  // Theme toggle (light/dark)
  const THEME_KEY = 'lib_theme_light';
  const themeSwitch = $('#themeSwitch');
  const stored = localStorage.getItem(THEME_KEY) === '1';
  themeSwitch.checked = stored;
  applyTheme(stored);
  themeSwitch.addEventListener('change', () => {
    localStorage.setItem(THEME_KEY, themeSwitch.checked ? '1' : '0');
    applyTheme(themeSwitch.checked);
  });
  function applyTheme(light){
    if(light){
      document.documentElement.style.setProperty('--bg', '245 245 250');
      document.documentElement.style.setProperty('--bg2', '235 235 242');
      document.documentElement.style.setProperty('--fg', '10 10 14');
      document.documentElement.style.setProperty('--muted', '60 60 80');
      document.documentElement.style.setProperty('--border', '0 0 0 / .08');
    } else {
      document.documentElement.style.setProperty('--bg', '12 12 16');
      document.documentElement.style.setProperty('--bg2', '18 18 24');
      document.documentElement.style.setProperty('--fg', '245 245 255');
      document.documentElement.style.setProperty('--muted', '180 180 200');
      document.documentElement.style.setProperty('--border', '255 255 255 / .08');
    }
  }

  // Tiny toast
  function flash(msg){
    const t = el('div', { class:'toast', html: escapeHtml(msg) });
    Object.assign(t.style, { position:'fixed', left:'50%', bottom:'24px', transform:'translateX(-50%)', padding:'10px 14px', background:'rgba(0,0,0,.75)', color:'#fff', borderRadius:'10px', backdropFilter:'blur(6px)', zIndex:9999 });
    document.body.append(t); setTimeout(()=>{ t.remove() }, 1600);
  }

  // kick things off
  render();
  </script>
</body>
</html>
