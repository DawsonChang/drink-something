<template>
<div>
    <!-- The Modal -->
    <div id="myModal" class="modal" :style='{ display: modalDisplay }' v-if='openModal'>

        <!-- Modal content -->
        <div class="modal-content">
            <div class="modal-header">
                <span class="close" @click='handleCloseModal'>&times;</span>
                <h3>{{ modalMode }}</h3>
            </div>
            <!-- ADD mode -->
            <div class="modal-body" v-if='modalMode=="add"'>
                <div class="input">
                    <div style="padding-right: 5px">Name: </div>
                    <div>
                        <input v-model="newOrderObject.name" placeholder="name">
                    </div>
                </div>
                <div class="input">
                    <div style="padding-right: 10px">Price: </div>
                    <div>
                        <input v-model="newOrderObject.price" placeholder="price" type='number'>
                    </div>
                </div>
                <div class="input">
                    <div style="padding-right: 10px">Notes: </div>
                    <div>
                        <textarea v-model="newOrderObject.notes" placeholder="notes"></textarea>
                    </div>
                </div>
                <div class='btn'>
                    <button @click='addOrder(newOrderObject)' >OK</button>
                </div>
            </div>
            <!-- EDIT mode -->
            <div class="modal-body" v-else-if='modalMode=="edit"'>
                <div class="input">
                    <div style="padding-right: 5px">Name: </div>
                    <div>
                        <input v-model="newOrderObject.name" placeholder="name">
                    </div>
                </div>
                <div class="input">
                    <div style="padding-right: 10px">Price: </div>
                    <div>
                        <input v-model="newOrderObject.price" placeholder="price" type='number'>
                    </div>
                </div>
                <div class="input">
                    <div style="padding-right: 10px">Notes: </div>
                    <div>
                        <textarea v-model="newOrderObject.notes" placeholder="notes"></textarea>
                    </div>
                </div>
                <div class='btn'>
                    <button @click='editOrder(newOrderObject)' >OK</button>
                </div>
            </div>
            <!-- Delete mode -->
            <div class="modal-body" v-else-if='modalMode=="delete"'>
                <div style="text-align: center; padding-top: 10px;">
                    <p>Are you sure to delete this order?</p>
                </div>
                <div class='btn'>
                    <button @click='deleteOrder(newOrderObject)'>Yes</button>
                </div>
            </div>
        </div>
    </div>
    </div>
</template>

<script>
import _ from 'lodash'

export default {
    name: 'Modal',
    props: {
      openModal: Boolean,
      modalDisplay: String,
      curOrder: Object,
      modalMode: String,
      handleCloseModal: Function,
      addOrder: Function,
      editOrder: Function,
      deleteOrder: Function
  },
  data() {
    return {
        newOrderObject: {
            id: 0,
            name: '',
            price: null,
            notes: ''
        }

    }
  },
  mounted() {
    // 改成 arraw function 則下面可以直接使用 this.closeModal()
    window.onclick = event => {
        if (event.target.id == 'myModal') {
            this.handleCloseModal()
        }
    }
  },
  watch: {
      modalMode: function(newVal) {
          if (newVal === 'edit' || newVal === 'delete') {
            this.newOrderObject = _.cloneDeep(this.curOrder)
          }
          else if (newVal === 'add') {
              this.newOrderObject = {
                id: 0,
                name: '',
                price: null,
                notes: ''
            }
          }
      }
  }
}
</script>

<style>
.modal {
  display: none; /* Hidden by default */
  position: fixed; /* Stay in place */
  z-index: 1; /* Sit on top */
  padding-top: 100px; /* Location of the box */
  left: 0;
  top: 0;
  width: 100%; /* Full width */
  height: 100%; /* Full height */
  overflow: auto; /* Enable scroll if needed */
  background-color: rgb(0,0,0); /* Fallback color */
  background-color: rgba(0,0,0,0.4); /* Black w/ opacity */
}

/* Modal Content */
.modal-content {
  position: relative;
  background-color: #fefefe;
  margin: auto;
  padding: 0;
  border: 1px solid #888;
  width: 60%;
  box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2),0 6px 20px 0 rgba(0,0,0,0.19);
}

@media only screen and (max-width: 600px) {
    .modal-content {
        width: 90%;
    }
}

/* The Close Button */
.close {
  color: white;
  float: right;
  font-size: 28px;
  font-weight: bold;
}

.close:hover,
.close:focus {
  color: #000;
  text-decoration: none;
  cursor: pointer;
}

.modal-header {
  padding: 1px 16px;
  background-color: #5cb85c;
  color: white;
}

.modal-body {
    padding: 2px 16px;
}

.input {
    display: flex;
    justify-content: center;
    padding-top: 20px;
}

.btn {
    text-align: center;
    padding: 15px 0;
}

</style>