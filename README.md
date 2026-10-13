# bus-reservation-system

<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>BusGo · bus reservation</title>
  <style>
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
      font-family: system-ui, 'Segoe UI', Roboto, 'Helvetica Neue', sans-serif;
    }

    body {
      background: linear-gradient(145deg, #eef2f7 0%, #d9e2ec 100%);
      min-height: 100vh;
      display: flex;
      justify-content: center;
      align-items: center;
      padding: 20px;
    }

    .app {
      max-width: 1100px;
      width: 100%;
      background: rgba(255,255,255,0.7);
      backdrop-filter: blur(12px);
      -webkit-backdrop-filter: blur(12px);
      border-radius: 40px;
      box-shadow: 0 25px 50px -12px rgba(0, 0, 0, 0.35), inset 0 1px 3px rgba(255,255,255,0.9);
      padding: 30px 35px;
      border: 1px solid rgba(255,255,255,0.6);
    }

    h1 {
      display: flex;
      align-items: center;
      gap: 12px;
      font-weight: 700;
      font-size: 2.2rem;
      color: #1e293b;
      letter-spacing: -0.5px;
      margin-bottom: 12px;
    }

    h1 span {
      background: #1e293b;
      color: #f8fafc;
      font-size: 1.2rem;
      font-weight: 500;
      padding: 8px 16px;
      border-radius: 40px;
      margin-left: auto;
    }

    .subhead {
      color: #334155;
      margin-bottom: 28px;
      font-weight: 400;
      border-left: 4px solid #3b82f6;
      padding-left: 18px;
      font-size: 1.1rem;
    }

    .search-panel {
      display: flex;
      flex-wrap: wrap;
      gap: 18px;
      margin-bottom: 35px;
      align-items: flex-end;
      background: #ffffffcc;
      padding: 22px 20px;
      border-radius: 32px;
      box-shadow: 0 8px 20px rgba(0,0,0,0.04);
      border: 1px solid #ffffff;
    }

    .input-group {
      flex: 1 1 180px;
      display: flex;
      flex-direction: column;
      gap: 8px;
    }

    .input-group label {
      font-size: 0.8rem;
      font-weight: 600;
      text-transform: uppercase;
      letter-spacing: 0.5px;
      color: #475569;
    }

    .input-group input, .input-group select {
      background: #ffffff;
      border: 1.5px solid #e2e8f0;
      border-radius: 18px;
      padding: 14px 18px;
      font-size: 0.95rem;
      transition: all 0.2s;
      outline: none;
      color: #0f172a;
      font-weight: 500;
    }

    .input-group input:focus, .input-group select:focus {
      border-color: #3b82f6;
      box-shadow: 0 0 0 4px #3b82f620;
    }

    .search-btn {
      background: #0f172a;
      color: white;
      border: none;
      border-radius: 40px;
      padding: 14px 32px;
      font-weight: 600;
      font-size: 1rem;
      display: flex;
      align-items: center;
      gap: 10px;
      cursor: pointer;
      transition: 0.2s;
      height: fit-content;
      box-shadow: 0 10px 20px -8px #0f172a60;
      border: 1px solid #334155;
    }

    .search-btn:hover {
      background: #1e293b;
      transform: scale(1.01);
      box-shadow: 0 12px 24px -8px #0f172a80;
    }

    .search-btn:active {
      transform: scale(0.98);
    }

    .bus-list {
      display: flex;
      flex-direction: column;
      gap: 22px;
      margin-bottom: 40px;
      max-height: 380px;
      overflow-y: auto;
      padding-right: 6px;
    }

    .bus-card {
      background: white;
      border-radius: 28px;
      padding: 22px 26px;
      display: flex;
      flex-wrap: wrap;
      align-items: center;
      justify-content: space-between;
      box-shadow: 0 10px 18px -10px rgba(0,0,0,0.15);
      border: 1.5px solid #ffffff;
      transition: 0.2s;
      cursor: pointer;
      backdrop-filter: blur(4px);
    }

    .bus-card:hover {
      border-color: #94a3b8;
      box-shadow: 0 20px 28px -12px #1e293b30;
      background: #fefefe;
    }

    .bus-card.selected {
      border: 2px solid #3b82f6;
      background: #eff6ff;
      box-shadow: 0 10px 22px -8px #3b82f680;
    }

    .bus-info h3 {
      font-size: 1.4rem;
      font-weight: 700;
      color: #0b1e33;
      display: flex;
      align-items: center;
      gap: 10px;
    }

    .bus-info .route {
      color: #475569;
      font-weight: 500;
      margin-top: 6px;
      display: flex;
      align-items: center;
      gap: 6px;
    }

    .bus-meta {
      display: flex;
      gap: 24px;
      margin-top: 12px;
      font-size: 0.9rem;
      color: #334155;
      flex-wrap: wrap;
    }

    .bus-meta span {
      background: #f1f5f9;
      padding: 5px 12px;
      border-radius: 30px;
      display: flex;
      align-items: center;
      gap: 6px;
      font-weight: 500;
    }

    .price-tag {
      font-weight: 700;
      font-size: 1.8rem;
      color: #0f172a;
      letter-spacing: -1px;
    }

    .price-tag small {
      font-size: 0.9rem;
      font-weight: 400;
      color: #64748b;
    }

    .seats-badge {
      background: #dbeafe;
      color: #1e40af;
      padding: 6px 16px;
      border-radius: 30px;
      font-weight: 600;
      font-size: 0.9rem;
    }

    .booking-area {
      display: grid;
      grid-template-columns: 1.4fr 1fr;
      gap: 30px;
      background: #ffffffb3;
      border-radius: 32px;
      padding: 28px 28px;
      border: 1px solid #ffffff;
      backdrop-filter: blur(4px);
    }

    .seat-section h3 {
      font-size: 1.2rem;
      font-weight: 600;
      color: #1e293b;
      margin-bottom: 16px;
      display: flex;
      align-items: center;
      gap: 10px;
    }

    .legend {
      display: flex;
      gap: 18px;
      font-size: 0.8rem;
      color: #334155;
      margin-bottom: 16px;
      flex-wrap: wrap;
    }

    .legend-item {
      display: flex;
      align-items: center;
      gap: 6px;
    }

    .legend-box {
      width: 18px;
      height: 18px;
      border-radius: 6px;
      background: #f1f5f9;
      border: 1.5px solid #cbd5e1;
    }

    .legend-box.selected {
      background: #3b82f6;
      border-color: #2563eb;
    }

    .legend-box.occupied {
      background: #cbd5e1;
      border-color: #94a3b8;
      background-image: linear-gradient(135deg, #94a3b8 25%, #cbd5e1 25%, #cbd5e1 50%, #94a3b8 50%, #94a3b8 75%, #cbd5e1 75%, #cbd5e1 100%);
      background-size: 10px 10px;
    }

    .seats-grid {
      display: grid;
      grid-template-columns: repeat(4, 1fr);
      gap: 10px;
      max-width: 400px;
    }

    .seat {
      aspect-ratio: 1 / 1;
      background: #f8fafc;
      border: 2px solid #e2e8f0;
      border-radius: 14px;
      display: flex;
      align-items: center;
      justify-content: center;
      font-weight: 600;
      color: #1e293b;
      font-size: 0.9rem;
      cursor: pointer;
      transition: 0.15s;
      user-select: none;
    }

    .seat.available:hover {
      background: #dbeafe;
      border-color: #3b82f6;
      transform: scale(1.02);
    }

    .seat.selected {
      background: #3b82f6;
      border-color: #2563eb;
      color: white;
      box-shadow: 0 6px 12px -6px #3b82f6;
    }

    .seat.occupied {
      background: #e2e8f0;
      border-color: #cbd5e1;
      color: #94a3b8;
      cursor: not-allowed;
      background-image: repeating-linear-gradient(45deg, #cbd5e1 0px, #cbd5e1 4px, #e2e8f0 4px, #e2e8f0 8px);
      pointer-events: none;
    }

    .summary-card {
      background: #f8fafc;
      border-radius: 24px;
      padding: 24px 22px;
      border: 1px solid #e2e8f0;
      display: flex;
      flex-direction: column;
      gap: 20px;
    }

    .summary-card h3 {
      font-size: 1.2rem;
      font-weight: 600;
      color: #0f172a;
      border-bottom: 1px dashed #cbd5e1;
      padding-bottom: 12px;
    }

    .summary-row {
      display: flex;
      justify-content: space-between;
      font-size: 0.95rem;
      color: #1e293b;
    }

    .summary-row.total {
      font-weight: 700;
      font-size: 1.3rem;
      color: #0f172a;
      border-top: 1px solid #cbd5e1;
      padding-top: 15px;
      margin-top: 5px;
    }

    .book-btn {
      background: #0f172a;
      color: white;
      border: none;
      border-radius: 40px;
      padding: 18px 20px;
      font-weight: 700;
      font-size: 1.1rem;
      width: 100%;
      cursor: pointer;
      transition: 0.2s;
      display: flex;
      align-items: center;
      justify-content: center;
      gap: 10px;
      margin-top: 12px;
    }

    .book-btn:hover:not(:disabled) {
      background: #1e293b;
      transform: scale(1.01);
    }

    .book-btn:disabled {
      background: #94a3b8;
      cursor: not-allowed;
      opacity: 0.7;
    }

    .message {
      padding: 12px 16px;
      border-radius: 40px;
      font-weight: 500;
      font-size: 0.9rem;
    }

    .message.success {
      background: #dcfce7;
      color: #166534;
      border: 1px solid #86efac;
    }

    .message.error {
      background: #fee2e2;
      color: #991b1b;
      border: 1px solid #fca5a5;
    }

    .empty-state {
      color: #64748b;
      text-align: center;
      padding: 30px;
      font-style: italic;
    }

    ::-webkit-scrollbar {
      width: 6px;
    }
    ::-webkit-scrollbar-track {
      background: #e2e8f0;
      border-radius: 10px;
    }
    ::-webkit-scrollbar-thumb {
      background: #94a3b8;
      border-radius: 10px;
    }

    @media (max-width: 800px) {
      .booking-area {
        grid-template-columns: 1fr;
      }
      .app {
        padding: 22px;
      }
      .seats-grid {
        max-width: 100%;
      }
    }
  </style>
</head>
<body>
<div class="app">
  <h1>
    🚌 BusGo
    <span>reservation</span>
  </h1>
  <div class="subhead">Choose your route, pick a seat, and ride.</div>

  <!-- search / filter -->
  <div class="search-panel">
    <div class="input-group">
      <label>From</label>
      <select id="fromSelect">
        <option value="New York">New York</option>
        <option value="Boston">Boston</option>
        <option value="Washington">Washington</option>
        <option value="Philadelphia">Philadelphia</option>
      </select>
    </div>
    <div class="input-group">
      <label>To</label>
      <select id="toSelect">
        <option value="Boston">Boston</option>
        <option value="New York">New York</option>
        <option value="Washington">Washington</option>
        <option value="Philadelphia">Philadelphia</option>
      </select>
    </div>
    <div class="input-group">
      <label>Date</label>
      <input type="date" id="datePicker" value="2025-06-15">
    </div>
    <button class="search-btn" id="searchBtn">
      🔍 Search buses
    </button>
  </div>

  <!-- bus list -->
  <div class="bus-list" id="busList"></div>

  <!-- booking area : seats + summary -->
  <div class="booking-area" id="bookingArea" style="display: none;">
    <div class="seat-section">
      <h3>🚌 Select seats <span id="selectedBusName" style="font-weight:400; font-size:0.9rem; color:#475569;"></span></h3>
      <div class="legend">
        <div class="legend-item"><div class="legend-box"></div> Available</div>
        <div class="legend-item"><div class="legend-box selected"></div> Selected</div>
        <div class="legend-item"><div class="legend-box occupied"></div> Occupied</div>
      </div>
      <div class="seats-grid" id="seatsGrid"></div>
    </div>

    <div class="summary-card">
      <h3>🧾 Booking summary</h3>
      <div class="summary-row">
        <span>Bus</span>
        <span id="summaryBus">—</span>
      </div>
      <div class="summary-row">
        <span>Route</span>
        <span id="summaryRoute">—</span>
      </div>
      <div class="summary-row">
        <span>Seats</span>
        <span id="summarySeats">—</span>
      </div>
      <div class="summary-row">
        <span>Price per seat</span>
        <span id="summaryPrice">—</span>
      </div>
      <div class="summary-row total">
        <span>Total</span>
        <span id="summaryTotal">$0</span>
      </div>
      <div id="messageBox"></div>
      <button class="book-btn" id="bookBtn" disabled>
        ✅ Confirm reservation
      </button>
    </div>
  </div>
</div>

<script>
  (function() {
    // ---------- DATA ----------
    const buses = [
      {
        id: 'bus-101',
        name: 'Silver Arrow',
        from: 'New York',
        to: 'Boston',
        departure: '08:30 AM',
        arrival: '12:45 PM',
        price: 45,
        totalSeats: 16,
        occupied: [2, 3, 7, 11, 15] // 1-indexed seat numbers (occupied)
      },
      {
        id: 'bus-102',
        name: 'Metro Liner',
        from: 'New York',
        to: 'Washington',
        departure: '09:15 AM',
        arrival: '02:30 PM',
        price: 55,
        totalSeats: 16,
        occupied: [1, 5, 6, 9, 14]
      },
      {
        id: 'bus-103',
        name: 'City Express',
        from: 'Boston',
        to: 'New York',
        departure: '11:00 AM',
        arrival: '03:20 PM',
        price: 42,
        totalSeats: 16,
        occupied: [4, 8, 12, 13, 16]
      },
      {
        id: 'bus-104',
        name: 'Capital Coach',
        from: 'Washington',
        to: 'Philadelphia',
        departure: '01:30 PM',
        arrival: '04:50 PM',
        price: 38,
        totalSeats: 16,
        occupied: [2, 7, 10]
      },
      {
        id: 'bus-105',
        name: 'Night Rider',
        from: 'Philadelphia',
        to: 'Boston',
        departure: '07:00 PM',
        arrival: '11:45 PM',
        price: 52,
        totalSeats: 16,
        occupied: [3, 5, 9, 12, 15, 16]
      }
    ];

    // ---------- STATE ----------
    let currentBuses = [...buses];            // filtered buses
    let selectedBus = null;                  // bus object
    let selectedSeats = new Set();           // seat numbers (1-indexed)
    let occupiedSeats = new Set();           // for selected bus (1-indexed)

    // ---------- DOM elements ----------
    const fromSelect = document.getElementById('fromSelect');
    const toSelect = document.getElementById('toSelect');
    const datePicker = document.getElementById('datePicker');
    const searchBtn = document.getElementById('searchBtn');
    const busListEl = document.getElementById('busList');
    const bookingArea = document.getElementById('bookingArea');
    const seatsGrid = document.getElementById('seatsGrid');
    const selectedBusName = document.getElementById('selectedBusName');
    const summaryBus = document.getElementById('summaryBus');
    const summaryRoute = document.getElementById('summaryRoute');
    const summarySeats = document.getElementById('summarySeats');
    const summaryPrice = document.getElementById('summaryPrice');
    const summaryTotal = document.getElementById('summaryTotal');
    const messageBox = document.getElementById('messageBox');
    const bookBtn = document.getElementById('bookBtn');

    // ---------- helper functions ----------
    function getFilteredBuses(from, to) {
      return buses.filter(bus => bus.from === from && bus.to === to);
    }

    // reset selection (used when changing bus or searching)
    function resetSelection() {
      selectedBus = null;
      selectedSeats.clear();
      occupiedSeats.clear();
      bookingArea.style.display = 'none';
      messageBox.innerHTML = '';
      bookBtn.disabled = true;
      // also remove any selected class from cards
      document.querySelectorAll('.bus-card').forEach(card => card.classList.remove('selected'));
    }

    // render bus list based on current filters
    function renderBusList(filteredBuses) {
      if (!filteredBuses.length) {
        busListEl.innerHTML = `<div class="empty-state">🚌 No buses found for this route. Try a different search.</div>`;
        return;
      }

      busListEl.innerHTML = filteredBuses.map(bus => {
        // count available seats = total - occupied count
        const occupiedCount = bus.occupied.length;
        const available = bus.totalSeats - occupiedCount;
        // preserve selected class if this bus is selected
        const isSelected = selectedBus && selectedBus.id === bus.id;
        return `
          <div class="bus-card ${isSelected ? 'selected' : ''}" data-bus-id="${bus.id}">
            <div class="bus-info">
              <h3>${bus.name} <span class="seats-badge">${available} seats left</span></h3>
              <div class="route">${bus.from} → ${bus.to}</div>
              <div class="bus-meta">
                <span>🕒 ${bus.departure} — ${bus.arrival}</span>
                <span>💺 ${bus.totalSeats} seats</span>
              </div>
            </div>
            <div class="price-tag">$${bus.price}<small> /seat</small></div>
          </div>
        `;
      }).join('');

      // attach click listeners to bus cards
      document.querySelectorAll('.bus-card').forEach(card => {
        card.addEventListener('click', (e) => {
          const busId = card.dataset.busId;
          const bus = buses.find(b => b.id === busId);
          if (!bus) return;

          // if same bus clicked, do nothing (keep selection)
          if (selectedBus && selectedBus.id === bus.id) return;

          // set new bus
          selectedBus = bus;
          // update occupied set
          occupiedSeats = new Set(bus.occupied);
          // clear previously selected seats
          selectedSeats.clear();

          // update UI: remove selected class from all cards, add to this one
          document.querySelectorAll('.bus-card').forEach(c => c.classList.remove('selected'));
          card.classList.add('selected');

          // render seat grid
          renderSeatGrid();

          // show booking area
          bookingArea.style.display = 'grid';
          updateSummaryAndButton();

          // clear message
          messageBox.innerHTML = '';
        });
      });
    }

    // render seat grid for selectedBus
    function renderSeatGrid() {
      if (!selectedBus) return;

      const total = selectedBus.totalSeats;
      selectedBusName.textContent = `· ${selectedBus.name}`;

      let seatsHtml = '';
      for (let i = 1; i <= total; i++) {
        const isOccupied = occupiedSeats.has(i);
        const isSelected = selectedSeats.has(i);
        let seatClass = 'seat';
        if (isOccupied) seatClass += ' occupied';
        else if (isSelected) seatClass += ' selected';
        else seatClass += ' available';
        seatsHtml += `<div class="${seatClass}" data-seat="${i}">${i}</div>`;
      }
      seatsGrid.innerHTML = seatsHtml;

      // attach seat click listeners (only available seats)
      document.querySelectorAll('.seat.available').forEach(seatDiv => {
        seatDiv.addEventListener('click', (e) => {
          const seatNum = parseInt(seatDiv.dataset.seat, 10);
          if (occupiedSeats.has(seatNum)) return; // extra safety

          if (selectedSeats.has(seatNum)) {
            selectedSeats.delete(seatNum);
            seatDiv.classList.remove('selected');
            seatDiv.classList.add('available');
          } else {
            selectedSeats.add(seatNum);
            seatDiv.classList.remove('available');
            seatDiv.classList.add('selected');
          }
          updateSummaryAndButton();
          messageBox.innerHTML = ''; // clear messages on new selection
        });
      });
    }

    // update summary card and book button state
    function updateSummaryAndButton() {
      if (!selectedBus) {
        summaryBus.textContent = '—';
        summaryRoute.textContent = '—';
        summarySeats.textContent = '—';
        summaryPrice.textContent = '—';
        summaryTotal.textContent = '$0';
        bookBtn.disabled = true;
        return;
      }

      const seatCount = selectedSeats.size;
      const totalPrice = seatCount * selectedBus.price;

      summaryBus.textContent = selectedBus.name;
      summaryRoute.textContent = `${selectedBus.from} → ${selectedBus.to}`;
      summarySeats.textContent = seatCount === 0 ? 'None selected' : Array.from(selectedSeats).sort((a,b)=>a-b).join(', ');
      summaryPrice.textContent = `$${selectedBus.price}`;
      summaryTotal.textContent = `$${totalPrice}`;

      bookBtn.disabled = seatCount === 0;
    }

    // book action
    function handleBook() {
      if (!selectedBus || selectedSeats.size === 0) return;

      // simulate booking: mark seats as occupied
      const seatsToBook = Array.from(selectedSeats);
      // add to bus's occupied array (so future searches reflect)
      selectedBus.occupied = [...selectedBus.occupied, ...seatsToBook].sort((a,b)=>a-b);
      // update occupied set
      occupiedSeats = new Set(selectedBus.occupied);
      // clear selected seats
      selectedSeats.clear();

      // re-render seat grid (now booked seats are occupied)
      renderSeatGrid();

      // update summary and disable button
      updateSummaryAndButton();

      // also update bus list card seat count (refresh bus list)
      // re-render filtered buses to show updated available seats count
      const from = fromSelect.value;
      const to = toSelect.value;
      const filtered = getFilteredBuses(from, to);
      renderBusList(filtered);
      // but we must preserve selected bus highlight — after re-render, the bus card may not have selected class.
      // We'll re-apply selected class after render:
      if (selectedBus) {
        const busCard = document.querySelector(`.bus-card[data-bus-id="${selectedBus.id}"]`);
        if (busCard) busCard.classList.add('selected');
        // also keep booking area visible and selectedBusName
      }

      // show success message
      messageBox.innerHTML = `<div class="message success">✅ Booking confirmed! Seats ${seatsToBook.join(', ')} reserved. Thank you!</div>`;

      // update summary seats text (since cleared, will show none)
      summarySeats.textContent = 'None selected';
      summaryTotal.textContent = '$0';
      bookBtn.disabled = true;
    }

    // initial load: filter default route (New York -> Boston)
    function loadInitial() {
      const from = fromSelect.value;
      const to = toSelect.value;
      const filtered = getFilteredBuses(from, to);
      currentBuses = filtered;
      resetSelection();
      renderBusList(filtered);
    }

    // search handler
    function handleSearch() {
      const from = fromSelect.value;
      const to = toSelect.value;

      if (from === to) {
        alert('From and To cannot be the same city.');
        return;
      }

      const filtered = getFilteredBuses(from, to);
      currentBuses = filtered;
      resetSelection();
      renderBusList(filtered);
    }

    // ---------- event listeners ----------
    searchBtn.addEventListener('click', handleSearch);

    // also trigger search when selects change (optional, but convenient)
    fromSelect.addEventListener('change', () => {
      if (fromSelect.value === toSelect.value) {
        // avoid same city, but we let search button handle, just skip auto
        return;
      }
      // optional auto search? let's keep user pressing search.
    });

    // date picker is visual only for this demo
    bookBtn.addEventListener('click', handleBook);

    // initial render
    loadInitial();

    // ensure seats grid is cleared if no bus selected (booking area hidden)
    // if booking area hidden, fine.
  })();
</script>
</body>
</html>
