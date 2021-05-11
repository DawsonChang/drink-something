<template>
  <div>
    <div v-for="order in displayOrders" :key='order.id'>
        <Card :order='order' 
              :firstOrderId='displayOrders.length === 0 ? 0 : displayOrders[0].id' 
              :handleOpenModal='handleOpenModal' />
    </div>
  </div>
</template>

<script>
import Card from '@/components/Card'

export default {
    name: 'List',
    components: {
        Card
    },
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

</style>