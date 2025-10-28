<!doctype html>
<html>
  <head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Basic Coffee Shop</title>
    <style>
      /* ---------- Global ---------- */
      :root {
        --bg: #67E2CC;
        --panel: #EED675;
        --cart-width: 280px;
        --gap: 12px;
        --radius: 10px;
        --text-color: #111;
      }

      html, body {
        margin: 0;
        padding: 0;
        font-family: Arial, Helvetica, sans-serif;
        color: var(--text-color);
        background: var(--bg);
        -webkit-font-smoothing: antialiased;
      }

      /* Container for main content (leaves space for cart on wide screens) */
      #main {
        padding: 16px;
        box-sizing: border-box;
        margin: 0 auto;
        max-width: 1100px;
      }

      h1 {
        margin: 6px 0 8px 0;
        font-size: 28px;
      }

      h3 {
        margin: 16px 0 8px 0;
        font-size: 20px;
      }

      p {
        margin: 8px 0;
        font-size: 16px;
      }

      /* ---------- Product table ---------- */
      #productsTable {
        width: 100%;
        border-collapse: separate;
        border-spacing: 8px;
        background: var(--panel);
        padding: 8px;
        box-sizing: border-box;
        border: 2px solid #000;
        border-radius: var(--radius);
      }

      #productsTable th {
        text-align: left;
        padding: 8px;
        font-size: 16px;
      }

      #productsTable td {
        padding: 8px;
        vertical-align: middle;
        background: transparent;
      }

      /* make each product row look clearer */
      #productsTable tr {
        background: transparent;
      }

      /* Product images */
      #productsTable img {
        width: 180px;      /* big on desktop */
        height: auto;
        display: block;
        border-radius: 14px;
        box-shadow: 0 4px 10px rgba(0,0,0,0.12);
      }

      /* Buttons */
      button {
        background: white;
        border: 1px solid #444;
        padding: 8px 12px;
        border-radius: 8px;
        font-size: 15px;
        cursor: pointer;
      }
      button:active {
        transform: translateY(1px);
      }

      /* Add Coffee button area */
      .add-area {
        margin-top: 12px;
      }

      /* ---------- Cart (desktop fixed) ---------- */
      #cartTable {
        width: var(--cart-width);
        border-collapse: collapse;
        position: fixed;
        right: 14px;
        top: 20px;
        background: #fff;
        max-height: 360px;
        overflow-y: auto;
        display: block;
        box-sizing: border-box;
        padding: 6px;
        border-radius: var(--radius);
        border: 2px solid #000;
      }

      #cartTable th, #cartTable td {
        padding: 8px;
        border-bottom: 1px solid rgba(0,0,0,0.06);
        text-align: left;
        background: transparent;
        font-size: 15px;
      }

      /* Keep the total row visible style */
      #totalRow td {
        font-weight: bold;
        border-top: 2px solid #ddd;
      }

      /* ---------- Responsive rules (phones & small screens) ---------- */
      @media (max-width: 900px) {

        /* Main uses full width on phones and no right margin */
        #main {
          padding: 12px;
          max-width: 100%;
        }

        /* product images scale down to fit phone */
        #productsTable img {
          width: 100%;
          max-width: 300px;   /* avoid extremely large images */
        }

        /* Make table cells readable on small screens */
        #productsTable th, #productsTable td {
          font-size: 15px;
          padding: 8px;
          display: table-cell;
        }

        /* Move cart below (no fixed positioning) */
        #cartTable {
          position: static;
          width: 100%;
          margin-top: 14px;
          max-height: none;
          overflow: visible;
          display: table;
        }

        /* Bigger headings on mobile to read easily */
        h1 { font-size: 22px; }
        h3 { font-size: 18px; }

        /* Make buttons easier to tap */
        button {
          padding: 12px 14px;
          font-size: 16px;
          border-radius: 10px;
        }

      }

      /* small touch-friendly tweaks for very small phones */
      @media (max-width: 420px) {
        h1 { font-size: 20px; }
        #productsTable img { max-width: 260px; }
        #productsTable th, #productsTable td { font-size: 14px; }
      }
    </style>
  </head>
  <body>

    <div id="main">
      <h1>Coffee Shop</h1>

      <p>Cart: <b id="cart">0</b> items</p>

      <hr>

      <h3>Products</h3>

      <!-- Product Table (normal flow) -->
      <table id="productsTable" border="0" cellspacing="0" cellpadding="0">
        <tr>
          <th>Image</th>
          <th>Name</th>
          <th>Price</th>
          <th>Actions</th>
        </tr>

        <tr>
          <td>
            <img src="https://upload.wikimedia.org/wikipedia/commons/4/45/A_small_cup_of_coffee.JPG" alt="Espresso">
          </td>
          <td>Espresso</td>
          <td>₹120</td>
          <td><button onclick="add('Espresso',120)">Add</button></td>
        </tr>

        <tr>
          <td>
            <img src="https://images.unsplash.com/photo-1525088553746-0c6e8f5872f1?q=80&w=1200&auto=format&fit=crop&ixlib=rb-4.0.3&s=4b38b9d5b55ae7892c5d6f8f5b9b8f97" alt="Cappuccino">
          </td>
          <td>Cappuccino</td>
          <td>₹150</td>
          <td><button onclick="add('Cappuccino',150)">Add</button></td>
        </tr>

        <tr>
          <td>
            <img src="https://images.unsplash.com/photo-1511920170033-f8396924c348?q=80&w=1200&auto=format&fit=crop&ixlib=rb-4.0.3&s=673e5b6d3f05d5d4c2e5f9a1b6b5adbd" alt="Latte">
          </td>
          <td>Latte</td>
          <td>₹140</td>
          <td><button onclick="add('Latte',140)">Add</button></td>
        </tr>
      </table>

      <div class="add-area">
        <button onclick="addCoffee()">Add Coffee</button>
      </div>

    </div>

    <!-- Cart Table on the right (fixed on wide screens, stacked on mobile) -->
    <table id="cartTable" border="0" cellspacing="0" cellpadding="0" aria-label="Cart">
      <tr>
        <th>Item</th>
        <th>Price</th>
      </tr>

      <tr id="totalRow">
        <td><b>Total:</b></td>
        <td><b id="total">₹0</b></td>
      </tr>
    </table>

    <script>
      var count = 0;
      var total = 0;

      function add(name, price) {
        count++;
        document.getElementById('cart').textContent = count;

        var table = document.getElementById('cartTable');
        var totalRow = document.getElementById('totalRow');

        // insert new item row before total row
        var row = table.insertRow(totalRow.rowIndex);
        var c1 = row.insertCell(0);
        var c2 = row.insertCell(1);
        c1.textContent = name;
        c2.textContent = '₹' + price;

        total += Number(price);
        document.getElementById('total').textContent = '₹' + total;
      }

      function addCoffee() {
        var name = prompt("Enter coffee name:");
        if (!name) return;

        var price = prompt("Enter price (in ₹):");
        if (!price || isNaN(price)) {
          alert("Please enter a valid number for price.");
          return;
        }

        var img = prompt("Enter image URL (optional):");
        if (!img) {
          img = "https://upload.wikimedia.org/wikipedia/commons/4/45/A_small_cup_of_coffee.JPG";
        }

        // create new product row
        var table = document.getElementById('productsTable');
        var row = table.insertRow();
        var c1 = row.insertCell(0);
        var c2 = row.insertCell(1);
        var c3 = row.insertCell(2);
        var c4 = row.insertCell(3);

        // sanitize the img URL string (basic)
        var safeImg = String(img).replace(/"/g,'');

        c1.innerHTML = '<img src="' + safeImg + '" alt="' + name.replace(/"/g,'') + '">';
        c2.textContent = name;
        c3.textContent = '₹' + price;

        var btn = document.createElement('button');
        btn.textContent = 'Add';
        btn.onclick = function() { add(name, Number(price)); };
        c4.appendChild(btn);
      }
    </script>

  </body>
</html>
