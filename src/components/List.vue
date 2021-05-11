<template>
  <div>
    <ul>
        <li v-for="order in displayOrders" :key='order.id'>
            {{ order.name }} - {{ order.price }} - {{ order.notes }}
            <div class='pencil-icon' @click='handleOpenModal("edit", order)'>
                <font-awesome-icon :icon="['fas', 'pencil-alt']" />
            </div>
            <div class='trash-icon' @click='handleOpenModal("delete", order)'>
                <font-awesome-icon :icon="['fas', 'trash-alt']" />
            </div>
        </li>
    </ul>
  </div>
</template>

<script>
export default {
    name: 'List',
    props: {
        displayOrders: Array,
        handleOpenModal: Function
    },
    data() {
        return {}
    }
}
</script>

<style>
.pencil-icon:hover,
.pencil-icon:focus {
  color: red;
  text-decoration: none;
  cursor: pointer;
}
.trash-icon:hover,
.trash-icon:focus {
  color: red;
  text-decoration: none;
  cursor: pointer;
}
</style>