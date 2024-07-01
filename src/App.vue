<template>
  <div id="app">
    <h1>Тарифный калькулятор</h1>
    <TariffSelector @select-tariff="setTariff"/>
    <CurrencySelector :exchange-rates="exchangeRates" @select-currency="setCurrency"/>
    <PaymentPeriodSelector @select-period="setPeriod"/>
    <ResultDisplay :tariff="selectedTariff" :currency="selectedCurrency" :period="selectedPeriod" :exchange-rates="exchangeRates"/>
  </div>
</template>

<script>
import axios from 'axios';
import TariffSelector from './components/TariffSelector.vue';
import CurrencySelector from './components/CurrencySelector.vue';
import PaymentPeriodSelector from './components/PaymentPeriodSelector.vue';
import ResultDisplay from './components/ResultDisplay.vue';

export default {
  name: 'App',
  components: {
    TariffSelector,
    CurrencySelector,
    PaymentPeriodSelector,
    ResultDisplay
  },
  data() {
    return {
      exchangeRates: {},
      selectedTariff: null,
      selectedCurrency: 'RUB',
      selectedPeriod: 'month'
    };
  },
  methods: {
    setTariff(tariff) {
      this.selectedTariff = tariff;
    },
    setCurrency(currency) {
      this.selectedCurrency = currency;
    },
    setPeriod(period) {
      this.selectedPeriod = period;
    },
    fetchExchangeRates() {
      axios.get('https://api.exchangerate-api.com/v4/latest/RUB')
        .then(response => {
          this.exchangeRates = response.data.rates;
        })
        .catch(error => {
          console.error("There was an error fetching the exchange rates!", error);
        });
    }
  },
  created() {
    this.fetchExchangeRates();
  }
};
</script>

<style>
#app {
  font-family: Arial, sans-serif;
  text-align: center;
  margin-top: 50px;
}

@media (max-width: 600px) {
  #app {
    margin: 10px;
  }
}
</style>