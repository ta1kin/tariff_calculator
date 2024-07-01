<template>
    <div>
      <h2>Выберите период оплаты</h2>
      <select @change="onSelectPeriod($event)">
        <option value="month">Ежемесячно</option>
        <option value="year">Ежегодно</option>
      </select>
    </div>
</template>
  
<script>
  export default {
    methods: {
      onSelectPeriod(event) {
        this.$emit('select-period', event.target.value);
      }
    }
  };
</script>
  