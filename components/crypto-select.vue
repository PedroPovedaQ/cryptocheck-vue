<template lang="html">
  <div class="crypto-container">
    <sui-dropdown placeholder="Select Currency"
                  selection
                  :options="getFormattedCurrencies(currencies)"
                  v-model="current" />
    <div class="ui centered two column grid">
      <div class="three column row">
        <sui-form v-if="current"
                  class="column">
          <sui-form-field class="small-2 medium-3 columns">
            <label>How much {{currencies[current].name}} do you own?</label>
            <input type="number"
                   v-model="currencyAmount">
          </sui-form-field>
          <sui-form-field class="small-2 medium-3 columns">
            <label>At what price did you purchase your {{currencies[current].name}}?</label>
            <input type="number"
                   v-model="originalPrice">
          </sui-form-field>
          <sui-button type="submit"
                      class="ui primary button"
                      @click.prevent="onSubmit()">Submit</sui-button>
        </sui-form>
      </div>
      <div class="three column row"
           v-if="submitted">
        <div class="column">
          <sui-table celled
                     class="small-2 medium-3 columns">
            <sui-table-header>
              <sui-table-row>
                <sui-table-header-cell>Coin</sui-table-header-cell>
                <sui-table-header-cell>Initial Price</sui-table-header-cell>
                <sui-table-header-cell>Current Price</sui-table-header-cell>
                <sui-table-header-cell>Profit/Loss</sui-table-header-cell>
              </sui-table-row>
            </sui-table-header>
            <sui-table-body>
              <sui-table-row>
                <sui-table-cell>
                  {{currencies[current].name}}
                </sui-table-cell>
                <sui-table-cell>{{getDisplayableCurrency(originalPrice)}}</sui-table-cell>
                <sui-table-cell>{{getDisplayableCurrency(currencies[current].price_usd)}}</sui-table-cell>
                <sui-table-cell>{{showProfit(originalPrice, currencies[current].price_usd, currencyAmount)}}</sui-table-cell>
              </sui-table-row>
            </sui-table-body>
          </sui-table>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  props: ['currencies'],
  data() {
    return {
      current: null,
      currencyAmount: null,
      originalPrice: null,
      submitted: false
    };
  },
  computed: {},
  methods: {
    getFormattedCurrencies: function(currencies) {
      if (Object.keys(currencies).length < 1) {
        return [];
      }
      return Object.keys(currencies).map(currencyId => {
        return {
          text: currencies[currencyId].name,
          value: currencies[currencyId].id
        };
      });
    },
    getDisplayableCurrency(currencyAmount) {
      return `$${Number(currencyAmount).toFixed(2)}`;
    },
    showProfit: function(originalPrice, currentPrice, amount) {
      let result;
      result = amount * currentPrice - amount * originalPrice;
      return `$${Number(result).toFixed(2)}`;
    },
    onSubmit: function() {
      this.submitted = true;
    }
  },
  watch: {
    current() {
      this.submitted = false;
      this.currencyAmount = null;
      this.originalPrice = null;
    }
  }
};

</script>

<style>
.crypto-container {
  text-align: center;
  margin-top: 5vh;
}
</style>
