<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Concert Seating Reservation</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background-color: #f4f4f4;
      margin: 0;
      padding: 0;
      text-align: center;
    }
    header {
      background-color: #333;
      color: white;
      padding: 20px;
    }
    .container {
      margin: 20px auto;
      width: 80%;
    }
    .seat-grid {
      display: grid;
      grid-template-columns: repeat(10, 40px);
      gap: 5px;
      justify-content: center;
      margin: 20px 0;
    }
    .seat {
      width: 40px;
      height: 40px;
      background-color: #4CAF50;
      border-radius: 5px;
      cursor: pointer;
      color: white;
      display: flex;
      align-items: center;
      justify-content: center;
      font-size: 12px;
    }
    .seat.reserved {
      background-color: #e74c3c;
      cursor: not-allowed;
    }
    .seat.selected {
      background-color: #3498db;
    }
    form {
      background: white;
      padding: 20px;
      border-radius: 10px;
      box-shadow: 0 0 10px rgba(0,0,0,0.1);
      display: inline-block;
    }
    input, select, button {
      margin: 10px;
      padding: 10px;
      width: 80%;
    }
    button {
      background-color: #4CAF50;
      color: white;
      border: none;
      cursor: pointer;
      font-size: 16px;
    }
    button:hover {
      background-color: #45a049;
    }
  </style>
</head>
<body>
  <header>
    <h1>Concert Seating Reservation</h1>
    <p>Choose your seat and reserve now!</p>
  </header>
  <div class="container">
    <h2>Select a Seat</h2>
    <div class="seat-grid" id="seatGrid"></div>

    <form id="reservationForm">
      <h3>Reservation Form</h3>
      <input type="text" id="name" placeholder="Full Name" required>
      <input type="text" id="contact" placeholder="Contact Number" required>
      <input type="text" id="selectedSeat" placeholder="Selected Seat" readonly>
      <button type="submit">Reserve Seat</button>
    </form>
  </div>

  <script>
    const seatGrid = document.getElementById('seatGrid');
    const selectedSeatInput = document.getElementById('selectedSeat');
    const totalSeats = 50; // 5 rows x 10 columns
    let selectedSeat = null;

    for (let i = 1; i <= totalSeats; i++) {
      const seat = document.createElement('div');
      seat.classList.add('seat');
      seat.textContent = i;
      seat.addEventListener('click', () => {
        if (seat.classList.contains('reserved')) return;
        document.querySelectorAll('.seat.selected').forEach(s => s.classList.remove('selected'));
        seat.classList.add('selected');
        selectedSeat = i;
        selectedSeatInput.value = `Seat ${i}`;
      });
      seatGrid.appendChild(seat);
    }

    document.getElementById('reservationForm').addEventListener('submit', (e) => {
      e.preventDefault();
      if (!selectedSeat) {
        alert('Please select a seat before reserving.');
        return;
      }
      const seatDivs = document.querySelectorAll('.seat');
      seatDivs[selectedSeat - 1].classList.add('reserved');
      seatDivs[selectedSeat - 1].classList.remove('selected');
      alert(`Reservation confirmed for ${selectedSeatInput.value}!`);
      selectedSeatInput.value = '';
      selectedSeat = null;
      e.target.reset();
    });
  </script>
</body>
</html>
