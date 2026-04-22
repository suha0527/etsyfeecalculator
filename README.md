# etsyfeecalculator
EtsyFeeCalculator
<div class="etsy-calculator">
  <h1>Etsy Profit Calculator</h1>
  <p class="subtitle">Instantly calculate your Etsy fees, profit & margins</p>

  <div class="grid">
    <div class="input-group">
      <label>Product Price ($)</label>
      <input type="number" id="price" value="25">
    </div>

    <div class="input-group">
      <label>Shipping Charged ($)</label>
      <input type="number" id="shippingCharged" value="5">
    </div>

    <div class="input-group">
      <label>Shipping Cost ($)</label>
      <input type="number" id="shippingCost" value="4">
    </div>

    <div class="input-group">
      <label>Quantity</label>
      <input type="number" id="quantity" value="1">
    </div>
  </div>

  <div class="results">
    <div class="card">
      <span>Total Fees</span>
      <h2 id="fees">$0.00</h2>
    </div>

    <div class="card highlight">
      <span>Net Profit</span>
      <h2 id="profit">$0.00</h2>
    </div>

    <div class="card">
      <span>Profit Margin</span>
      <h2 id="margin">0%</h2>
    </div>
  </div>
</div>

<style>
.etsy-calculator {
  max-width: 800px;
  margin: auto;
  padding: 30px;
  border-radius: 20px;
  background: linear-gradient(135deg, #ffffff, #f7f7f7);
  box-shadow: 0 10px 40px rgba(0,0,0,0.08);
  font-family: -apple-system, BlinkMacSystemFont, sans-serif;
}

h1 {
  text-align: center;
  margin-bottom: 5px;
}

.subtitle {
  text-align: center;
  color: #777;
  margin-bottom: 25px;
}

.grid {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 15px;
}

.input-group label {
  font-size: 14px;
  color: #555;
}

.input-group input {
  width: 100%;
  padding: 10px;
  border-radius: 8px;
  border: 1px solid #ddd;
  margin-top: 5px;
}

.results {
  display: flex;
  justify-content: space-between;
  margin-top: 25px;
  gap: 15px;
}

.card {
  flex: 1;
  padding: 20px;
  border-radius: 15px;
  background: #fafafa;
  text-align: center;
  box-shadow: inset 0 0 0 1px #eee;
}

.card h2 {
  margin-top: 10px;
}

.highlight {
  background: linear-gradient(135deg, #ff6600, #ff8533);
  color: white;
}

@media(max-width:600px){
  .grid {
    grid-template-columns: 1fr;
  }
  .results {
    flex-direction: column;
  }
}
</style>

<script>
const inputs = document.querySelectorAll("#price, #shippingCharged, #shippingCost, #quantity");

inputs.forEach(input => {
  input.addEventListener("input", calculate);
});

function calculate() {
  let price = parseFloat(document.getElementById("price").value) || 0;
  let shippingCharged = parseFloat(document.getElementById("shippingCharged").value) || 0;
  let shippingCost = parseFloat(document.getElementById("shippingCost").value) || 0;
  let quantity = parseInt(document.getElementById("quantity").value) || 1;

  let listingFee = 0.20 * quantity;
  let transactionFee = 0.065 * (price + shippingCharged) * quantity;
  let paymentFee = (0.03 * (price + shippingCharged) + 0.25) * quantity;

  let totalFees = listingFee + transactionFee + paymentFee;
  let revenue = (price + shippingCharged) * quantity;
  let totalShippingCost = shippingCost * quantity;

  let profit = revenue - totalFees - totalShippingCost;
  let margin = revenue > 0 ? (profit / revenue) * 100 : 0;

  document.getElementById("fees").innerText = "$" + totalFees.toFixed(2);
  document.getElementById("profit").innerText = "$" + profit.toFixed(2);
  document.getElementById("margin").innerText = margin.toFixed(2) + "%";
}

calculate();
</script>
