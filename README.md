# systemplay
"Magazin Sisteme de Operare" este un site simplu și eficient dedicat vânzării și distribuirii sistemelor de operare către utilizatori. Platforma este gândită pentru a oferi o experiență intuitivă atât pentru cumpărători, cât și pentru administrator.

<!DOCTYPE html>
<html lang="ro">
<head>
  <meta charset="UTF-8" />
  <title>Magazin Sisteme de Operare</title>
  <style>
    body { font-family: Arial, sans-serif; margin: 20px; }
    h1 { text-align: center; }
    .os-card { border: 1px solid #ccc; padding: 10px; margin: 10px; border-radius: 10px; }
    .admin-panel { display: none; margin-top: 30px; border-top: 1px solid #888; padding-top: 20px; }
    input, button { padding: 5px; margin: 5px; }
    .os-list { display: flex; flex-wrap: wrap; gap: 10px; }
  </style>
</head>
<body>

<h1>Magazin Sisteme de Operare</h1>

<div class="os-list" id="osList">
  <!-- Aici se vor adăuga sistemele de operare -->
</div>

<hr>

<button onclick="toggleAdmin()">🔐 Admin Login</button>
<div class="admin-panel" id="adminPanel">
  <h2>Panou Administrator</h2>
  <input type="text" id="osName" placeholder="Nume sistem" />
  <input type="text" id="osPrice" placeholder="Preț (lei)" />
  <input type="text" id="osLink" placeholder="Link descărcare" />
  <button onclick="addOS()">Adaugă sistem</button>
</div>

<script>
  const osList = document.getElementById('osList');
  const adminPanel = document.getElementById('adminPanel');

  function toggleAdmin() {
    adminPanel.style.display = adminPanel.style.display === 'none' ? 'block' : 'none';
  }

  function loadOS() {
    const systems = JSON.parse(localStorage.getItem('osData') || '[]');
    osList.innerHTML = '';
    systems.forEach((os, index) => {
      const card = document.createElement('div');
      card.className = 'os-card';
      card.innerHTML = `
        <h3>${os.name}</h3>
        <p>Preț: ${os.price} lei</p>
        <a href="${os.link}" target="_blank"><button>Descarcă</button></a>
      `;
      osList.appendChild(card);
    });
  }

  function addOS() {
    const name = document.getElementById('osName').value;
    const price = document.getElementById('osPrice').value;
    const link = document.getElementById('osLink').value;

    if (!name || !price || !link) return alert("Completează toate câmpurile!");

    const systems = JSON.parse(localStorage.getItem('osData') || '[]');
    systems.push({ name, price, link });
    localStorage.setItem('osData', JSON.stringify(systems));
    loadOS();
  }

  loadOS();
</script>

</body>
</html>

