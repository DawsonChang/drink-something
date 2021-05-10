<template>
  <div>
    <ul>
        <li v-for="order in orders" :key="order.id" @click="deleteOrder(order.id)">
            {{ order.name }} - {{ order.price }} - {{ order.notes }}
        </li>
    </ul>
  </div>
</template>

<script>
export default {
    name: 'List',
    props: {
        orders: Array,
        deleteOrder: Function
    },
    data() {
        return {}
    }
}
</script>

<style>

</style>