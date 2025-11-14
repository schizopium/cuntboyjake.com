<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>@cuntboyjake • FTM Edge Empire</title>

  <!-- Stripe + Firebase -->
  <script src="https://js.stripe.com/v3/"></script>
  <script src="https://www.gstatic.com/firebasejs/9.22.0/firebase-app-compat.js"></script>
  <script src="https://www.gstatic.com/firebasejs/9.22.0/firebase-database-compat.js"></script>
  <script src="https.//www.gstatic.com/firebasejs/9.22.0/firebase-auth-compat.js"></script>

  <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@600;800&display=swap" rel="stylesheet">
  <style>
    :root { --pink:#ff4d94; --purple:#9d4edd; --dark:#1a0d2b; --light:#f8e1ff; --accent:#ff3399; }
    * { margin:0; padding:0; box-sizing:border-box; font-family:'Poppins',sans-serif; }
    body { background:linear-gradient(135deg,var(--dark),#2a1b3d); color:var(--light); min-height:100vh; padding:20px; }
    .container { max-width:1100px; margin:auto; display:grid; gap:20px; grid-template-columns:1fr 1fr; }
    @media(max-width:768px){ .container{grid-template-columns:1fr;} }

    .card { background:rgba(255,255,255,0.05); border:2px solid var(--accent); border-radius:16px; padding:20px; backdrop-filter:blur(8px); }
    h1, h2, h3 { color:var(--accent); text-align:center; text-shadow:0 0 10px rgba(255,77,148,0.6); }
    .btn { background:var(--purple); color:white; padding:12px; margin:8px 0; border-radius:10px; font-weight:bold; cursor:pointer; transition:0.3s; text-align:center; }
    .btn:hover { background:#b15bff; transform:translateY(-2px); }
    .goal-bar { height:12px; background:rgba(255,255,255,0.2); border-radius:6px; overflow:hidden; margin:10px 0; }
    .fill { height:100%; background:var(--accent); width:0%; transition:width 1s ease; }

    #age-gate, #admin-panel, #teaser-modal, #fanclub-modal { position:fixed; top:0; left:0; width:100%; height:100%; background:rgba(0,0,0,0.95); display:flex; flex-direction:column; align-items:center; justify-content:center; z-index:9999; padding:20px; text-align:center; }
    #age-gate button, #admin-panel button, #teaser-modal button, #fanclub-modal button { background:var(--accent); color:white; border:none; padding:12px 24px; border-radius:8px; font-weight:800; cursor:pointer; margin:10px; }

    .links { display:grid; grid-template-columns:repeat(auto-fit,minmax(140px,1fr)); gap:10px; }
    .link-btn { background:var(--purple); padding:10px; border-radius:8px; text-align:center; font-size:0.9rem; }

    .premade { display:flex; gap:10px; align-items:center; background:rgba(0,0,0,0.3); padding:10px; border-radius:10px; margin:10px 0; }
    .premade img { width:80px; height:80px; object-fit:cover; border-radius:8px; border:2px solid var(--accent); }
    .premade-info { flex:1; }

    #tip-log { max-height:200px; overflow-y:auto; font-size:0.85rem; }
    .tip { padding:5px 0; border-bottom:1px dashed rgba(255,255,255,0.2); }

    .form-group { margin:15px 0; }
    input, textarea { width:100%; padding:12px; border-radius:8px; border:none; margin-top:5px; }

    .copyright { font-size:0.7rem; text-align:center; color:#ff99cc; margin-top:20px; }

    .fanclub-badge { background:#ff3399; color:white; padding:5px 10px; border-radius:20px; font-size:0.8rem; }
  </style>
</head>
<body>

<!-- AGE GATE -->
<div id="age-gate">
  <h1>🔞 @cuntboyjake • 18+ Only</h1>
  <p>FTM Twink • Edging • Breeding • C2C • Customs • Fanclub</p>
  <input type="date" id="dob" required />
  <button onclick="verifyAge()">Enter Empire</button>
</div>

<div id="main" style="display:none;">

  <div class="container">

    <!-- LEFT: MENU + LINKS + PREMADES + FANCLUB -->
    <div class="card">
      <h1>@cuntboyjake</h1>
      <p style="text-align:center;">FTM Twink • Edging God • Breed Me (Optional)</p>

      <h3>🔗 Live Now</h3>
      <div class="links">
        <a href="https://chaturbate.com/ftmjakeoff" class="link-btn" target="_blank">Chaturbate</a>
        <a href="https://stripchat.com/ftmjakeoff" class="link-btn" target="_blank">Stripchat</a>
        <a href="https://cam4.com/jake0ff" class="link-btn" target="_blank">CAM4</a>
        <a href="https://fansly.com/ftmjakeoff" class="link-btn" target="_blank">Fansly</a>
        <a href="https://onlyfans.com/ftmjakeoff" class="link-btn" target="_blank">OnlyFans</a>
        <a href="https://x.com/ftmjakeoff" class="link-btn" target="_blank">X</a>
      </div>

      <h3>🎯 Live Goal: Breed Load</h3>
      <div class="goal-bar"><div class="fill" id="goal-fill"></div></div>
      <p style="text-align:center; font-size:0.9rem;" id="goal-text">$0 / $500</p>

      <h3>📜 Tip Menu</h3>
      <div class="btn" data-id="flash" data-price="5">Flash Boypussy • $5</div>
      <div class="btn" data-id="edge" data-price="15">Edge Tease • $15</div>
      <div class="btn" data-id="toy" data-price="25">Toy Boycunt • $25</div>
      <div class="btn" data-id="cum" data-price="50">Cum / Breed Load • $50</div>

      <h3>💎 Fanclub ($9.99/mo)</h3>
      <p style="font-size:0.9rem; text-align:center;">
        <strong>Exclusive:</strong> Kink vids, hot pics, breeding extras<br>
        <span class="fanclub-badge">Discounted tips!</span>
      </p>
      <button class="btn" onclick="joinFanclub()">Join Fanclub</button>

      <h3>🎥 Premium Premades</h3>
      <div class="premade" data-id="pre1" data-price="15">
        <img src="previews/edge-solo.jpg" alt="preview">
        <div class="premade-info"><strong>Edge Solo</strong><div>5min • $15</div></div>
        <button class="btn" style="padding:8px; font-size:0.8rem;">Buy Now</button>
      </div>
      <div class="premade" data-id="pre2" data-price="25">
        <img src="previews/breed-tease.jpg" alt="preview">
        <div class="premade-info"><strong>Breeding Fantasy</strong><div>8min • $25</div></div>
        <button class="btn" style="padding:8px; font-size:0.8rem;">Buy Now</button>
      </div>
    </div>

    <!-- RIGHT: CART + CUSTOM + NOTIFY -->
    <div class="card">
      <h2>🛒 Edge Cart</h2>
      <div id="cart-items"></div>
      <div style="font-weight:bold; text-align:right; color:var(--accent);" id="cart-total">$0</div>

      <div id="payment-element" style="margin:15px 0;"></div>
      <button class="btn" id="checkout-btn">Pay with Card</button>

      <h3>🎥 Custom Request</h3>
      <div class="form-group">
        <input type="text" id="custom-name" placeholder="Your Name" />
      </div>
      <div class="form-group">
        <textarea id="custom-request" placeholder="C2C, breeding, edging, etc."></textarea>
      </div>
      <div class="form-group">
        <input type="number" id="custom-price" placeholder="Offer (USD)" min="20" />
      </div>
      <button class="btn" onclick="submitCustom()">Send Request</button>

      <h3>📧 Stay Updated</h3>
      <div class="form-group">
        <input type="email" id="notify-email" placeholder="Email for live alerts" />
        <button class="btn" onclick="subscribe()">Subscribe</button>
      </div>

      <h3>📜 Recent Tips</h3>
      <div id="tip-log"></div>
    </div>

  </div>

  <p class="copyright">
    © 2025 @cuntboyjake. All content is protected. Unauthorized distribution, resale, or republication is prohibited and will be prosecuted.
  </p>
</div>

<!-- FANCLUB MODAL -->
<div id="fanclub-modal" style="display:none;">
  <h2>💎 Join Fanclub</h2>
  <p>$9.99/month • Exclusive kink vids, pics, discounts</p>
  <div id="fanclub-element"></div>
  <button class="btn" id="fanclub-btn">Subscribe</button>
  <button onclick="closeFanclub()">Cancel</button>
</div>

<!-- TEASER MODAL -->
<div id="teaser-modal" style="display:none;">
  <h2>Teaser Clip</h2>
  <video controls style="width:90%; max-width:400px; border-radius:12px;">
    <source src="" type="video/mp4">
  </video>
  <button onclick="closeTeaser()">Close</button>
</div>

<!-- ADMIN PANEL -->
<div id="admin-panel" style="display:none;">
  <h2>Admin: cuntboyjake</h2>
  <button class="btn" onclick="resetGoal()">Reset Goal</button>
  <button class="btn" onclick="viewDMCALogs()">View DMCA Logs</button>
  <button class="btn" onclick="closeAdmin()">Close</button>
</div>

<!-- MOANS -->
<audio id="moan1" src="https://assets.mixkit.co/sfx/preview/mixkit-female-moan-686.mp3"></audio>

<script>
  // STRIPE
  const stripe = Stripe('pk_test_XXXXXXXXXXXXXXXXXXXXXXXX'); // REPLACE
  const elements = stripe.elements();
  const paymentElement = elements.create('payment');
  paymentElement.mount('#payment-element');

  // FANCLUB
  const fanclubElement = elements.create('payment');
  fanclubElement.mount('#fanclub-element');

  // FIREBASE
  const firebaseConfig = { databaseURL: "https://cuntboy-stream-default-rtdb.firebaseio.com" };
  firebase.initializeApp(firebaseConfig);
  const db = firebase.database();
  const goalRef = db.ref('goals/cum');
  const tipsRef = db.ref('tips');
  const customsRef = db.ref('customs');
  const subsRef = db.ref('subscribers');
  const fill = document.getElementById('goal-fill');
  const goalText = document.getElementById('goal-text');
  const tipLog = document.getElementById('tip-log');

  // AGE GATE
  function verifyAge() {
    const dob = new Date(document.getElementById('dob').value);
    const age = new Date().getFullYear() - dob.getFullYear();
    if (age < 18) return alert('18+ only.');
    localStorage.setItem('ageVerified', 'true');
    document.getElementById('age-gate').style.display = 'none';
    document.getElementById('main').style.display = 'block';
  }
  if (localStorage.getItem('ageVerified')) {
    document.getElementById('age-gate').style.display = 'none';
    document.getElementById('main').style.display = 'block';
  }

  // ADMIN
  let clicks = 0;
  document.body.addEventListener('dblclick', () => {
    clicks++; if (clicks >= 3) { document.getElementById('admin-panel').style.display = 'block'; clicks = 0; }
  });

  // CART
  let cart = {};
  function addToCart(id, name, price, user) {
    cart[id] = cart[id] || {name, price, qty:0}; cart[id].qty++;
    renderCart(); playMoan();
    tipsRef.push({user, amount:price, time:Date.now()});
    goalRef.transaction(v => (v||0) + price*100);
  }
  function renderCart() {
    const items = document.getElementById('cart-items');
    const total = document.getElementById('cart-total');
    items.innerHTML = ''; let sum = 0;
    for (let id in cart) {
      const i = cart[id]; sum += i.price * i.qty;
      items.innerHTML += `<div>${i.name} ×${i.qty} = $${(i.price*i.qty).toFixed(2)}</div>`;
    }
    total.textContent = `$${sum.toFixed(2)}`;
  }

  // CHECKOUT
  document.getElementById('checkout-btn').onclick = async () => {
    const email = prompt('Email:');
    const { client_secret } = await fetch('https://us-central1-cuntboy-stream.cloudfunctions.net/createPayment', {
      method: 'POST',
      body: JSON.stringify({ amount: Object.values(cart).reduce((s,i)=>s+i.price*i.qty,0)*100, email }),
      headers: { 'Content-Type': 'application/json' }
    }).then(r => r.json());
    const { error } = await stripe.confirmCardPayment(client_secret);
    if (error) return alert(error.message);
    alert('Paid! Check email.');
    cart = {}; renderCart();
  };

  // FANCLUB
  function joinFanclub() {
    document.getElementById('fanclub-modal').style.display = 'flex';
  }
  function closeFanclub() {
    document.getElementById('fanclub-modal').style.display = 'none';
  }
  document.getElementById('fanclub-btn').onclick = async () => {
    const email = prompt('Email for fanclub:');
    const { client_secret } = await fetch('https://us-central1-cuntboy-stream.cloudfunctions.net/createSubscription', {
      method: 'POST',
      body: JSON.stringify({ email }),
      headers: { 'Content-Type': 'application/json' }
    }).then(r => r.json());
    const { error } = await stripe.confirmCardPayment(client_secret);
    if (error) return alert(error.message);
    alert('Welcome to the Fanclub! Exclusive content unlocked.');
    closeFanclub();
  };

  // CUSTOM + PREMADES + SUBSCRIBE + GOAL + LOG
  document.querySelectorAll('[data-id]').forEach(b => b.addEventListener('click', () => {
    const id = b.dataset.id; const price = parseFloat(b.dataset.price);
    const name = prompt('Your name:') || 'Anon';
    addToCart(id, b.innerText.split(' • ')[0], price, name);
  }));

  document.querySelectorAll('.premade').forEach(p => {
    p.querySelector('button').addEventListener('click', async () => {
      const id = p.dataset.id; const price = parseFloat(p.dataset.price);
      const email = prompt('Email:');
      const { client_secret } = await fetch('https://us-central1-cuntboy-stream.cloudfunctions.net/createPayment', {
        method: 'POST',
        body: JSON.stringify({ amount: price*100, email, metadata: { type: 'premade', id } }),
        headers: { 'Content-Type': 'application/json' }
      }).then(r => r.json());
      const { error } = await stripe.confirmCardPayment(client_secret);
      if (error) return alert(error.message);
      alert('Paid! Delivery in 60s.');
    });
  });

  function submitCustom() {
    const name = document.getElementById('custom-name').value;
    const req = document.getElementById('custom-request').value;
    const price = document.getElementById('custom-price').value;
    if (!name || !req || !price) return alert('Fill all fields.');
    customsRef.push({ name, req, price, time: Date.now() });
    alert('Request sent! I’ll DM you on Snapchat.');
  }

  function subscribe() {
    const email = document.getElementById('notify-email').value;
    if (!email) return alert('Enter email.');
    subsRef.push({email, time:Date.now()});
    alert('Subscribed!');
  }

  goalRef.on('value', s => {
    const raised = s.val() || 0;
    const percent = Math.min(100, (raised/5000)*100);
    fill.style.width = percent + '%';
    goalText.textContent = `$${raised} / $5000`;
  });
  tipsRef.limitToLast(5).on('child_added', s => {
    const t = s.val();
    tipLog.innerHTML = `<div class="tip"><strong>${t.user}</strong> tipped $${t.amount}</div>` + tipLog.innerHTML;
  });

  function playMoan() { document.getElementById('moan1').play(); }
  function resetGoal() { goalRef.set(0); }
  function closeAdmin() { document.getElementById('admin-panel').style.display = 'none'; }
  function viewDMCALogs() {
    db.ref('dmca/logs').once('value').then(s => {
      const logs = s.val();
      let html = '<h3>DMCA Takedowns</h3>';
      for (let id in logs) {
        html += `<div>${new Date(logs[id].time).toLocaleString()} → ${logs[id].results.length} sites</div>`;
      }
      alert(html || 'No takedowns yet.');
    });
  }
</script>

</body>
</html>