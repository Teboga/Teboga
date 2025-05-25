<head>
  <meta charset="UTF-8">
  <title>Teboga Electrical Calculator</title>
  <style>
    body { font-family: Arial; max-width: 600px; margin: auto; padding: 20px; }
    select, input { width: 100%; padding: 8px; margin: 8px 0; }
    button { padding: 10px; width: 100%; background-color: #28a745; color: white; border: none; }
    .section { margin-top: 20px; }
    .result, .company { margin-top: 20px; font-weight: bold; }
    .company { font-size: 12px; color: gray; border-top: 1px solid #ddd; padding-top: 10px; }
  </style>
</head>
<body>
  <h2>⚡ Teboga Electrical Calculator</h2>

  <div class="company">
    <strong>Company:</strong> Teboga Electrical<br>
    <strong>Address:</strong> 1090 Tshikota Location<br>
    <strong>Email:</strong> tebogaelec@gmail.com<br>
    <strong>Reg. No:</strong> 2017/093900/07
  </div>

  <div class="section">
    <label for="service">Choose a Service:</label>
    <select id="service">
      <option value="450">Residential Wiring - R450/hr</option>
      <option value="600">Commercial Maintenance - R600/hr</option>
      <option value="750">Solar Panel Installation - R750/hr</option>
      <option value="1000">Emergency Call-out - R1000/hr</option>
    </select>

    <label for="hours">Hours Worked:</label>
    <input type="number" id="hours" placeholder="e.g. 3.5" step="0.1" />

    <label for="sqm">Square Meters (optional):</label>
    <input type="number" id="sqm" placeholder="e.g. 45" />

    <label for="ratePerSqm">Rate per m² (if applicable):</label>
    <input type="number" id="ratePerSqm" placeholder="e.g. 50" />

    <label for="distance">Distance to Site (km):</label>
    <input type="number" id="distance" placeholder="e.g. 10" />

    <label for="travelRate">Rate per km:</label>
    <input type="number" id="travelRate" value="5" />

    <label for="materials">Material Cost (R):</label>
    <input type="number" id="materials" placeholder="e.g. 350" />

    <label for="serviceCount">Number of Services Acquired:</label>
    <input type="number" id="serviceCount" placeholder="e.g. 7" />

    <label><input type="checkbox" id="isReferral"> Referral Customer</label><br>
    <label><input type="checkbox" id="vat"> Include VAT (15%)</label>

    <button onclick="calculate()">Calculate Total</button>

    <div class="result" id="result"></div>
  </div>

  <script>
    function calculate() {
      const rate = parseFloat(document.getElementById('service').value);
      const hours = parseFloat(document.getElementById('hours').value) || 0;
      const sqm = parseFloat(document.getElementById('sqm').value) || 0;
      const ratePerSqm = parseFloat(document.getElementById('ratePerSqm').value) || 0;
      const distance = parseFloat(document.getElementById('distance').value) || 0;
      const travelRate = parseFloat(document.getElementById('travelRate').value) || 0;
      const material = parseFloat(document.getElementById('materials').value) || 0;
      const serviceCount = parseInt(document.getElementById('serviceCount').value) || 0;
      const isReferral = document.getElementById('isReferral').checked;
      const includeVAT = document.getElementById('vat').checked;

      const labourCost = rate * hours;
      const sqmCost = sqm * ratePerSqm;
      const travelCost = distance * travelRate;
      const subtotal = labourCost + sqmCost + travelCost + material;

      // Determine customer rank and discount
      let rank = 'Bronze';
      let rankDiscount = 0;
      if (serviceCount >= 21) {
        rank = 'Platinum';
        rankDiscount = 0.06;
      } else if (serviceCount >= 11) {
        rank = 'Gold';
        rankDiscount = 0.04;
      } else if (serviceCount >= 6) {
        rank = 'Silver';
        rankDiscount = 0.02;
      }

      // Additional discounts
      const loyaltyDiscount = serviceCount >= 3 ? 0.05 : 0;
      const referralDiscount = isReferral ? 0.03 : 0;

      const totalDiscountRate = rankDiscount + loyaltyDiscount + referralDiscount;
      const discountAmount = subtotal * totalDiscountRate;
      const discountedSubtotal = subtotal - discountAmount;

      const vatAmount = includeVAT ? discountedSubtotal * 0.15 : 0;
      const total = discountedSubtotal + vatAmount;

      document.getElementById('result').innerHTML = `
        Labour: R${labourCost.toFixed(2)}<br>
        Square Meter Work: R${sqmCost.toFixed(2)}<br>
        Travel: R${travelCost.toFixed(2)}<br>
        Materials: R${material.toFixed(2)}<br>
        Subtotal: R${subtotal.toFixed(2)}<br>
        Customer Rank: ${rank}<br>
        Total Discounts: R${discountAmount.toFixed(2)}<br>
        VAT: R${vatAmount.toFixed(2)}<br><br>
        <strong>Total: R${total.toFixed(2)}</strong>
      `;
    }
  </script>
</body>
</html>## Hi there 👋

<!--
**Teboga/Teboga** is a ✨ _special_ ✨ repository because its `README.md` (this file) appears on your GitHub profile.

Here are some ideas to get you started:

- 🔭 I’m currently working on ...
- 🌱 I’m currently learning ...
- 👯 I’m looking to collaborate on ...
- 🤔 I’m looking for help with ...
- 💬 Ask me about ...
- 📫 How to reach me: ...
- 😄 Pronouns: ...
- ⚡ Fun fact: ...
-->
