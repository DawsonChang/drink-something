<template>
  <div class='card'>
    <div class='grid-item name'><div>{{ order.name }}</div></div>
    <div class='grid-item price'><div>${{ order.price }}</div></div>
    <div class='grid-item notes'><div>{{ order.notes }}</div></div>
    <div class='grid-item edit'>
        <div class='pencil-icon' @click='handleOpenModal("edit", order)'>
                <font-awesome-icon :icon="['fas', 'pencil-alt']" />
        </div>
    </div>
    <div class='grid-item delete'>
        <div class='trash-icon' @click='handleOpenModal("delete", order)'>
                <font-awesome-icon :icon="['fas', 'trash-alt']" />
        </div>
    </div>
  </div>
</template>

<script>
export default {
    name: 'Card',
    props: {
        order: Object,
        handleOpenModal: Function
    }

}
</script>

<style lang="scss" scoped>

.card {
    display: grid;
    grid-template-columns: repeat(6, 1fr);
    grid-template-rows: auto;
    grid-template-areas: "name name name name price edit"
                         "notes notes notes notes notes delete"; 
    border: 0.5px solid #becacf;
    border-right: none;
    border-left: none;
    // border-radius: 5px;
    font-family: 'Noto Sans TC', sans-serif;
}

.grid-item div {
  display: flex;
  font-size: 1.2rem;
  align-items: center;
  height: 100%;
}

.name {
  grid-area: name;
  padding: 5px 0 5px 10px;
  div {
      color: #285e75;
  }
}

.price {
  grid-area: price;
  padding: 5px 10px 5px 0;
  div {
      justify-content: flex-end;
      color: #4185a1;
  }
}

.notes {
  grid-area: notes;
  padding: 0 0 5px 10px;
  div {
      color: #478caa;
  }
}
.edit {
    background-color: #ebce7e;
    grid-area: edit;
    div {
      justify-content: center;
      color: white;
    }
}
.delete {
    background-color: #b3979f;
    grid-area: delete;
    div {
      justify-content: center;
      color: white;
    }
}

.pencil-icon:hover,
.pencil-icon:focus {
  opacity: 50%;
  text-decoration: none;
  cursor: pointer;
}
.trash-icon:hover,
.trash-icon:focus {
  opacity: 50%;
  text-decoration: none;
  cursor: pointer;
}

</style>