<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0" />
<title>TurfBook — Book Your Game</title>
<link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700;900&display=swap" rel="stylesheet" />
<style>
  *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

  :root {
    --green: #1a9e5c;
    --green-dark: #127a44;
    --green-light: #e6f7ee;
    --green-mid: #2dc774;
    --turf: #0f6e3c;
    --turf-dark: #0a4a28;
    --accent: #f5a623;
    --accent-dark: #c87d0a;
    --text: #1a1a1a;
    --text-muted: #666;
    --bg: #f7f9f7;
    --card: #fff;
    --border: #e2e8e2;
    --stripe: rgba(255,255,255,0.06);
    --red: #e03e3e;
  }

  body {
    font-family: 'Inter', sans-serif;
    background: var(--bg);
    color: var(--text);
    min-height: 100vh;
  }

  /* HEADER */
  header {
    background: var(--turf-dark);
    padding: 0 2rem;
    display: flex;
    align-items: center;
    justify-content: space-between;
    height: 64px;
    position: sticky;
    top: 0;
    z-index: 100;
    box-shadow: 0 2px 12px rgba(0,0,0,0.18);
  }

  .logo {
    display: flex;
    align-items: center;
    gap: 10px;
    text-decoration: none;
  }

  .logo-icon {
    width: 36px; height: 36px;
    background: var(--green-mid);
    border-radius: 8px;
    display: flex; align-items: center; justify-content: center;
    font-size: 18px;
  }

  .logo-text {
    font-size: 20px;
    font-weight: 900;
    color: #fff;
    letter-spacing: -0.5px;
  }

  .logo-text span { color: var(--green-mid); }

  nav { display: flex; gap: 8px; }
  nav a {
    color: rgba(255,255,255,0.75);
    text-decoration: none;
    font-size: 14px;
    font-weight: 500;
    padding: 6px 14px;
    border-radius: 6px;
    transition: background 0.15s, color 0.15s;
  }
  nav a:hover { background: rgba(255,255,255,0.1); color: #fff; }
  nav a.active { background: var(--green); color: #fff; }

  /* HERO */
  .hero {
    background: var(--turf-dark);
    padding: 3.5rem 2rem 5rem;
    text-align: center;
    position: relative;
    overflow: hidden;
  }

  .hero::before {
    content: '';
    position: absolute;
    inset: 0;
    background-image:
      repeating-linear-gradient(0deg, var(--stripe) 0px, var(--stripe) 1px, transparent 1px, transparent 40px),
      repeating-linear-gradient(90deg, var(--stripe) 0px, var(--stripe) 1px, transparent 1px, transparent 80px);
    pointer-events: none;
  }

  .hero-tag {
    display: inline-block;
    background: var(--green);
    color: #fff;
    font-size: 12px;
    font-weight: 600;
    text-transform: uppercase;
    letter-spacing: 1.5px;
    padding: 4px 12px;
    border-radius: 20px;
    margin-bottom: 1.25rem;
  }

  .hero h1 {
    font-size: clamp(2rem, 5vw, 3.2rem);
    font-weight: 900;
    color: #fff;
    letter-spacing: -1px;
    line-height: 1.1;
    margin-bottom: 1rem;
  }

  .hero h1 span { color: var(--green-mid); }

  .hero p {
    color: rgba(255,255,255,0.65);
    font-size: 1.05rem;
    max-width: 500px;
    margin: 0 auto 2rem;
    line-height: 1.6;
  }

  /* SEARCH BAR */
  .search-bar {
    background: #fff;
    border-radius: 14px;
    padding: 10px;
    display: flex;
    gap: 8px;
    max-width: 620px;
    margin: 0 auto;
    box-shadow: 0 4px 24px rgba(0,0,0,0.18);
    position: relative;
    z-index: 1;
  }

  .search-bar select,
  .search-bar input {
    flex: 1;
    border: none;
    outline: none;
    font-size: 14px;
    padding: 8px 12px;
    border-radius: 8px;
    background: var(--bg);
    color: var(--text);
    font-family: inherit;
    cursor: pointer;
  }

  .search-bar button {
    background: var(--green);
    color: #fff;
    border: none;
    padding: 10px 22px;
    border-radius: 8px;
    font-size: 14px;
    font-weight: 600;
    cursor: pointer;
    transition: background 0.15s;
    white-space: nowrap;
  }
  .search-bar button:hover { background: var(--green-dark); }

  /* STATS STRIP */
  .stats-strip {
    background: var(--green);
    display: flex;
    justify-content: center;
    gap: 0;
  }

  .stat-item {
    text-align: center;
    padding: 1rem 2.5rem;
    border-right: 1px solid rgba(255,255,255,0.2);
  }
  .stat-item:last-child { border-right: none; }

  .stat-item strong {
    display: block;
    font-size: 1.4rem;
    font-weight: 900;
    color: #fff;
  }
  .stat-item span {
    font-size: 12px;
    color: rgba(255,255,255,0.75);
    text-transform: uppercase;
    letter-spacing: 0.8px;
  }

  /* MAIN CONTENT */
  .container {
    max-width: 1100px;
    margin: 0 auto;
    padding: 0 2rem;
  }

  /* SECTION TITLES */
  .section-title {
    font-size: 1.5rem;
    font-weight: 800;
    color: var(--text);
    letter-spacing: -0.5px;
    margin-bottom: 0.4rem;
  }
  .section-sub {
    color: var(--text-muted);
    font-size: 14px;
    margin-bottom: 2rem;
  }

  /* TURF CARDS */
  .turfs-section { padding: 3rem 0; }

  .filter-row {
    display: flex;
    gap: 8px;
    margin-bottom: 1.75rem;
    flex-wrap: wrap;
  }

  .filter-btn {
    padding: 6px 16px;
    border-radius: 20px;
    border: 1.5px solid var(--border);
    background: var(--card);
    color: var(--text-muted);
    font-size: 13px;
    font-weight: 500;
    cursor: pointer;
    transition: all 0.15s;
    font-family: inherit;
  }
  .filter-btn:hover { border-color: var(--green); color: var(--green); }
  .filter-btn.active { background: var(--green); border-color: var(--green); color: #fff; }

  .turfs-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
    gap: 1.5rem;
  }

  .turf-card {
    background: var(--card);
    border-radius: 16px;
    border: 1px solid var(--border);
    overflow: hidden;
    transition: transform 0.18s, box-shadow 0.18s;
    cursor: pointer;
  }
  .turf-card:hover { transform: translateY(-4px); box-shadow: 0 12px 32px rgba(0,0,0,0.10); }

  .turf-banner {
    height: 140px;
    position: relative;
    display: flex;
    align-items: flex-end;
    padding: 1rem;
  }

  .turf-badge {
    background: rgba(0,0,0,0.55);
    color: #fff;
    font-size: 11px;
    font-weight: 600;
    padding: 3px 10px;
    border-radius: 20px;
    backdrop-filter: blur(4px);
  }

  .availability-dot {
    width: 8px; height: 8px;
    border-radius: 50%;
    display: inline-block;
    margin-right: 5px;
  }
  .dot-green { background: #2dc774; }
  .dot-red { background: var(--red); }

  .turf-body { padding: 1.25rem; }

  .turf-name {
    font-size: 1.1rem;
    font-weight: 800;
    letter-spacing: -0.3px;
    margin-bottom: 4px;
    color: var(--text);
  }

  .turf-meta {
    display: flex;
    gap: 12px;
    font-size: 12px;
    color: var(--text-muted);
    margin-bottom: 1rem;
  }
  .turf-meta span { display: flex; align-items: center; gap: 4px; }

  .turf-tags {
    display: flex;
    gap: 6px;
    flex-wrap: wrap;
    margin-bottom: 1rem;
  }
  .tag {
    background: var(--green-light);
    color: var(--green-dark);
    font-size: 11px;
    font-weight: 600;
    padding: 3px 9px;
    border-radius: 20px;
  }

  .turf-footer {
    display: flex;
    align-items: center;
    justify-content: space-between;
    padding-top: 1rem;
    border-top: 1px solid var(--border);
  }

  .price {
    font-size: 1.3rem;
    font-weight: 900;
    color: var(--turf);
  }
  .price small {
    font-size: 13px;
    font-weight: 500;
    color: var(--text-muted);
  }

  .book-btn {
    background: var(--green);
    color: #fff;
    border: none;
    padding: 9px 20px;
    border-radius: 8px;
    font-size: 13px;
    font-weight: 700;
    cursor: pointer;
    transition: background 0.15s;
    font-family: inherit;
  }
  .book-btn:hover { background: var(--green-dark); }

  /* RATING STARS */
  .stars { color: var(--accent); font-size: 13px; letter-spacing: 1px; }

  /* MODAL */
  .modal-overlay {
    display: none;
    position: fixed;
    inset: 0;
    background: rgba(0,0,0,0.55);
    z-index: 200;
    align-items: center;
    justify-content: center;
    padding: 1rem;
  }
  .modal-overlay.open { display: flex; }

  .modal {
    background: var(--card);
    border-radius: 20px;
    max-width: 520px;
    width: 100%;
    max-height: 90vh;
    overflow-y: auto;
    box-shadow: 0 24px 64px rgba(0,0,0,0.25);
    animation: slideUp 0.22s ease;
  }

  @keyframes slideUp {
    from { transform: translateY(20px); opacity: 0; }
    to { transform: translateY(0); opacity: 1; }
  }

  .modal-header {
    padding: 1.5rem 1.5rem 0;
    display: flex;
    justify-content: space-between;
    align-items: flex-start;
  }

  .modal-header h2 { font-size: 1.25rem; font-weight: 800; }
  .modal-close {
    background: var(--bg);
    border: none;
    width: 32px; height: 32px;
    border-radius: 50%;
    font-size: 18px;
    cursor: pointer;
    display: flex; align-items: center; justify-content: center;
    color: var(--text-muted);
    flex-shrink: 0;
  }
  .modal-close:hover { background: var(--border); }

  .modal-body { padding: 1.25rem 1.5rem 1.5rem; }

  .form-group { margin-bottom: 1.1rem; }
  .form-group label {
    display: block;
    font-size: 13px;
    font-weight: 600;
    margin-bottom: 6px;
    color: var(--text-muted);
    text-transform: uppercase;
    letter-spacing: 0.5px;
  }

  .form-group input,
  .form-group select {
    width: 100%;
    padding: 10px 14px;
    border: 1.5px solid var(--border);
    border-radius: 10px;
    font-size: 14px;
    font-family: inherit;
    outline: none;
    background: var(--bg);
    transition: border-color 0.15s;
    color: var(--text);
  }
  .form-group input:focus,
  .form-group select:focus { border-color: var(--green); }

  .time-grid {
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    gap: 8px;
    margin-top: 4px;
  }
  .time-slot {
    padding: 8px 4px;
    border-radius: 8px;
    border: 1.5px solid var(--border);
    font-size: 12px;
    font-weight: 600;
    text-align: center;
    cursor: pointer;
    background: var(--card);
    transition: all 0.15s;
    font-family: inherit;
    color: var(--text);
  }
  .time-slot:hover { border-color: var(--green); color: var(--green); }
  .time-slot.selected { background: var(--green); border-color: var(--green); color: #fff; }
  .time-slot.booked { background: var(--bg); color: var(--border); cursor: not-allowed; border-color: var(--border); }

  .summary-box {
    background: var(--green-light);
    border-radius: 12px;
    padding: 1rem 1.25rem;
    margin: 1.25rem 0;
  }

  .summary-row {
    display: flex;
    justify-content: space-between;
    font-size: 14px;
    padding: 3px 0;
    color: var(--text-muted);
  }
  .summary-row strong { color: var(--text); font-weight: 700; }
  .summary-total {
    display: flex;
    justify-content: space-between;
    font-size: 16px;
    font-weight: 800;
    color: var(--turf);
    padding-top: 8px;
    margin-top: 8px;
    border-top: 1px solid rgba(15,110,60,0.2);
  }

  .confirm-btn {
    width: 100%;
    padding: 14px;
    background: var(--green);
    color: #fff;
    border: none;
    border-radius: 12px;
    font-size: 15px;
    font-weight: 800;
    cursor: pointer;
    transition: background 0.15s;
    font-family: inherit;
    letter-spacing: -0.2px;
  }
  .confirm-btn:hover { background: var(--green-dark); }

  /* SUCCESS */
  .success-screen {
    text-align: center;
    padding: 2rem 1.5rem;
  }
  .success-icon {
    width: 72px; height: 72px;
    background: var(--green-light);
    border-radius: 50%;
    display: flex; align-items: center; justify-content: center;
    font-size: 32px;
    margin: 0 auto 1rem;
  }
  .success-screen h2 { font-size: 1.3rem; font-weight: 800; margin-bottom: 8px; }
  .success-screen p { color: var(--text-muted); font-size: 14px; line-height: 1.6; }
  .booking-ref {
    background: var(--turf-dark);
    color: var(--green-mid);
    font-size: 1.1rem;
    font-weight: 900;
    letter-spacing: 2px;
    padding: 10px 20px;
    border-radius: 8px;
    display: inline-block;
    margin: 1rem 0;
    font-family: monospace;
  }
  .done-btn {
    background: var(--green);
    color: #fff;
    border: none;
    padding: 11px 28px;
    border-radius: 10px;
    font-size: 14px;
    font-weight: 700;
    cursor: pointer;
    font-family: inherit;
    margin-top: 0.5rem;
  }

  /* TESTIMONIALS */
  .testimonials { padding: 3rem 0; background: var(--card); border-top: 1px solid var(--border); border-bottom: 1px solid var(--border); }
  .t-grid { display: grid; grid-template-columns: repeat(auto-fill, minmax(260px, 1fr)); gap: 1.25rem; margin-top: 2rem; }
  .t-card {
    background: var(--bg);
    border-radius: 14px;
    padding: 1.25rem;
    border: 1px solid var(--border);
  }
  .t-card p { font-size: 14px; line-height: 1.6; color: var(--text); margin-bottom: 1rem; }
  .t-author { display: flex; align-items: center; gap: 10px; }
  .avatar {
    width: 36px; height: 36px;
    border-radius: 50%;
    display: flex; align-items: center; justify-content: center;
    font-weight: 700; font-size: 13px; color: #fff;
    flex-shrink: 0;
  }
  .t-name { font-size: 13px; font-weight: 700; }
  .t-meta { font-size: 12px; color: var(--text-muted); }

  /* FOOTER */
  footer {
    background: var(--turf-dark);
    color: rgba(255,255,255,0.6);
    text-align: center;
    padding: 2rem;
    font-size: 13px;
  }
  footer strong { color: var(--green-mid); }

  /* NOTIFICATION TOAST */
  .toast {
    position: fixed;
    bottom: 24px;
    right: 24px;
    background: var(--turf-dark);
    color: #fff;
    padding: 12px 20px;
    border-radius: 12px;
    font-size: 14px;
    font-weight: 600;
    box-shadow: 0 8px 24px rgba(0,0,0,0.25);
    transform: translateY(80px);
    opacity: 0;
    transition: all 0.3s;
    z-index: 300;
  }
  .toast.show { transform: translateY(0); opacity: 1; }

  @media (max-width: 600px) {
    .stats-strip { flex-wrap: wrap; }
    .stat-item { border-right: none; border-bottom: 1px solid rgba(255,255,255,0.2); width: 50%; }
    nav { display: none; }
    .time-grid { grid-template-columns: repeat(3, 1fr); }
  }
</style>
</head>
<body>

<!-- HEADER -->
<header>
  <a class="logo" href="#">
    <div class="logo-icon">⚽</div>
    <div class="logo-text">Turf<span>Book</span></div>
  </a>
  <nav>
    <a href="#" class="active">Turfs</a>
    <a href="#bookings">My Bookings</a>
    <a href="#contact">Contact</a>
  </nav>
</header>

<!-- HERO -->
<section class="hero">
  <div class="hero-tag">⚡ Instant Confirmation</div>
  <h1>Book Your <span>Perfect Turf</span><br/>Play Today</h1>
  <p>5 premium turfs. Real-time availability. Zero hassle. Pick your slot and get on the field.</p>
  <div class="search-bar">
    <select id="heroTurfFilter">
      <option value="">All Turfs</option>
      <option value="Riyan">Riyan</option>
      <option value="2innings">2innings</option>
      <option value="Mh04">Mh04</option>
      <option value="Hit-wicket">Hit-wicket</option>
      <option value="Arena">Arena</option>
    </select>
    <input type="date" id="heroDate" />
    <button onclick="scrollToTurfs()">Find Turf →</button>
  </div>
</section>

<!-- STATS -->
<div class="stats-strip">
  <div class="stat-item"><strong>5</strong><span>Premium Turfs</span></div>
  <div class="stat-item"><strong>500+</strong><span>Games Played</span></div>
  <div class="stat-item"><strong>4.8★</strong><span>Avg Rating</span></div>
  <div class="stat-item"><strong>24/7</strong><span>Booking Support</span></div>
</div>

<!-- TURFS -->
<section class="turfs-section" id="turfs">
  <div class="container">
    <h2 class="section-title">Available Turfs</h2>
    <p class="section-sub">Choose from our top-rated venues and lock in your slot</p>

    <div class="filter-row">
      <button class="filter-btn active" onclick="filterTurfs('all', this)">All</button>
      <button class="filter-btn" onclick="filterTurfs('budget', this)">Budget (≤₹600)</button>
      <button class="filter-btn" onclick="filterTurfs('premium', this)">Premium (>₹600)</button>
      <button class="filter-btn" onclick="filterTurfs('available', this)">Available Now</button>
    </div>

    <div class="turfs-grid" id="turfsGrid"></div>
  </div>
</section>

<!-- TESTIMONIALS -->
<section class="testimonials" id="bookings">
  <div class="container">
    <h2 class="section-title">What players say</h2>
    <p class="section-sub">Real reviews from the TurfBook community</p>
    <div class="t-grid">
      <div class="t-card">
        <div class="stars">★★★★★</div>
        <p>"Booked Arena for a Sunday 7s match. The turf was flawless and booking took under 2 minutes. Will be back every weekend!"</p>
        <div class="t-author">
          <div class="avatar" style="background:#0f6e3c;">RK</div>
          <div><div class="t-name">Rahul K.</div><div class="t-meta">Arena regular · 12 bookings</div></div>
        </div>
      </div>
      <div class="t-card">
        <div class="stars">★★★★★</div>
        <p>"2innings is perfect for our cricket practice. Love that the slot system is so transparent — no surprise double bookings."</p>
        <div class="t-author">
          <div class="avatar" style="background:#185fa5;">AM</div>
          <div><div class="t-name">Arjun M.</div><div class="t-meta">2innings fan · 8 bookings</div></div>
        </div>
      </div>
      <div class="t-card">
        <div class="stars">★★★★☆</div>
        <p>"Hit-wicket is great value. Floodlights are top-notch for evening matches. Riyan is a bit pricey but worth it for the surface quality."</p>
        <div class="t-author">
          <div class="avatar" style="background:#854f0b;">SP</div>
          <div><div class="t-name">Sneha P.</div><div class="t-meta">Multi-turf · 5 bookings</div></div>
        </div>
      </div>
    </div>
  </div>
</section>

<!-- FOOTER -->
<footer id="contact">
  <strong>TurfBook</strong> — All 5 turfs in one place.<br/>
  <span style="font-size:12px; margin-top:4px; display:block;">📍 Mumbai &nbsp;|&nbsp; 📞 +91 98765 43210 &nbsp;|&nbsp; ✉️ hello@turfbook.in</span>
</footer>

<!-- TOAST -->
<div class="toast" id="toast"></div>

<!-- BOOKING MODAL -->
<div class="modal-overlay" id="modalOverlay" onclick="closeModal(event)">
  <div class="modal" id="modal">
    <div id="modalContent"></div>
  </div>
</div>

<script>
  const TURFS = [
    {
      id: 1, name: "Riyan", price: 1000,
      color: "#0f6e3c", emoji: "🏟️",
      tags: ["Floodlit", "Premium Surface", "Parking"],
      rating: 4.9, reviews: 87,
      available: true, surface: "Artificial grass",
      capacity: "11v11",
      bookedSlots: ["08:00","09:00","14:00"]
    },
    {
      id: 2, name: "2innings", price: 500,
      color: "#185fa5", emoji: "🏏",
      tags: ["Cricket", "Nets Available", "Coaching"],
      rating: 4.7, reviews: 63,
      available: true, surface: "Concrete + matting",
      capacity: "6v6",
      bookedSlots: ["10:00","11:00"]
    },
    {
      id: 3, name: "Mh04", price: 800,
      color: "#7f77dd", emoji: "⚽",
      tags: ["Floodlit", "Turf Shoes Req.", "Canteen"],
      rating: 4.8, reviews: 112,
      available: false, surface: "FIFA approved turf",
      capacity: "7v7",
      bookedSlots: ["06:00","07:00","08:00","09:00","10:00","11:00","12:00","13:00","14:00","15:00","16:00","17:00","18:00","19:00","20:00","21:00"]
    },
    {
      id: 4, name: "Hit-wicket", price: 600,
      color: "#993c1d", emoji: "🏏",
      tags: ["Cricket Specialist", "Box Cricket"],
      rating: 4.6, reviews: 45,
      available: true, surface: "Synthetic mat",
      capacity: "8v8",
      bookedSlots: ["07:00","12:00","18:00","19:00"]
    },
    {
      id: 5, name: "Arena", price: 700,
      color: "#854f0b", emoji: "🥅",
      tags: ["Dual Sport", "Spectator Stands", "Washrooms"],
      rating: 4.8, reviews: 98,
      available: true, surface: "Hybrid grass",
      capacity: "11v11",
      bookedSlots: ["06:00","07:00","20:00","21:00"]
    }
  ];

  const TIME_SLOTS = ["06:00","07:00","08:00","09:00","10:00","11:00","12:00","13:00","14:00","15:00","16:00","17:00","18:00","19:00","20:00","21:00"];

  let selectedTime = null;
  let selectedHours = 1;
  let currentTurf = null;

  function starsHTML(r) {
    return '★'.repeat(Math.floor(r)) + (r%1>=0.5?'½':'') + '☆'.repeat(5-Math.ceil(r));
  }

  function renderCards(filter='all') {
    const grid = document.getElementById('turfsGrid');
    let turfs = TURFS;
    if(filter==='budget') turfs = TURFS.filter(t=>t.price<=600);
    if(filter==='premium') turfs = TURFS.filter(t=>t.price>600);
    if(filter==='available') turfs = TURFS.filter(t=>t.available);

    grid.innerHTML = turfs.map(t => `
      <div class="turf-card" onclick="openModal(${t.id})">
        <div class="turf-banner" style="background: linear-gradient(135deg, ${t.color}ee, ${t.color}99);">
          <div style="position:absolute;top:14px;right:14px;font-size:2.2rem;">${t.emoji}</div>
          <div class="turf-badge">
            <span class="availability-dot ${t.available?'dot-green':'dot-red'}"></span>
            ${t.available ? 'Slots Available' : 'Fully Booked'}
          </div>
        </div>
        <div class="turf-body">
          <div class="turf-name">${t.name}</div>
          <div class="turf-meta">
            <span>⭐ ${t.rating} (${t.reviews} reviews)</span>
            <span>👥 ${t.capacity}</span>
            <span>🌿 ${t.surface}</span>
          </div>
          <div class="turf-tags">${t.tags.map(tag=>`<span class="tag">${tag}</span>`).join('')}</div>
          <div class="turf-footer">
            <div class="price">₹${t.price.toLocaleString('en-IN')}<small>/hr</small></div>
            <button class="book-btn" ${!t.available?'disabled style="opacity:0.4;cursor:not-allowed;"':''}>
              ${t.available ? 'Book Now' : 'Unavailable'}
            </button>
          </div>
        </div>
      </div>
    `).join('');
  }

  function filterTurfs(f, btn) {
    document.querySelectorAll('.filter-btn').forEach(b=>b.classList.remove('active'));
    btn.classList.add('active');
    renderCards(f);
  }

  function openModal(id) {
    currentTurf = TURFS.find(t=>t.id===id);
    if(!currentTurf || !currentTurf.available) return;
    selectedTime = null;
    selectedHours = 1;
    renderBookingForm();
    document.getElementById('modalOverlay').classList.add('open');
  }

  function renderBookingForm() {
    const t = currentTurf;
    const today = new Date().toISOString().split('T')[0];
    document.getElementById('modalContent').innerHTML = `
      <div class="modal-header">
        <div>
          <div style="font-size:12px;text-transform:uppercase;letter-spacing:1px;color:var(--text-muted);margin-bottom:4px;">${t.emoji} Book Turf</div>
          <h2>${t.name}</h2>
        </div>
        <button class="modal-close" onclick="closeModalDirect()">✕</button>
      </div>
      <div class="modal-body">
        <div class="form-group">
          <label>Your Name</label>
          <input type="text" id="bookName" placeholder="Enter your name" />
        </div>
        <div class="form-group">
          <label>Phone Number</label>
          <input type="tel" id="bookPhone" placeholder="+91 XXXXX XXXXX" />
        </div>
        <div class="form-group">
          <label>Date</label>
          <input type="date" id="bookDate" value="${today}" min="${today}" />
        </div>
        <div class="form-group">
          <label>Pick a Time Slot</label>
          <div class="time-grid" id="timeGrid">
            ${TIME_SLOTS.map(slot => {
              const booked = t.bookedSlots.includes(slot);
              return `<button class="time-slot ${booked?'booked':''}" 
                ${booked?'disabled':''} onclick="selectTime('${slot}', this)">${slot}</button>`;
            }).join('')}
          </div>
        </div>
        <div class="form-group">
          <label>Duration (hours)</label>
          <select id="bookHours" onchange="updateHours(this.value)">
            <option value="1">1 hour</option>
            <option value="2">2 hours</option>
            <option value="3">3 hours</option>
          </select>
        </div>
        <div class="summary-box" id="summaryBox" style="display:none;">
          <div class="summary-row"><span>Turf</span><strong>${t.name}</strong></div>
          <div class="summary-row"><span>Slot</span><strong id="sumSlot">—</strong></div>
          <div class="summary-row"><span>Duration</span><strong id="sumDur">1 hr</strong></div>
          <div class="summary-total"><span>Total</span><span id="sumTotal">₹${t.price.toLocaleString('en-IN')}</span></div>
        </div>
        <button class="confirm-btn" onclick="confirmBooking()">Confirm Booking →</button>
      </div>
    `;
  }

  function selectTime(slot, btn) {
    document.querySelectorAll('.time-slot').forEach(b=>b.classList.remove('selected'));
    btn.classList.add('selected');
    selectedTime = slot;
    updateSummary();
  }

  function updateHours(val) {
    selectedHours = parseInt(val);
    updateSummary();
  }

  function updateSummary() {
    if(!selectedTime) return;
    const box = document.getElementById('summaryBox');
    box.style.display = 'block';
    document.getElementById('sumSlot').textContent = selectedTime;
    document.getElementById('sumDur').textContent = selectedHours + (selectedHours>1?' hrs':' hr');
    document.getElementById('sumTotal').textContent = '₹' + (currentTurf.price * selectedHours).toLocaleString('en-IN');
  }

  function confirmBooking() {
    const name = document.getElementById('bookName').value.trim();
    const phone = document.getElementById('bookPhone').value.trim();
    const date = document.getElementById('bookDate').value;
    if(!name) { showToast('Please enter your name'); return; }
    if(!phone) { showToast('Please enter your phone number'); return; }
    if(!selectedTime) { showToast('Please select a time slot'); return; }

    const ref = 'TB' + Math.random().toString(36).substr(2,7).toUpperCase();
    const total = (currentTurf.price * selectedHours).toLocaleString('en-IN');

    document.getElementById('modalContent').innerHTML = `
      <div class="success-screen">
        <div class="success-icon">✅</div>
        <h2>Booking Confirmed!</h2>
        <p>You're all set, <strong>${name}</strong>! Your slot at <strong>${currentTurf.name}</strong> is locked in.</p>
        <div class="booking-ref">${ref}</div>
        <div style="font-size:13px;color:var(--text-muted);margin-bottom:1rem;">
          📅 ${date} &nbsp;|&nbsp; ⏰ ${selectedTime} (${selectedHours}hr) &nbsp;|&nbsp; 💰 ₹${total}
        </div>
        <p style="font-size:13px;color:var(--text-muted);">A confirmation will be sent to your number.</p>
        <button class="done-btn" onclick="closeModalDirect()">Done</button>
      </div>
    `;
    showToast('🎉 Booking confirmed for ' + currentTurf.name);
  }

  function closeModal(e) {
    if(e.target===document.getElementById('modalOverlay')) closeModalDirect();
  }
  function closeModalDirect() {
    document.getElementById('modalOverlay').classList.remove('open');
  }

  function showToast(msg) {
    const t = document.getElementById('toast');
    t.textContent = msg;
    t.classList.add('show');
    setTimeout(()=>t.classList.remove('show'), 3000);
  }

  function scrollToTurfs() {
    const filter = document.getElementById('heroTurfFilter').value;
    document.getElementById('turfs').scrollIntoView({ behavior:'smooth' });
    if(filter) {
      setTimeout(()=>{
        const card = [...document.querySelectorAll('.turf-card')].find(c=>
          c.querySelector('.turf-name')?.textContent === filter
        );
        if(card) card.scrollIntoView({behavior:'smooth', block:'center'});
      }, 600);
    }
  }

  // Set today's date on hero datepicker
  document.getElementById('heroDate').value = new Date().toISOString().split('T')[0];

  renderCards();
</script>
</body>
</html>
