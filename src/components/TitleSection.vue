<template>
  <div>
    <h1>Drink Something</h1>
    <div><font-awesome-icon :icon="['fas', 'plus']" /></div>
    <div><font-awesome-icon :icon="['fas', 'pencil-alt']" /></div>
    <div><font-awesome-icon :icon="['fas', 'trash-alt']" /></div>
    <select v-model="selected">
      <option disabled value="">Please select sorting method</option>
      <option>Original</option>
      <option>By name (ascending)</option>
      <option>By name (descending)</option>
      <option>By price (ascending)</option>
      <option>By price (descending)</option>
    </select>
  </div>
  
</template>

<script>
export default {
  name: 'List',
  props: {
      orders: Array,
      sortOrder: Function
  },
  data() {
    return {
      selected: ''
    }
  },
  watch: {
    selected: function(newVal) {
      this.sortOrder(newVal)
    }
  }
}
</script>

<style>

</style>