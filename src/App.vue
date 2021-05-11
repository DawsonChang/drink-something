<template>
    <div>
        <Modal 
            :openModal='openModal' 
            :modalDisplay='modalDisplay'
            :curOrder='curOrder'
            :modalMode='modalMode' 
            :handleCloseModal='handleCloseModal'
            :addOrder='addOrder'
            :editOrder='editOrder'
            :deleteOrder='deleteOrder'>
        </Modal>
        <div class='app'>
            <TitleSection 
                :sortOrder='sortOrder'
                :handleOpenModal='handleOpenModal'
                >
            </TitleSection>
            <List class='list'
                :displayOrders='displayOrders'
                :handleOpenModal='handleOpenModal'>
            </List>
        </div>
    </div>
</template>

<script>
import TitleSection from '@/components/TitleSection'
import List from '@/components/List'
import Modal from '@/components/Modal'

import orders from '@/data/orders.json'

import _ from 'lodash'

export default {
    name: 'App',
    components: {
        TitleSection,
        List,
        Modal
    },
    data() {
        // orders 是原本照 id 排列的順序; displayOrders 是顯示在螢幕的順序
        return {
            orders,
            displayOrders: [],
            openModal: false,
            modalDisplay: 'none',
            modalMode: '',
            curOrder: {}
        }
    },
    mounted() {
        this.displayOrders = _.cloneDeep(this.orders)
    },
    methods: {
        addOrder(newOrder) {
            let newId = 1
            // new order 的 id 為最後一個 order 的 id + 1
            if (this.orders.length != 0) {
                newId = this.orders[this.orders.length - 1].id + 1
            }
            newOrder.id = newId
            this.orders.push(newOrder)
            this.displayOrders = _.cloneDeep(this.orders)
            this.handleCloseModal()
        },
        editOrder(updateOrder) {
            const curId = updateOrder.id
            // 尋找欲編輯的id，如果找到就回傳 updateOrder，否則就是原本的 obj
            this.orders = this.orders.map(obj => 
                obj.id === curId ? {...updateOrder} : obj
            )
            this.displayOrders = _.cloneDeep(this.orders)
            this.handleCloseModal()
        },
        deleteOrder(deleteOrder) {
            const curId = deleteOrder.id
            this.orders = this.orders.filter(obj => {
                return obj.id != curId
            })
            this.displayOrders = _.cloneDeep(this.orders)
            this.handleCloseModal()
        },
        sortOrder (method) {
            switch(method) {
                case 'Original':
                    this.displayOrders = _.cloneDeep(this.orders)
                    break
                case 'By name (ascending)':
                    this.displayOrders.sort((a, b) => a.name.localeCompare(b.name, "zh-hant"))
                    break
                case 'By name (descending)':
                    this.displayOrders.sort((a, b) => b.name.localeCompare(a.name, "zh-hant"))
                    break
                case 'By price (ascending)':
                    this.displayOrders.sort((a, b) => a.price - b.price)
                    break
                case 'By price (descending)':
                    this.displayOrders.sort((a, b) => b.price - a.price)
                    break
            }
        },
        handleOpenModal(mode, curOrder) {
          this.openModal = true
          this.modalDisplay = 'block'
          this.modalMode = mode
          this.curOrder = curOrder
        },
        handleCloseModal() {
          this.openModal = false
          this.modalDisplay = 'none'
          this.modalMode = ''
          this.curOrder = {}
        }
    }

}
</script>

<style>

@import url('https://fonts.googleapis.com/css2?family=Noto+Sans+TC:wght@500&display=swap');
@import url('https://fonts.googleapis.com/css2?family=Open+Sans:wght@400;700&display=swap');

.app {
    width: 50%;
    position: absolute;
    left: 50%;
    transform: translate(-50%, 0);
    margin: 30px 0;
}

.list {
    margin-top: 30px;
}

</style>