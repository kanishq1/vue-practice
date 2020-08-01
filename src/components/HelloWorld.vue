<template>
  <div id="calculator">
    <div class="container">
      <form action>
        <h1>EMI Calculator</h1>
        <label for="price">Purchase price</label>
        <input type="number" name="price" class="currency" v-model.number="price" />
        <br />
        <label for="down-payment">Down payment</label>
        <input type="number" name="down-payment" class="currency" v-model.number="downPayment" />
        <br />

        <label for="trade-in">Trade-in value</label>
        <input type="number" name="trade-in" class="currency" v-model.number="tradeIn" />
        <br />

        <label for="length">Term length</label>
        <select name="length" v-model="length">
          <option value="12">12 months</option>
          <option value="24">24 months</option>
          <option value="36">36 months</option>
          <option value="48">48 months</option>
          <option value="60" selected>60 months</option>
          <option value="72">72 months</option>
          <option value="84">84 months</option>
        </select>

        <label for="rate">Rate</label>
        <input type="number" name="rate" v-model.number="rate" />
      </form>
      <div class="payment">{{ calcPayment }} / month</div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Calculator",
  data() {
    return {
      price: "",
      downPayment: "",
      tradeIn: "",
      length: "12",
      rate: "",
    };
  },
  methods: {
    currencyFormat(num) {
      return "Rs." + num.toFixed(0).replace(/(\d)(?=(\d{3})+(?!\d))/g, "Rs.1,");
    },
    calcPayment() {
      var p = this.price - this.downPayment - this.tradeIn;
      var r = this.rate / 1200;
      var n = this.length;
      var i = Math.pow(1 + r, n);
      var payment = (p * r * i) / (i - 1) || 0;
      return "Rs." + payment.toFixed(0);
    },
    numFormat(e) {
      e.replace(/(\d)(?=(\d\d\d)+(?!\d))/g, "Rs.1,");
    },
  },
};
</script>

<style scoped>
h1 {
  text-align: center;
  color: #000;
  margin: 0 0 16px 0;
}

p {
  text-align: center;
  margin-top: 0;
  margin-bottom: 24px;
}

.container {
  max-width: 480px;
  margin: 0 auto;
  background-color: #fff;
  padding: 64px;
  box-shadow: 2px 2px 96px #111;
  border-radius: 8px;
  -webkit-transition: all 0.3s ease-in;
  transition: all 0.3s ease-in;
}
@media (max-width: 512px) {
  .container {
    padding: 32px;
    -webkit-transition: all 0.3s ease-in;
    transition: all 0.3s ease-in;
  }
}
@media (max-width: 360px) {
  .container {
    padding: 16px;
    -webkit-transition: all 0.3s ease-in;
    transition: all 0.3s ease-in;
  }
}

label {
  display: inline-block;
  width: 25%;
  min-width: 128px;
  margin-bottom: 8px;
  font-weight: bold;
}

input,
select {
  display: inline-block;
  background-color: #fff;
  color: #888;
  border: 2px solid #888;
  border-radius: 2px;
  height: 56px;
  width: 100%;
  font-size: 24px;
  padding: 0 16px;
  margin-bottom: 24px;
}
input:focus,
select:focus {
  background-color: #fff;
  color: #3200ff;
  border-color: #3200ff;
  outline: 0;
}

input[type="number"]::-webkit-inner-spin-button,
input[type="number"]::-webkit-outer-spin-button {
  -webkit-appearance: none;
  margin: 0;
}

.payment {
  color: #000;
  font-size: 48px;
  text-align: center;
  font-weight: bold;
  -webkit-transition: all 0.3s ease-in;
  transition: all 0.3s ease-in;
}
@media (max-width: 512px) {
  .payment {
    font-size: 40px;
    -webkit-transition: all 0.3s ease-in;
    transition: all 0.3s ease-in;
  }
}
@media (max-width: 400px) {
  .payment {
    font-size: 32px;
    -webkit-transition: all 0.3s ease-in;
    transition: all 0.3s ease-in;
  }
}

@media (max-height: 750px) {
  body {
    height: 100%;
  }
}
</style>
