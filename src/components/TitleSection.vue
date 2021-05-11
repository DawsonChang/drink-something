<template>
  <div >
    <h1 class="title">Drink Something</h1>
    <div class="section">
    <div @click='handleOpenModal("add", {})' class="plus-icon"><font-awesome-icon :icon="['fas', 'plus']" /></div>
    <div>
      <select v-model="selected" @click='sortOrder(selected)'>
        <option disabled value="">Please select sorting method</option>
        <option>Original</option>
        <option>By name (ascending)</option>
        <option>By name (descending)</option>
        <option>By price (ascending)</option>
        <option>By price (descending)</option>
      </select>
    </div>
    </div>
  </div>
  
</template>

<script>
export default {
  name: 'List',
  props: {
      sortOrder: Function,
      handleOpenModal: Function
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

.title {
  text-align: center;
}

.section {
  display: flex;
  justify-content: center;
}

.plus-icon {
  padding-right: 20px;
}

.plus-icon:hover,
.plus-icon:focus {
  color: red;
  text-decoration: none;
  cursor: pointer;
}

</style>