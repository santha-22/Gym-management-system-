# Gym-management-system-
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Gym Receipt and Notifications</title>
    <link rel="stylesheet" href="styles.css">
</head>
<body>

    <div class="container">
        <header>
            <h1>Gym Receipt & Notifications</h1>
        </header>

        <!-- User Receipts Section -->
        <section class="receipts-section">
            <h2>Save Your Payment Receipts</h2>
            <form id="receiptForm">
                <label for="receiptId">Receipt ID:</label>
                <input type="text" id="receiptId" placeholder="Enter Receipt ID" required><br>
                
                <label for="amount">Amount Paid:</label>
                <input type="number" id="amount" placeholder="Enter Amount" required><br>

                <label for="date">Payment Date:</label>
                <input type="date" id="date" required><br>

                <button type="submit">Save Receipt</button>
            </form>

            <div id="receiptList">
                <h3>Saved Receipts:</h3>
                <ul id="receiptUl"></ul>
            </div>
        </section>

        <!-- Gym Working Days Section -->
        <section class="working-days">
            <h2>Gym Working & Non-Working Days</h2>
            <div id="workingDays">
                <h3>Working Days:</h3>
                <p>Monday to Friday: 6 AM - 10 PM</p>
            </div>
            <div id="nonWorkingDays">
                <h3>Non-Working Days:</h3>
                <p>Saturday and Sunday</p>
            </div>
        </section>
        
    </div>

    <script src="app.js"></script>
</body>
</html>
body {
    font-family: Arial, sans-serif;
    margin: 0;
    padding: 0;
    background-color: #f4f4f4;
}

.container {
    width: 80%;
    margin: 20px auto;
    padding: 20px;
    background-color: #fff;
    box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
}

header {
    text-align: center;
    margin-bottom: 30px;
}

h1 {
    font-size: 2.5rem;
}

h2 {
    color: #333;
}

form {
    margin-bottom: 20px;
}

label {
    display: block;
    margin-bottom: 8px;
}

input[type="text"],
input[type="number"],
input[type="date"] {
    width: 100%;
    padding: 10px;
    margin-bottom: 12px;
    border: 1px solid #ccc;
    border-radius: 4px;
}

button {
    background-color: #4CAF50;
    color: white;
    padding: 10px 15px;
    border: none;
    border-radius: 5px;
    cursor: pointer;
}

button:hover {
    background-color: #45a049;
}

#receiptList ul {
    list-style-type: none;
    padding: 0;
}

#receiptList ul li {
    background-color: #f1f1f1;
    margin: 10px 0;
    padding: 10px;
    border-radius: 5px;
}

section {
    margin-bottom: 40px;
}
document.getElementById('receiptForm').addEventListener('submit', function(event) {
    event.preventDefault();

    // Get form values
    const receiptId = document.getElementById('receiptId').value;
    const amount = document.getElementById('amount').value;
    const date = document.getElementById('date').value;

    // Create a receipt object
    const receipt = {
        receiptId,
        amount,
        date
    };

    // Store the receipt data in local storage (if needed)
    let receipts = JSON.parse(localStorage.getItem('receipts')) || [];
    receipts.push(receipt);
    localStorage.setItem('receipts', JSON.stringify(receipts));

    // Display the receipt
    displayReceipts();

    // Reset the form
    document.getElementById('receiptForm').reset();
});

// Display saved receipts
function displayReceipts() {
    const receipts = JSON.parse(localStorage.getItem('receipts')) || [];
    const receiptUl = document.getElementById('receiptUl');
    receiptUl.innerHTML = ''; // Clear existing list

    receipts.forEach(receipt => {
        const li = document.createElement('li');
        li.textContent = `Receipt ID: ${receipt.receiptId}, Amount: $${receipt.amount}, Date: ${receipt.date}`;
        receiptUl.appendChild(li);
    });
}

// Initialize the display of receipts when the page loads
window.onload = displayReceipts;