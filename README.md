# Braz.github.io
<html><head><base href="https://brazhome.example.com/">
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Braz Home Improvement - Management System</title>

<style>
:root {
  --primary: #34495e;
  --secondary: #e74c3c;
  --accent: #3498db;
  --light: #f5f6fa;
  --dark: #2c3e50;
  --success: #2ecc71;
}

* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
  font-family: 'Poppins', sans-serif;
}

body {
  background: var(--light);
  min-height: 100vh;
}

.navbar {
  background: var(--primary);
  padding: 1rem 2rem;
  color: white;
  display: flex;
  justify-content: space-between;
  align-items: center;
  box-shadow: 0 2px 10px rgba(0,0,0,0.1);
}

.logo {
  display: flex;
  align-items: center;
  gap: 1rem;
}

.logo svg {
  width: 40px;
  height: 40px;
  fill: var(--secondary);
}

.logo-text {
  font-size: 1.5rem;
  font-weight: 600;
  color: white;
}

.container {
  max-width: 1400px;
  margin: 0 auto;
  padding: 2rem;
}

.dashboard {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  gap: 2rem;
  margin-top: 2rem;
}

.card {
  background: white;
  border-radius: 12px;
  padding: 1.5rem;
  box-shadow: 0 4px 6px rgba(0,0,0,0.1);
  transition: transform 0.3s ease;
}

.card:hover {
  transform: translateY(-5px);
}

.card-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 1.5rem;
  padding-bottom: 1rem;
  border-bottom: 2px solid var(--light);
}

.card-title {
  font-size: 1.2rem;
  font-weight: 600;
  color: var(--dark);
}

.tab-container {
  display: flex;
  gap: 1rem;
  flex-wrap: wrap;
  margin-bottom: 2rem;
}

.tab {
  padding: 0.8rem 1.5rem;
  background: var(--primary);
  color: white;
  border: none;
  border-radius: 8px;
  cursor: pointer;
  transition: all 0.3s ease;
  font-weight: 500;
}

.tab:hover {
  background: var(--secondary);
  transform: translateY(-2px);
}

.tab.active {
  background: var(--secondary);
  box-shadow: 0 4px 12px rgba(231, 76, 60, 0.2);
}

.form-group {
  margin-bottom: 1.5rem;
}

label {
  display: block;
  margin-bottom: 0.5rem;
  color: var(--dark);
  font-weight: 500;
}

input, textarea, select {
  width: 100%;
  padding: 0.8rem;
  border: 2px solid #e9ecef;
  border-radius: 8px;
  transition: border-color 0.3s ease;
  font-size: 1rem;
}

input:focus, textarea:focus, select:focus {
  border-color: var(--accent);
  outline: none;
}

button {
  background: var(--secondary);
  color: white;
  padding: 0.8rem 1.5rem;
  border: none;
  border-radius: 8px;
  cursor: pointer;
  transition: all 0.3s ease;
  font-weight: 500;
}

button:hover {
  background: #c0392b;
  transform: translateY(-2px);
}

.materials-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));
  gap: 1rem;
  margin-top: 1rem;
}

.material-card {
  background: white;
  padding: 1rem;
  border-radius: 8px;
  border: 1px solid #e9ecef;
}

.stock-low {
  color: var(--secondary);
}

.stock-good {
  color: var(--success);
}

.list-container {
  max-height: 400px;
  overflow-y: auto;
  padding-right: 1rem;
}

.list-item {
  padding: 1rem;
  border-bottom: 1px solid #e9ecef;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.list-item:hover {
  background: #f8f9fa;
}

.badge {
  padding: 0.3rem 0.8rem;
  border-radius: 20px;
  font-size: 0.8rem;
  font-weight: 500;
}

.badge-pending {
  background: #fff3cd;
  color: #856404;
}

.badge-complete {
  background: #d4edda;
  color: #155724;
}

@keyframes slideIn {
  from {
    opacity: 0;
    transform: translateY(20px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

.slide-in {
  animation: slideIn 0.4s ease;
}
</style>

<link href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;500;600;700&display=swap" rel="stylesheet">
<script src="https://cdn.jsdelivr.net/npm/sweetalert2@11"></script>
</head>
<body>

<nav class="navbar">
  <div class="logo">
    <svg viewBox="0 0 24 24">
      <path d="M3,13H5V11H3V13M3,17H5V15H3V17M3,9H5V7H3V9M7,13H21V11H7V13M7,17H21V15H7V17M7,7V9H21V7H7Z"/>
    </svg>
    <span class="logo-text">Braz Home Improvement</span>
  </div>
</nav>

<div class="container">
  <div class="tab-container">
    <button class="tab active" onclick="showSection('quote')">Quotes</button>
    <button class="tab" onclick="showSection('billing')">Billing</button>
    <button class="tab" onclick="showSection('contacts')">Contacts</button>
    <button class="tab" onclick="showSection('materials')">Materials</button>
  </div>

  <div id="quote-section" class="section slide-in">
    <div class="card">
      <div class="card-header">
        <h2 class="card-title">New Quote Request</h2>
      </div>
      <form id="quote-form">
        <div class="form-group">
          <label>Client Name</label>
          <input type="text" id="client-name" required>
        </div>
        <div class="form-group">
          <label>Service Type</label>
          <select id="service-type" required>
            <option value="">Select service...</option>
            <option value="kitchen">Kitchen Remodeling</option>
            <option value="bathroom">Bathroom Renovation</option>
            <option value="painting">Interior/Exterior Painting</option>
            <option value="flooring">Flooring Installation</option>
            <option value="other">Other Services</option>
          </select>
        </div>
        <div class="form-group">
          <label>Project Details</label>
          <textarea id="project-details" rows="4" required></textarea>
        </div>
        <div class="form-group">
          <label>Estimated Budget</label>
          <input type="number" id="budget" min="0" step="100" required>
        </div>
        <button type="submit">Generate Quote</button>
      </form>
    </div>
  </div>

  <div id="billing-section" class="section slide-in" style="display: none;">
    <div class="card">
      <div class="card-header">
        <h2 class="card-title">Billing Management</h2>
      </div>
      <form id="billing-form">
        <div class="form-group">
          <label>Invoice Number</label>
          <input type="text" id="invoice-number" required>
        </div>
        <div class="form-group">
          <label>Client Name</label>
          <input type="text" id="invoice-client" required>
        </div>
        <div class="form-group">
          <label>Services</label>
          <textarea id="invoice-services" rows="3" required></textarea>
        </div>
        <div class="form-group">
          <label>Amount ($)</label>
          <input type="number" id="invoice-amount" step="0.01" required>
        </div>
        <button type="submit">Create Invoice</button>
      </form>
    </div>
  </div>

  <div id="contacts-section" class="section slide-in" style="display: none;">
    <div class="card">
      <div class="card-header">
        <h2 class="card-title">Contact Directory</h2>
      </div>
      <form id="contact-form">
        <div class="form-group">
          <label>Name</label>
          <input type="text" id="contact-name" required>
        </div>
        <div class="form-group">
          <label>Email</label>
          <input type="email" id="contact-email" required>
        </div>
        <div class="form-group">
          <label>Phone</label>
          <input type="tel" id="contact-phone" required>
        </div>
        <div class="form-group">
          <label>Type</label>
          <select id="contact-type" required>
            <option value="client">Client</option>
            <option value="supplier">Supplier</option>
            <option value="contractor">Contractor</option>
          </select>
        </div>
        <button type="submit">Add Contact</button>
      </form>
    </div>
  </div>

  <div id="materials-section" class="section slide-in" style="display: none;">
    <div class="card">
      <div class="card-header">
        <h2 class="card-title">Materials Inventory</h2>
      </div>
      <form id="materials-form">
        <div class="form-group">
          <label>Material Name</label>
          <input type="text" id="material-name" required>
        </div>
        <div class="form-group">
          <label>Category</label>
          <select id="material-category" required>
            <option value="lumber">Lumber</option>
            <option value="paint">Paint</option>
            <option value="tiles">Tiles</option>
            <option value="fixtures">Fixtures</option>
            <option value="tools">Tools</option>
          </select>
        </div>
        <div class="form-group">
          <label>Quantity</label>
          <input type="number" id="material-quantity" required>
        </div>
        <div class="form-group">
          <label>Unit Price ($)</label>
          <input type="number" id="material-price" step="0.01" required>
        </div>
        <button type="submit">Add Material</button>
      </form>
    </div>
  </div>
</div>

<script>
// Initialize local storage
const storage = {
  quotes: JSON.parse(localStorage.getItem('quotes')) || [],
  invoices: JSON.parse(localStorage.getItem('invoices')) || [],
  contacts: JSON.parse(localStorage.getItem('contacts')) || [],
  materials: JSON.parse(localStorage.getItem('materials')) || []
};

function showSection(sectionName) {
  document.querySelectorAll('.section').forEach(section => {
    section.style.display = 'none';
  });
  document.querySelectorAll('.tab').forEach(tab => {
    tab.classList.remove('active');
  });
  document.getElementById(`${sectionName}-section`).style.display = 'block';
  event.target.classList.add('active');
}

// Quote Form Handler
document.getElementById('quote-form').addEventListener('submit', (e) => {
  e.preventDefault();
  const newQuote = {
    id: Date.now(),
    client: document.getElementById('client-name').value,
    service: document.getElementById('service-type').value,
    details: document.getElementById('project-details').value,
    budget: document.getElementById('budget').value,
    status: 'pending'
  };
  storage.quotes.push(newQuote);
  localStorage.setItem('quotes', JSON.stringify(storage.quotes));
  Swal.fire({
    title: 'Quote Created!',
    text: 'The quote has been generated successfully.',
    icon: 'success',
    confirmButtonColor: '#e74c3c'
  });
  e.target.reset();
});

// Billing Form Handler
document.getElementById('billing-form').addEventListener('submit', (e) => {
  e.preventDefault();
  const newInvoice = {
    id: document.getElementById('invoice-number').value,
    client: document.getElementById('invoice-client').value,
    services: document.getElementById('invoice-services').value,
    amount: document.getElementById('invoice-amount').value,
    date: new Date().toISOString(),
    status: 'unpaid'
  };
  storage.invoices.push(newInvoice);
  localStorage.setItem('invoices', JSON.stringify(storage.invoices));
  Swal.fire({
    title: 'Invoice Created!',
    text: 'The invoice has been generated successfully.',
    icon: 'success',
    confirmButtonColor: '#e74c3c'
  });
  e.target.reset();
});

// Contact Form Handler
document.getElementById('contact-form').addEventListener('submit', (e) => {
  e.preventDefault();
  const newContact = {
    id: Date.now(),
    name: document.getElementById('contact-name').value,
    email: document.getElementById('contact-email').value,
    phone: document.getElementById('contact-phone').value,
    type: document.getElementById('contact-type').value
  };
  storage.contacts.push(newContact);
  localStorage.setItem('contacts', JSON.stringify(storage.contacts));
  Swal.fire({
    title: 'Contact Added!',
    text: 'The contact has been added successfully.',
    icon: 'success',
    confirmButtonColor: '#e74c3c'
  });
  e.target.reset();
});

// Materials Form Handler
document.getElementById('materials-form').addEventListener('submit', (e) => {
  e.preventDefault();
  const newMaterial = {
    id: Date.now(),
    name: document.getElementById('material-name').value,
    category: document.getElementById('material-category').value,
    quantity: document.getElementById('material-quantity').value,
    price: document.getElementById('material-price').value
  };
  storage.materials.push(newMaterial);
  localStorage.setItem('materials', JSON.stringify(storage.materials));
  Swal.fire({
    title: 'Material Added!',
    text: 'The material has been added to inventory.',
    icon: 'success',
    confirmButtonColor: '#e74c3c'
  });
  e.target.reset();
});

function deleteItem(type, id) {
  storage[type] = storage[type].filter(item => item.id !== id);
  localStorage.setItem(type, JSON.stringify(storage[type]));
  updateDisplay(type);
}

function updateDisplay(type) {
  // Implementation for updating the display of different sections
  const items = storage[type];
  const container = document.getElementById(`${type}-list`);
  if (!container) return;

  container.innerHTML = items.map(item => `
    <div class="list-item">
      <div>
        <strong>${item.name || item.client}</strong>
        ${type === 'materials' ? `<span class="${item.quantity < 10 ? 'stock-low' : 'stock-good'}">
          Stock: ${item.quantity}
        </span>` : ''}
      </div>
      <button onclick="deleteItem('${type}', ${item.id})">Delete</button>
    </div>
  `).join('');
}

// Initialize displays
['quotes', 'invoices', 'contacts', 'materials'].forEach(updateDisplay);
</script>

</body>
</html>
