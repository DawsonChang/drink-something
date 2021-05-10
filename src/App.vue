<template>
    <div>
        <TitleSection :sortOrder='sortOrder'></TitleSection>
        <List :orders='orders' :deleteOrder='deleteOrder'></List>
    </div>
</template>

<script>
import TitleSection from '@/components/TitleSection'
import List from '@/components/List'

import orders from '@/data/orders.json'

export default {
    name: 'App',
    components: {
        TitleSection,
        List
    },
    data() {
        return {
            orders
        }
    },
    methods: {
        // addOrder(newOrder) {
        //     this.orders.push(newOrder)
        // },
        // editOrder(curId, updateOrder) {
        //     this.orders.filter(obj => {
        //         if (obj.id === curId) {
        //             const { name, price, notes } = updateOrder
        //             obj = {...obj, name, price, notes}
        //         }
        //     })
        // },
        deleteOrder(curId) {
            this.orders = this.orders.filter(obj => {
                return obj.id != curId
            })

        },
        sortOrder (method) {
            switch(method) {
                case 'Original':
                    this.orders.sort((a, b) => a.id > b.id ? 1 : -1)
                    break
                case 'By name (ascending)':
                    this.orders.sort((a, b) => a.name.localeCompare(b.name, "zh-hant"))
                    break
                case 'By name (descending)':
                    this.orders.sort((a, b) => b.name.localeCompare(a.name, "zh-hant"))
                    break
                case 'By price (ascending)':
                    this.orders.sort((a, b) => a.price > b.price ? 1 : -1)
                    break
                case 'By price (descending)':
                    this.orders.sort((a, b) => a.price < b.price ? 1 : -1)
                    break
            }
        }
    }

}
</script>

<style>

</style>