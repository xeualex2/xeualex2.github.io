<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>Valentine?</title>
  <style>
    :root{
      --bg1:#fff0f6;
      --bg2:#ffe8f1;
      --card:#ffffffcc;
      --text:#2b2b2b;
      --yes:#ff4d6d;
      --yes2:#ff8fa3;
      --no:#6c757d;
      --shadow: 0 20px 50px rgba(0,0,0,.12);
    }
    *{box-sizing:border-box}
    body{
      margin:0;
      min-height:100vh;
      display:grid;
      place-items:center;
      font-family: ui-sans-serif, system-ui, -apple-system, Segoe UI, Roboto, Helvetica, Arial;
      color:var(--text);
      background:
        radial-gradient(1200px 600px at 20% 10%, var(--bg2), transparent 60%),
        radial-gradient(900px 500px at 90% 30%, #ffe3ed, transparent 55%),
        linear-gradient(180deg, var(--bg1), #fff);
      overflow:hidden;
    }

    .card{
      width:min(920px, 92vw);
      padding: clamp(18px, 3vw, 34px);
      background:var(--card);
      backdrop-filter: blur(10px);
      border: 1px solid rgba(255,255,255,.6);
      border-radius: 26px;
      box-shadow: var(--shadow);
      position:relative;
    }

    .layout{
      display:grid;
      grid-template-columns: 1fr 1.05fr;
      gap: clamp(14px, 3vw, 30px);
      align-items:center;
    }

    @media (max-width: 760px){
      .layout{grid-template-columns:1fr; text-align:center;}
    }

    h1{
      margin:0 0 14px 0;
      font-size: clamp(30px, 4vw, 52px);
      line-height:1.05;
      letter-spacing:-.02em;
    }
    .sub{
      margin:0 0 18px 0;
      font-size: clamp(14px, 1.6vw, 18px);
      opacity:.85;
    }

    .stage{
      display:grid;
      place-items:center;
      padding: 10px;
    }

    /* Buttons area */
    .cta-wrap{
      position:relative;
      height: 96px;
      margin-top: 10px;
    }
    .btn{
      border:0;
      border-radius: 999px;
      padding: 14px 22px;
      font-size: 18px;
      font-weight: 700;
      cursor:pointer;
      box-shadow: 0 12px 25px rgba(0,0,0,.12);
      transition: transform .15s ease, filter .15s ease;
      user-select:none;
      touch-action: manipulation;
      position:absolute;
      top: 18px;
      left: 0;
      will-change: transform, left, top;
    }
    .btn:hover{transform: translateY(-1px) scale(1.02);}
    .btn:active{transform: translateY(0px) scale(0.98);}

    #yesBtn{
      background: linear-gradient(135deg, var(--yes), var(--yes2));
      color:white;
      left: 0;
    }
    #noBtn{
      background: linear-gradient(135deg, #adb5bd, var(--no));
      color:white;
      left: 170px;
    }

    .hint{
      font-size: 13px;
      opacity:.7;
      margin-top: 8px;
    }

    /* Cute bear SVG sizing */
    .bear svg{
      width: min(340px, 70vw);
      height:auto;
      filter: drop-shadow(0 18px 22px rgba(0,0,0,.12));
    }

    /* Floating hearts background */
    .hearts{
      position:absolute; inset:0;
      pointer-events:none;
      overflow:hidden;
      border-radius: 26px;
    }
    .heart{
      position:absolute;
      width:16px; height:16px;
      opacity:.25;
      transform: rotate(45deg);
      background: #ff4d6d;
      animation: floatUp linear infinite;
    }
    .heart::before, .heart::after{
      content:"";
      position:absolute;
      width:16px; height:16px;
      background:#ff4d6d;
      border-radius:50%;
    }
    .heart::before{left:-8px; top:0}
    .heart::after{left:0; top:-8px}

    @keyframes floatUp{
      from { transform: translateY(120%) rotate(45deg); }
      to   { transform: translateY(-140%) rotate(45deg); }
    }

    .success{
      display:none;
      margin-top:10px;
      font-weight:800;
      color:#d00042;
      font-size: 20px;
    }
    .success.show{display:block;}
  </style>
</head>
<body>
  <div class="card" id="card">
    <div class="hearts" id="hearts"></div>

    <div class="layout">
      <div>
        <h1>Do you want to be my valentine?</h1>
        <p class="sub">Choose wisely… 💘</p>

        <div class="cta-wrap" id="ctaArea">
          <button class="btn" id="yesBtn" aria-label="Yes">Yes 💖</button>
          <button class="btn" id="noBtn" aria-label="No">No 🙈</button>
        </div>
        <div class="hint">Tip: the “No” button is a little… shy.</div>
        <div class="success" id="successText">YAY!!! 🎉💞</div>
      </div>

      <div class="stage">
        <div class="bear" id="bearArt" aria-hidden="true">
          <!-- Bear holding heart (default) -->
          <svg viewBox="0 0 420 420" fill="none" xmlns="http://www.w3.org/2000/svg">
            <!-- ears -->
            <circle cx="130" cy="120" r="45" fill="#B67C52"/>
            <circle cx="290" cy="120" r="45" fill="#B67C52"/>
            <circle cx="130" cy="120" r="25" fill="#E7C6A7"/>
            <circle cx="290" cy="120" r="25" fill="#E7C6A7"/>

            <!-- head -->
            <circle cx="210" cy="185" r="120" fill="#C58A5A"/>
            <ellipse cx="210" cy="230" rx="78" ry="60" fill="#E7C6A7"/>

            <!-- eyes -->
            <circle cx="170" cy="185" r="10" fill="#2B2B2B"/>
            <circle cx="250" cy="185" r="10" fill="#2B2B2B"/>
            <circle cx="166" cy="180" r="3" fill="#fff" opacity=".8"/>
            <circle cx="246" cy="180" r="3" fill="#fff" opacity=".8"/>

            <!-- nose + mouth -->
            <path d="M200 218c0-10 8-18 18-18s18 8 18 18c0 10-8 16-18 16s-18-6-18-16Z" fill="#2B2B2B"/>
            <path d="M210 234c0 14-18 18-28 10" stroke="#2B2B2B" stroke-width="6" stroke-linecap="round"/>
            <path d="M210 234c0 14 18 18 28 10" stroke="#2B2B2B" stroke-width="6" stroke-linecap="round"/>

            <!-- body -->
            <ellipse cx="210" cy="322" rx="120" ry="90" fill="#C58A5A"/>
            <ellipse cx="210" cy="340" rx="78" ry="58" fill="#E7C6A7"/>

            <!-- arms -->
            <ellipse cx="115" cy="315" rx="55" ry="40" fill="#C58A5A" transform="rotate(-18 115 315)"/>
            <ellipse cx="305" cy="315" rx="55" ry="40" fill="#C58A5A" transform="rotate(18 305 315)"/>

            <!-- heart -->
            <g transform="translate(210 300)">
              <path d="M0 35s-55-35-55-78c0-20 16-36 36-36 14 0 26 8 32 20 6-12 18-20 32-20 20 0 36 16 36 36C81 0 0 35 0 35Z"
                fill="#FF4D6D" stroke="#D00042" stroke-width="6" stroke-linejoin="round"/>
            </g>

            <!-- blush -->
            <circle cx="150" cy="215" r="12" fill="#ff7aa2" opacity=".45"/>
            <circle cx="270" cy="215" r="12" fill="#ff7aa2" opacity=".45"/>
          </svg>
        </div>
      </div>
    </div>
  </div>

  <script>
    // Floating hearts
    const hearts = document.getElementById('hearts');
    for (let i = 0; i < 18; i++) {
      const h = document.createElement('div');
      h.className = 'heart';
      h.style.left = Math.random() * 100 + '%';
      h.style.animationDuration = (6 + Math.random() * 8) + 's';
      h.style.animationDelay = (-Math.random() * 10) + 's';
      h.style.opacity = (0.12 + Math.random() * 0.25).toFixed(2);
      h.style.transform = `translateY(${100 + Math.random() * 120}%) rotate(45deg)`;
      h.style.width = h.style.height = (10 + Math.random() * 14) + 'px';
      hearts.appendChild(h);
    }

    const ctaArea = document.getElementById('ctaArea');
    const noBtn = document.getElementById('noBtn');
    const yesBtn = document.getElementById('yesBtn');
    const card = document.getElementById('card');
    const bearArt = document.getElementById('bearArt');
    const successText = document.getElementById('successText');

    // Keep "No" inside the cta area
    function clamp(v, min, max){ return Math.max(min, Math.min(max, v)); }

    // Initialize positions
    const state = {
      noX: 170,
      noY: 18,
      radius: 140,     // repulsion distance
      strength: 18     // how fast it runs away
    };

    // Apply initial position
    function applyNoPos(){
      noBtn.style.left = state.noX + 'px';
      noBtn.style.top  = state.noY + 'px';
    }
    applyNoPos();

    // Repel away from cursor in real time
    function repel(e){
      const rect = ctaArea.getBoundingClientRect();

      const cursorX = e.clientX - rect.left;
      const cursorY = e.clientY - rect.top;

      const btnRect = noBtn.getBoundingClientRect();
      const btnX = (btnRect.left - rect.left) + btnRect.width/2;
      const btnY = (btnRect.top  - rect.top ) + btnRect.height/2;

      const dx = btnX - cursorX;
      const dy = btnY - cursorY;
      const dist = Math.hypot(dx, dy) || 0.0001;

      if (dist < state.radius){
        // direction away from cursor
        const ux = dx / dist;
        const uy = dy / dist;

        // speed scales with closeness
        const factor = (1 - dist / state.radius);
        const move = state.strength * (0.6 + factor * 1.6);

        state.noX += ux * move;
        state.noY += uy * move;

        // bounds within area
        const maxX = rect.width  - noBtn.offsetWidth;
        const maxY = rect.height - noBtn.offsetHeight;

        state.noX = clamp(state.noX, 0, maxX);
        state.noY = clamp(state.noY, 0, maxY);

        applyNoPos();
      }
    }

    // Track mouse + touch inside the button area
    ctaArea.addEventListener('mousemove', repel);
    ctaArea.addEventListener('touchmove', (e) => {
      if (!e.touches || !e.touches[0]) return;
      repel(e.touches[0]);
    }, {passive:true});

    // Also repel when hovering the No button directly
    noBtn.addEventListener('mouseenter', (e) => repel(e));
    noBtn.addEventListener('touchstart', (e) => {
      if (e.touches && e.touches[0]) repel(e.touches[0]);
    }, {passive:true});

    // Clicking "No" does nothing (it should be hard to click)
    noBtn.addEventListener('click', (e) => {
      e.preventDefault();
      e.stopPropagation();
      // small extra jump if they somehow click it
      const rect = ctaArea.getBoundingClientRect();
      state.noX = Math.random() * (rect.width - noBtn.offsetWidth);
      state.noY = Math.random() * (rect.height - noBtn.offsetHeight);
      applyNoPos();
    });

    // On "Yes": swap bear art to YAY version
    yesBtn.addEventListener('click', () => {
      successText.classList.add('show');

      // Disable runaway after success
      ctaArea.removeEventListener('mousemove', repel);

      // Replace SVG with "YAY" bear holding heart + shouting
      bearArt.innerHTML = `
        <svg viewBox="0 0 420 420" fill="none" xmlns="http://www.w3.org/2000/svg">
          <!-- confetti dots -->
          <circle cx="60" cy="70" r="6" fill="#ff4d6d"/>
          <circle cx="92" cy="48" r="5" fill="#ffd6e0"/>
          <circle cx="345" cy="70" r="6" fill="#ff4d6d"/>
          <circle cx="320" cy="45" r="5" fill="#ffd6e0"/>

          <!-- ears -->
          <circle cx="130" cy="120" r="45" fill="#B67C52"/>
          <circle cx="290" cy="120" r="45" fill="#B67C52"/>
          <circle cx="130" cy="120" r="25" fill="#E7C6A7"/>
          <circle cx="290" cy="120" r="25" fill="#E7C6A7"/>

          <!-- head -->
          <circle cx="210" cy="185" r="120" fill="#C58A5A"/>
          <ellipse cx="210" cy="235" rx="82" ry="62" fill="#E7C6A7"/>

          <!-- excited eyes -->
          <path d="M155 178c10-18 25-18 35 0" stroke="#2B2B2B" stroke-width="8" stroke-linecap="round"/>
          <path d="M230 178c10-18 25-18 35 0" stroke="#2B2B2B" stroke-width="8" stroke-linecap="round"/>

          <!-- nose -->
          <path d="M200 220c0-10 8-18 18-18s18 8 18 18c0 10-8 16-18 16s-18-6-18-16Z" fill="#2B2B2B"/>

          <!-- big happy mouth -->
          <path d="M170 250c18 28 62 28 80 0" stroke="#2B2B2B" stroke-width="10" stroke-linecap="round"/>
          <path d="M190 258c10 10 40 10 50 0" stroke="#ff4d6d" stroke-width="6" stroke-linecap="round" opacity=".7"/>

          <!-- blush -->
          <circle cx="150" cy="225" r="13" fill="#ff7aa2" opacity=".55"/>
          <circle cx="270" cy="225" r="13" fill="#ff7aa2" opacity=".55"/>

          <!-- body -->
          <ellipse cx="210" cy="322" rx="120" ry="90" fill="#C58A5A"/>
          <ellipse cx="210" cy="340" rx="78" ry="58" fill="#E7C6A7"/>

          <!-- arms raised -->
          <ellipse cx="105" cy="300" rx="58" ry="40" fill="#C58A5A" transform="rotate(-35 105 300)"/>
          <ellipse cx="315" cy="300" rx="58" ry="40" fill="#C58A5A" transform="rotate(35 315 300)"/>

          <!-- heart -->
          <g transform="translate(210 300)">
            <path d="M0 35s-55-35-55-78c0-20 16-36 36-36 14 0 26 8 32 20 6-12 18-20 32-20 20 0 36 16 36 36C81 0 0 35 0 35Z"
              fill="#FF4D6D" stroke="#D00042" stroke-width="6" stroke-linejoin="round"/>
          </g>

          <!-- YAY bubble -->
          <g>
            <path d="M280 70c0-28 30-48 64-42 24 4 40 20 40 40 0 22-18 40-44 44-18 3-38 0-50-10l-20 12 8-22c-8-6- - - - - -"
              fill="transparent"/>
          </g>
          <path d="M260 58c6-22 30-36 58-32 24 4 40 18 40 36 0 20-18 36-42 40-16 3-34 1-46-8l-20 12 8-22c-6-6-8-14- - -"
                fill="#ffffff" opacity=".92" stroke="#ffb3c1" stroke-width="4" stroke-linejoin="round"/>

          <text x="286" y="78" font-size="34" font-weight="900" fill="#d00042" style="font-family: ui-sans-serif, system-ui;">YAY!</text>
        </svg>
      `;

      // Optional: hide the No button after success
      noBtn.style.display = 'none';
      yesBtn.textContent = 'Sent 💌';
      yesBtn.disabled = true;
      yesBtn.style.filter = 'grayscale(0.2)';
      yesBtn.style.cursor = 'default';
    });

    // Keep No button in bounds on resize
    window.addEventListener('resize', () => {
      const rect = ctaArea.getBoundingClientRect();
      state.noX = clamp(state.noX, 0, rect.width - noBtn.offsetWidth);
      state.noY = clamp(state.noY, 0, rect.height - noBtn.offsetHeight);
      applyNoPos();
    });
  </script>
</body>
</html>
