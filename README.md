<!DOCTYPE html>
<html lang="de">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Life is Good – Bakery Münsingen</title>
<link href="https://fonts.googleapis.com/css2?family=Playfair+Display:ital,wght@0,400;0,700;1,400&family=Cormorant+Garamond:ital,wght@0,300;0,400;1,300&family=Sacramento&display=swap" rel="stylesheet">
<style>
  :root {
    --bg:         #fdf6f0;
    --bg2:        #fef0f5;
    --white:      #ffffff;
    --peach:      #f7c5a0;
    --peach-pale: #fde8d8;
    --rose:       #f0a0b8;
    --rose-pale:  #fce4ee;
    --mint:       #a8d8c8;
    --mint-pale:  #e0f5ef;
    --lavender:   #c8b4e8;
    --lav-pale:   #ede4f8;
    --yellow:     #f7dfa0;
    --accent:     #e07898;   /* main accent – dusty rose */
    --accent2:    #d4956a;   /* warm caramel */
    --text:       #4a2a3a;
    --text-mid:   #8a5a6a;
    --text-soft:  #b89aa8;
    --border:     rgba(224,120,152,0.2);
  }

  * { margin:0; padding:0; box-sizing:border-box; }
  html { scroll-behavior:smooth; }
  body { background:var(--bg); color:var(--text); font-family:'Cormorant Garamond',serif; overflow-x:hidden; cursor:none; }

  /* ── CURSOR ── */
  .cursor { position:fixed; width:12px; height:12px; background:var(--accent); border-radius:50%; pointer-events:none; z-index:9999; transform:translate(-50%,-50%); transition:width .3s,height .3s,background .3s; }
  .cursor-ring { position:fixed; width:38px; height:38px; border:1.5px solid var(--accent); border-radius:50%; pointer-events:none; z-index:9998; transform:translate(-50%,-50%); transition:width .3s,height .3s,opacity .3s; opacity:.45; }

  /* ── NAV ── */
  nav {
    position:fixed; top:0; left:0; right:0; z-index:100;
    display:flex; justify-content:space-between; align-items:center;
    padding:1rem 4rem;
    background:linear-gradient(to bottom,rgba(253,246,240,.98),rgba(253,246,240,0));
    transition:background .4s,box-shadow .4s;
  }
  nav.scrolled { background:rgba(255,255,255,.95); backdrop-filter:blur(14px); box-shadow:0 2px 30px rgba(224,120,152,.12); }
  .nav-logo-img { height:52px; object-fit:contain; }
  .nav-links { display:flex; gap:2.2rem; align-items:center; }
  .nav-links a { color:var(--text-mid); text-decoration:none; font-size:.9rem; letter-spacing:.12em; text-transform:uppercase; transition:color .3s; }
  .nav-links a:hover { color:var(--accent); }
  .nav-order-btn {
    background:var(--accent)!important; color:#fff!important;
    padding:.6rem 1.5rem!important; border-radius:40px; font-weight:600;
    transition:background .3s,transform .2s!important; letter-spacing:.05em!important;
  }
  .nav-order-btn:hover { background:#c05878!important; transform:translateY(-2px); }

  /* ── HERO ── */
  .hero { position:relative; height:100vh; min-height:600px; overflow:hidden; display:flex; align-items:flex-end; justify-content:center; }
  .hero-img { position:absolute; inset:0; width:100%; height:100%; object-fit:cover; object-position:center top; filter:brightness(.78) saturate(.85); }
  .hero-overlay { position:absolute; inset:0; background:linear-gradient(to bottom,rgba(253,246,240,.04) 0%,rgba(253,246,240,0) 30%,rgba(253,246,240,.5) 65%,rgba(253,246,240,1) 100%); }
  .hero-content { position:relative; z-index:2; text-align:center; padding-bottom:5.5rem; animation:fadeUp 1.2s ease forwards; }
  .hero-wordmark { height:clamp(80px,14vw,160px); object-fit:contain; filter:drop-shadow(0 6px 24px rgba(74,42,58,.25)); }
  .hero-subtitle { font-size:clamp(.95rem,2.5vw,1.3rem); letter-spacing:.3em; text-transform:uppercase; color:var(--text); margin-top:.8rem; opacity:.7; }
  .hero-cta { margin-top:2.2rem; display:inline-block; padding:.95rem 2.8rem; border:2px solid var(--accent); color:var(--accent); font-size:1.05rem; letter-spacing:.2em; text-transform:uppercase; text-decoration:none; border-radius:50px; transition:background .35s,color .35s,transform .3s,box-shadow .3s; cursor:none; background:rgba(255,255,255,.6); backdrop-filter:blur(6px); }
  .hero-cta:hover { background:var(--accent); color:#fff; transform:translateY(-3px); box-shadow:0 12px 35px rgba(224,120,152,.35); }
  @keyframes fadeUp { from{opacity:0;transform:translateY(40px)} to{opacity:1;transform:translateY(0)} }

  /* ── LOGO CHARACTER SECTION ── */
  .logo-section { display:flex; flex-direction:column; align-items:center; padding:3.5rem 2rem 1.5rem; background:var(--bg); }
  .logo-wrapper { position:relative; width:200px; height:200px; animation:floatLogo 4s ease-in-out infinite; }
  .logo-wrapper img { width:100%; height:100%; object-fit:contain; border-radius:50%; box-shadow:0 0 50px rgba(224,120,152,.2),0 0 100px rgba(224,120,152,.08); transition:box-shadow .4s; }
  .logo-wrapper:hover img { box-shadow:0 0 70px rgba(224,120,152,.45),0 0 140px rgba(224,120,152,.18); animation-play-state:paused; }
  .logo-glow-ring { position:absolute; inset:-14px; border-radius:50%; border:2px solid rgba(224,120,152,.22); animation:pulseRing 3s ease-in-out infinite; }
  .logo-glow-ring-2 { position:absolute; inset:-28px; border-radius:50%; border:1px solid rgba(247,197,160,.2); animation:pulseRing 3s ease-in-out infinite 1.2s; }
  @keyframes floatLogo { 0%,100%{transform:translateY(0)} 50%{transform:translateY(-13px)} }
  @keyframes pulseRing { 0%,100%{transform:scale(1);opacity:.55} 50%{transform:scale(1.05);opacity:1} }

  /* ── SHARED ── */
  .section-eyebrow { font-size:.78rem; letter-spacing:.4em; text-transform:uppercase; color:var(--accent); }
  .section-heading { font-family:'Playfair Display',serif; font-size:clamp(2rem,5vw,3.2rem); color:var(--text); line-height:1.2; margin-top:.4rem; }
  .section-heading em { font-style:italic; color:var(--accent); }

  /* ── PASTEL STRIP ── */
  .pastel-strip { display:flex; height:8px; }
  .pastel-strip span { flex:1; }
  .ps1{background:var(--peach)} .ps2{background:var(--rose)} .ps3{background:var(--mint)} .ps4{background:var(--lavender)} .ps5{background:var(--yellow)} .ps6{background:var(--peach)} .ps7{background:var(--rose)} .ps8{background:var(--mint)}

  /* ── ICONS ── */
  .icons-section { padding:4rem 4rem 3rem; max-width:1050px; margin:0 auto; text-align:center; }
  .icons-grid { display:flex; justify-content:center; gap:2.5rem; margin-top:2.5rem; flex-wrap:wrap; }
  .icon-item { display:flex; flex-direction:column; align-items:center; gap:.7rem; cursor:none; transition:transform .3s; }
  .icon-item:hover { transform:translateY(-8px); }
  .icon-circle { width:72px; height:72px; border-radius:50%; display:flex; align-items:center; justify-content:center; font-size:1.7rem; border:1.5px solid rgba(255,255,255,.8); transition:transform .3s,box-shadow .3s; }
  .ic-peach  { background:var(--peach-pale); }
  .ic-rose   { background:var(--rose-pale); }
  .ic-mint   { background:var(--mint-pale); }
  .ic-lav    { background:var(--lav-pale); }
  .ic-yellow { background:var(--yellow); opacity:.85; }
  .icon-item:hover .icon-circle { box-shadow:0 8px 25px rgba(74,42,58,.14); transform:scale(1.1); }
  .icon-label { font-size:.78rem; letter-spacing:.2em; text-transform:uppercase; color:var(--text-soft); }

  /* ── DIVIDER ── */
  .divider { display:flex; align-items:center; gap:1.5rem; max-width:260px; margin:0 auto; padding:1rem 0; }
  .divider span { flex:1; height:1px; background:linear-gradient(to right,transparent,var(--rose),transparent); }
  .divider-icon { color:var(--rose); font-size:.9rem; }

  /* ── WELCOME ── */
  .welcome { padding:5rem 4rem; max-width:1100px; margin:0 auto; display:grid; grid-template-columns:1fr 1fr; gap:5rem; align-items:center; }
  .welcome-text p { margin-top:1.5rem; font-size:1.2rem; line-height:1.9; color:var(--text-mid); font-weight:300; }
  .cta-btn { display:inline-block; margin-top:2.5rem; padding:.9rem 2.4rem; background:var(--accent); color:#fff; font-size:1rem; letter-spacing:.15em; text-transform:uppercase; text-decoration:none; font-weight:600; border-radius:50px; transition:background .3s,transform .3s,box-shadow .3s; cursor:none; }
  .cta-btn:hover { background:#c05878; transform:translateY(-3px); box-shadow:0 12px 30px rgba(224,120,152,.3); }
  .welcome-visual { position:relative; height:440px; border-radius:20px; overflow:hidden; box-shadow:0 20px 60px rgba(74,42,58,.1); }
  .welcome-visual img { width:100%; height:100%; object-fit:cover; filter:brightness(.9) saturate(.9); transition:transform .8s ease; }
  .welcome-visual:hover img { transform:scale(1.04); }
  .welcome-visual::after { content:''; position:absolute; inset:0; background:linear-gradient(135deg,rgba(247,197,160,.12),transparent 60%); pointer-events:none; }

  /* ── PASTEL CARDS ── */
  .cards-section { padding:5rem 4rem; }
  .cards-inner { max-width:1100px; margin:0 auto; }
  .cards-grid { display:grid; grid-template-columns:repeat(3,1fr); gap:1.8rem; margin-top:3rem; }
  .card { border-radius:20px; padding:2.8rem 2rem; text-align:center; transition:transform .3s,box-shadow .3s; cursor:none; }
  .card-peach  { background:var(--peach-pale); }
  .card-rose   { background:var(--rose-pale); }
  .card-mint   { background:var(--mint-pale); }
  .card:hover  { transform:translateY(-8px); box-shadow:0 20px 50px rgba(74,42,58,.1); }
  .card-icon { font-size:2.6rem; margin-bottom:1rem; display:block; }
  .card h3 { font-family:'Playfair Display',serif; font-size:1.3rem; color:var(--text); margin-bottom:.6rem; }
  .card p { font-size:1rem; line-height:1.7; color:var(--text-mid); font-weight:300; }

  /* ── ORDER ── */
  .order-section { padding:6rem 4rem; background:var(--rose-pale); text-align:center; }
  .order-section p { max-width:560px; margin:1.5rem auto 0; font-size:1.2rem; line-height:1.9; color:var(--text-mid); font-weight:300; }
  .order-btn-big { display:inline-block; margin-top:2.8rem; padding:1.1rem 4rem; background:var(--accent); color:#fff; font-family:'Playfair Display',serif; font-size:1.1rem; letter-spacing:.15em; text-decoration:none; border-radius:60px; transition:background .35s,color .35s,transform .3s,box-shadow .3s; cursor:none; border:2px solid var(--accent); }
  .order-btn-big:hover { background:transparent; color:var(--accent); transform:translateY(-3px); box-shadow:0 15px 40px rgba(224,120,152,.25); }

  /* ── LOCATION ── */
  .location-section { padding:5rem 4rem; max-width:900px; margin:0 auto; text-align:center; }
  .location-badge { display:inline-flex; align-items:center; gap:.7rem; background:var(--mint-pale); border-radius:50px; padding:.8rem 2rem; font-size:1rem; color:var(--text-mid); margin-top:2rem; letter-spacing:.05em; }
  .location-badge span { font-size:1.3rem; }

  /* ── TESTIMONIALS ── */
  .testimonials { padding:6rem 4rem; max-width:1100px; margin:0 auto; }
  .testimonials>.section-eyebrow,.testimonials>.section-heading { text-align:center; }
  .testimonials-grid { display:grid; grid-template-columns:repeat(3,1fr); gap:2rem; margin-top:3.5rem; }
  .testimonial-card { padding:2.4rem; background:var(--white); border-radius:18px; border:1px solid var(--border); box-shadow:0 4px 20px rgba(224,120,152,.07); transition:transform .3s,box-shadow .3s; }
  .testimonial-card:hover { transform:translateY(-6px); box-shadow:0 18px 45px rgba(224,120,152,.16); }
  .testimonial-card p { font-size:1.05rem; line-height:1.85; font-style:italic; color:var(--text-mid); font-weight:300; }
  .testimonial-stars { color:var(--accent); font-size:.95rem; margin-bottom:1rem; }

  /* ── SOCIAL ── */
  .social-section { padding:5rem 4rem 6rem; text-align:center; background:linear-gradient(135deg,var(--lav-pale) 0%,var(--rose-pale) 50%,var(--peach-pale) 100%); }
  .social-buttons { display:flex; gap:1.5rem; justify-content:center; margin-top:3rem; flex-wrap:wrap; }
  .social-btn { display:flex; align-items:center; gap:.8rem; padding:1rem 2.5rem; text-decoration:none; font-size:1.05rem; letter-spacing:.08em; border:1.5px solid; border-radius:50px; transition:all .35s; cursor:none; background:rgba(255,255,255,.7); backdrop-filter:blur(8px); }
  .social-btn svg { width:22px; height:22px; fill:currentColor; }
  .social-btn-ig { border-color:#e1306c; color:#e1306c; }
  .social-btn-ig:hover { background:#e1306c; color:#fff; transform:translateY(-4px); box-shadow:0 14px 40px rgba(225,48,108,.25); }
  .social-btn-wa { border-color:#25b560; color:#25b560; }
  .social-btn-wa:hover { background:#25b560; color:#fff; transform:translateY(-4px); box-shadow:0 14px 40px rgba(37,181,96,.25); }

  /* ── FOOTER ── */
  footer { background:var(--white); border-top:1px solid var(--border); padding:4rem; }
  .footer-grid { max-width:1100px; margin:0 auto; display:grid; grid-template-columns:1.5fr 1fr 1fr; gap:3rem; }
  .footer-logo-img { height:70px; object-fit:contain; margin-bottom:1rem; }
  .footer-desc { font-size:1rem; line-height:1.8; color:var(--text-soft); font-weight:300; }
  .footer-heading { font-size:.78rem; letter-spacing:.15em; text-transform:uppercase; color:var(--text); margin-bottom:1.2rem; font-family:'Playfair Display',serif; }
  .hours-list { list-style:none; }
  .hours-list li { display:flex; justify-content:space-between; padding:.4rem 0; border-bottom:1px solid var(--rose-pale); font-size:.9rem; color:var(--text-mid); }
  .hours-list li span:first-child { color:var(--accent); }
  .contact-list { list-style:none; }
  .contact-list li { padding:.4rem 0; font-size:.95rem; color:var(--text-mid); display:flex; align-items:center; gap:.6rem; }
  .contact-list a { color:var(--accent); text-decoration:none; transition:color .3s; }
  .contact-list a:hover { color:#c05878; }
  .footer-bottom { max-width:1100px; margin:3rem auto 0; padding-top:1.5rem; border-top:1px solid var(--border); text-align:center; font-size:.85rem; color:var(--text-soft); }

  /* ── REVEAL ── */
  .reveal { opacity:0; transform:translateY(26px); transition:opacity .8s ease,transform .8s ease; }
  .reveal.visible { opacity:1; transform:translateY(0); }

  /* ── PARTICLES ── */
  .particles { position:fixed; inset:0; pointer-events:none; z-index:0; overflow:hidden; }
  .particle { position:absolute; border-radius:50%; animation:drift linear infinite; }
  @keyframes drift { 0%{transform:translateY(100vh) translateX(0);opacity:0} 10%{opacity:1} 90%{opacity:.35} 100%{transform:translateY(-120px) translateX(50px);opacity:0} }

  @media(max-width:900px){
    nav{padding:1rem 1.5rem} .nav-links{display:none}
    .welcome{grid-template-columns:1fr;gap:2rem;padding:3rem 1.5rem} .welcome-visual{height:260px}
    .testimonials-grid,.cards-grid{grid-template-columns:1fr} .footer-grid{grid-template-columns:1fr}
    .icons-section,.order-section,.social-section,.testimonials,.cards-section,.location-section,footer{padding:4rem 1.5rem}
  }
</style>
</head>
<body>

<div class="cursor" id="cursor"></div>
<div class="cursor-ring" id="cursorRing"></div>
<div class="particles" id="particles"></div>

<!-- NAV -->
<nav id="navbar">
  <a href="#"><img src="/mnt/user-data/uploads/eb63b7a6-e88f-4ab7-b942-ab5a2ea8bed8.JPG" alt="Life is Good Logo" class="nav-logo-img"></a>
  <div class="nav-links">
    <a href="#welcome">Über uns</a>
    <a href="#angebot">Angebot</a>
    <a href="#order">Bestellen</a>
    <a href="#testimonials">Bewertungen</a>
    <a href="#kontakt">Kontakt</a>
    <a href="https://wa.me/41000000000" target="_blank" class="nav-order-btn">Jetzt bestellen</a>
  </div>
</nav>

<!-- HERO -->
<section class="hero">
  <img src="/mnt/user-data/uploads/Bild_oben.jpg" alt="Life is Good Bakery" class="hero-img">
  <div class="hero-overlay"></div>
  <div class="hero-content">
    <img src="/mnt/user-data/uploads/1d933d7d-0d24-4df7-b48f-06403212c3fd.JPG" alt="Life is Good" class="hero-wordmark">
    <div class="hero-subtitle">Handgemachte Torten &amp; Desserts · Münsingen</div>
    <a href="#order" class="hero-cta">Torte bestellen</a>
  </div>
</section>

<!-- PASTEL STRIP -->
<div class="pastel-strip"><span class="ps1"></span><span class="ps2"></span><span class="ps3"></span><span class="ps4"></span><span class="ps5"></span><span class="ps6"></span><span class="ps7"></span><span class="ps8"></span></div>

<!-- LOGO CHARACTER -->
<section class="logo-section">
  <div class="logo-wrapper">
    <div class="logo-glow-ring-2"></div>
    <div class="logo-glow-ring"></div>
    <img src="/mnt/user-data/uploads/eb63b7a6-e88f-4ab7-b942-ab5a2ea8bed8.JPG" alt="Life is Good Logo">
  </div>
</section>

<!-- ICONS -->
<div class="icons-section reveal">
  <p class="section-eyebrow">Was wir anbieten</p>
  <h2 class="section-heading">Süsses für jeden Anlass</h2>
  <div class="icons-grid">
    <div class="icon-item"><div class="icon-circle ic-peach">🎂</div><span class="icon-label">Custom Torten</span></div>
    <div class="icon-item"><div class="icon-circle ic-rose">🧁</div><span class="icon-label">Cupcakes</span></div>
    <div class="icon-item"><div class="icon-circle ic-mint">🍰</div><span class="icon-label">Desserts</span></div>
    <div class="icon-item"><div class="icon-circle ic-lav">🩷</div><span class="icon-label">Mit Liebe gemacht</span></div>
    <div class="icon-item"><div class="icon-circle ic-yellow">📍</div><span class="icon-label">Münsingen</span></div>
  </div>
</div>

<div class="divider"><span></span><span class="divider-icon">✦</span><span></span></div>

<!-- WELCOME -->
<section class="welcome" id="welcome">
  <div class="welcome-text reveal">
    <p class="section-eyebrow">Willkommen</p>
    <h2 class="section-heading">Jede Torte ist<br><em>ein Kunstwerk</em></h2>
    <p>Willkommen bei Life is Good – deiner Anlaufstelle für wunderschöne Custom Torten, liebevoll handgefertigt in Münsingen. Egal ob Geburtstag, Hochzeit oder einfach so – wir kreieren für dich ein essbares Kunstwerk, das Herzen öffnet.</p>
    <a href="https://wa.me/41000000000" target="_blank" class="cta-btn">Jetzt bestellen</a>
  </div>
  <div class="welcome-visual reveal">
    <img src="/mnt/user-data/uploads/Bild_oben.jpg" alt="Bakery Atmosphäre">
  </div>
</section>

<div class="divider"><span></span><span class="divider-icon">✦</span><span></span></div>

<!-- PASTEL CARDS -->
<section class="cards-section" id="angebot">
  <div class="cards-inner reveal">
    <p class="section-eyebrow" style="text-align:center">Warum Life is Good</p>
    <h2 class="section-heading" style="text-align:center">Mit Liebe &amp; <em>Leidenschaft</em></h2>
    <div class="cards-grid">
      <div class="card card-peach reveal">
        <span class="card-icon">🎨</span>
        <h3>Individuelles Design</h3>
        <p>Jede Torte wird nach deinen Wünschen gestaltet – einzigartig, persönlich und unvergesslich schön.</p>
      </div>
      <div class="card card-rose reveal">
        <span class="card-icon">🫶</span>
        <h3>Frisch &amp; Handgemacht</h3>
        <p>Alle Kreationen entstehen mit frischen Zutaten und viel Herzblut – kein Kompromiss bei Qualität.</p>
      </div>
      <div class="card card-mint reveal">
        <span class="card-icon">✨</span>
        <h3>Instagram-würdig</h3>
        <p>Ästhetische Torten, die nicht nur köstlich schmecken, sondern auch auf dem Feed glänzen.</p>
      </div>
    </div>
  </div>
</section>

<!-- ORDER -->
<section class="order-section" id="order">
  <p class="section-eyebrow reveal">Deine Torte</p>
  <h2 class="section-heading reveal">Custom Cake<br><em>für dich</em></h2>
  <p class="reveal">Du hast eine Idee, wir machen sie wahr. Schreib uns direkt auf WhatsApp – wir melden uns schnellstmöglich bei dir und besprechen gemeinsam deine Traumtorte.</p>
  <a href="https://wa.me/41000000000" target="_blank" class="order-btn-big reveal">Torte anfragen 🩷</a>
</section>

<!-- LOCATION -->
<section class="location-section reveal" id="location">
  <p class="section-eyebrow">Wo du uns findest</p>
  <h2 class="section-heading">Wir sind in <em>Münsingen</em></h2>
  <div class="location-badge">
    <span>📍</span>
    <span>Münsingen, Kanton Bern, Schweiz</span>
  </div>
  <p style="margin-top:1.5rem;font-size:1.1rem;color:var(--text-mid);font-weight:300;line-height:1.8;max-width:520px;margin-left:auto;margin-right:auto;">
    Bestellungen nehmen wir per WhatsApp oder Instagram entgegen.<br>Lieferung &amp; Abholung nach Absprache möglich.
  </p>
</section>

<!-- TESTIMONIALS -->
<section class="testimonials reveal" id="testimonials">
  <p class="section-eyebrow">Was Kunden sagen</p>
  <h2 class="section-heading">Stimmen aus <em>der Region</em></h2>
  <div class="testimonials-grid">
    <div class="testimonial-card reveal">
      <div class="testimonial-stars">★★★★★</div>
      <p>„Die Torte war ein absoluter Traum – wunderschön und unglaublich lecker. Alle Gäste waren begeistert!"</p>
    </div>
    <div class="testimonial-card reveal">
      <div class="testimonial-stars">★★★★★</div>
      <p>„Mega lecker, alle haben den Kuchen super gefunden und er sah so schön aus. Danke von Herzen!"</p>
    </div>
    <div class="testimonial-card reveal">
      <div class="testimonial-stars">★★★★★</div>
      <p>„Everybody loved it! One of my friends said it was the best cake he ever tried. THANK YOU so much!"</p>
    </div>
  </div>
</section>

<div class="divider"><span></span><span class="divider-icon">✦</span><span></span></div>

<!-- SOCIAL -->
<section class="social-section reveal" id="kontakt">
  <p class="section-eyebrow">Verbinde dich mit uns</p>
  <h2 class="section-heading">Folge uns &amp;<br><em>schreib uns</em></h2>
  <div class="social-buttons">
    <a href="https://www.instagram.com/" target="_blank" class="social-btn social-btn-ig">
      <svg viewBox="0 0 24 24"><path d="M12 2.163c3.204 0 3.584.012 4.85.07 3.252.148 4.771 1.691 4.919 4.919.058 1.265.069 1.645.069 4.849 0 3.205-.012 3.584-.069 4.849-.149 3.225-1.664 4.771-4.919 4.919-1.266.058-1.644.07-4.85.07-3.204 0-3.584-.012-4.849-.07-3.26-.149-4.771-1.699-4.919-4.92-.058-1.265-.07-1.644-.07-4.849 0-3.204.013-3.583.07-4.849.149-3.227 1.664-4.771 4.919-4.919 1.266-.057 1.645-.069 4.849-.069zM12 0C8.741 0 8.333.014 7.053.072 2.695.272.273 2.69.073 7.052.014 8.333 0 8.741 0 12c0 3.259.014 3.668.072 4.948.2 4.358 2.618 6.78 6.98 6.98C8.333 23.986 8.741 24 12 24c3.259 0 3.668-.014 4.948-.072 4.354-.2 6.782-2.618 6.979-6.98.059-1.28.073-1.689.073-4.948 0-3.259-.014-3.667-.072-4.947-.196-4.354-2.617-6.78-6.979-6.98C15.668.014 15.259 0 12 0zm0 5.838a6.162 6.162 0 100 12.324 6.162 6.162 0 000-12.324zM12 16a4 4 0 110-8 4 4 0 010 8zm6.406-11.845a1.44 1.44 0 100 2.881 1.44 1.44 0 000-2.881z"/></svg>
      Instagram
    </a>
    <a href="https://wa.me/41000000000" target="_blank" class="social-btn social-btn-wa">
      <svg viewBox="0 0 24 24"><path d="M17.472 14.382c-.297-.149-1.758-.867-2.03-.967-.273-.099-.471-.148-.67.15-.197.297-.767.966-.94 1.164-.173.199-.347.223-.644.075-.297-.15-1.255-.463-2.39-1.475-.883-.788-1.48-1.761-1.653-2.059-.173-.297-.018-.458.13-.606.134-.133.298-.347.446-.52.149-.174.198-.298.298-.497.099-.198.05-.371-.025-.52-.075-.149-.669-1.612-.916-2.207-.242-.579-.487-.5-.669-.51-.173-.008-.371-.01-.57-.01-.198 0-.52.074-.792.372-.272.297-1.04 1.016-1.04 2.479 0 1.462 1.065 2.875 1.213 3.074.149.198 2.096 3.2 5.077 4.487.709.306 1.262.489 1.694.625.712.227 1.36.195 1.871.118.571-.085 1.758-.719 2.006-1.413.248-.694.248-1.289.173-1.413-.074-.124-.272-.198-.57-.347m-5.421 7.403h-.004a9.87 9.87 0 01-5.031-1.378l-.361-.214-3.741.982.998-3.648-.235-.374a9.86 9.86 0 01-1.51-5.26c.001-5.45 4.436-9.884 9.888-9.884 2.64 0 5.122 1.03 6.988 2.898a9.825 9.825 0 012.893 6.994c-.003 5.45-4.437 9.884-9.885 9.884m8.413-18.297A11.815 11.815 0 0012.05 0C5.495 0 .16 5.335.157 11.892c0 2.096.547 4.142 1.588 5.945L.057 24l6.305-1.654a11.882 11.882 0 005.683 1.448h.005c6.554 0 11.89-5.335 11.893-11.893a11.821 11.821 0 00-3.48-8.413z"/></svg>
      WhatsApp
    </a>
  </div>
</section>

<!-- FOOTER -->
<footer>
  <div class="footer-grid">
    <div>
      <img src="/mnt/user-data/uploads/eb63b7a6-e88f-4ab7-b942-ab5a2ea8bed8.JPG" alt="Life is Good" class="footer-logo-img">
      <p class="footer-desc">Handgefertigte Custom Torten und Desserts aus Münsingen – mit Liebe, Leidenschaft und einem Hauch Magie.</p>
    </div>
    <div>
      <p class="footer-heading">Öffnungszeiten</p>
      <ul class="hours-list">
        <li><span>Mo – Di</span><span>Geschlossen</span></li>
        <li><span>Mi – Do</span><span>14:30 – 21:30</span></li>
        <li><span>Freitag</span><span>14:30 – 23:00</span></li>
        <li><span>Samstag</span><span>15:00 – 23:00</span></li>
        <li><span>Sonntag</span><span>15:00 – 22:00</span></li>
      </ul>
    </div>
    <div>
      <p class="footer-heading">Kontakt</p>
      <ul class="contact-list">
        <li>📍 Münsingen, Kanton Bern</li>
        <li>📱 <a href="https://wa.me/41000000000">WhatsApp</a></li>
        <li>📸 <a href="https://www.instagram.com/" target="_blank">Instagram</a></li>
      </ul>
    </div>
  </div>
  <p class="footer-bottom">© 2026 Life is Good Bakery · Münsingen ✦ Made with 🩷</p>
</footer>

<script>
  // Cursor
  const cursor=document.getElementById('cursor'),ring=document.getElementById('cursorRing');
  let mx=0,my=0,rx=0,ry=0;
  document.addEventListener('mousemove',e=>{mx=e.clientX;my=e.clientY;});
  (function a(){cursor.style.left=mx+'px';cursor.style.top=my+'px';rx+=(mx-rx)*.15;ry+=(my-ry)*.15;ring.style.left=rx+'px';ring.style.top=ry+'px';requestAnimationFrame(a);})();
  document.querySelectorAll('a,button').forEach(el=>{
    el.addEventListener('mouseenter',()=>{cursor.style.width=cursor.style.height='20px';ring.style.width=ring.style.height='58px';ring.style.opacity='1';});
    el.addEventListener('mouseleave',()=>{cursor.style.width=cursor.style.height='12px';ring.style.width=ring.style.height='38px';ring.style.opacity='.45';});
  });

  // Nav
  window.addEventListener('scroll',()=>document.getElementById('navbar').classList.toggle('scrolled',scrollY>60));

  // Parallax
  window.addEventListener('scroll',()=>{const img=document.querySelector('.hero-img');if(img)img.style.transform=`translateY(${scrollY*.28}px)`;});

  // Reveal
  const obs=new IntersectionObserver(entries=>{entries.forEach((e,i)=>{if(e.isIntersecting){setTimeout(()=>e.target.classList.add('visible'),i*70);obs.unobserve(e.target);}});},{threshold:.1});
  document.querySelectorAll('.reveal').forEach(el=>obs.observe(el));

  // Particles – pastel rainbow
  const colors=['rgba(247,197,160,.5)','rgba(240,160,184,.5)','rgba(168,216,200,.5)','rgba(200,180,232,.5)','rgba(247,223,160,.5)'];
  const pc=document.getElementById('particles');
  for(let i=0;i<22;i++){
    const p=document.createElement('div'); p.classList.add('particle');
    const s=3+Math.random()*5;
    p.style.cssText=`left:${Math.random()*100}vw;width:${s}px;height:${s}px;background:${colors[i%colors.length]};animation-duration:${14+Math.random()*18}s;animation-delay:${Math.random()*16}s;opacity:${.2+Math.random()*.45}`;
    pc.appendChild(p);
  }
</script>
</body>
</html>
