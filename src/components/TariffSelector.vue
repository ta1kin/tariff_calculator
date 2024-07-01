<template>
    <div>
      <h2>Выберите тариф</h2>
      <select @change="onSelectTariff($event)">
        <option value="standard">Стандартный - 100 руб/мес или 1000 руб/год</option>
        <option value="advanced">Продвинутый - 150 руб/мес или 1400 руб/год</option>
      </select>
    </div>
  </template>
  
  <script>
  export default {
    methods: {
      onSelectTariff(event) {
        this.$emit('select-tariff', event.target.value);
      }
    }
  };
  </script>