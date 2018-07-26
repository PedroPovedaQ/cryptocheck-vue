<template>
  <div>
    <header class="App-header">
      <img src="/logo.png" class="App-logo" alt="logo">
      <h1 class="title">Welcome to your Crypto Portfolio</h1>
    </header>
    <crypto-select :currencies="getCurrencyMap(currencies)"/>
  </div>
</template>

<script>
import CryptoSelect from '~/components/crypto-select';
import axios from 'axios';

export default {
  async asyncData({ params }) {
    let { data } = await axios.get(`https://api.coinmarketcap.com/v1/ticker/`);
    return { currencies: data };
  },
  components: {
    CryptoSelect
  },
  methods: {
    getCurrencyMap: function(currencies) {
      if(!currencies) {
        return {};
      }
      let currencyMap = {};
      currencies.map(currency => {
        currencyMap[currency.id] = currency;
      });
      return currencyMap;
    }
  }
};
</script>

<style>
header {
  background-color: #222;
  height: 200px;
  padding: 20px;
  color: #fff;
  text-align: center;
}
.container {
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}
.title {
  margin-top: 20px;
}
.subtitle {
  font-weight: 300;
  font-size: 42px;
  color: #526488;
  word-spacing: 5px;
  padding-bottom: 15px;
}
.links {
  padding-top: 15px;
}
.App-logo {
  animation: App-logo-spin infinite 20s linear;
  height: 80px;
}
@keyframes App-logo-spin {
  from {
    transform: rotate(0deg);
  }
  to {
    transform: rotate(360deg);
  }
}

.title {
  font-size: 1.5em;
  color: #fff;
}
</style>
