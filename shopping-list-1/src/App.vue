<template>
  <div class="container">
    <input v-model="input" type="text" />
    <button @click="addItem()">Add to list</button>

    <h2>Items:</h2>
    <ul>
      <li v-for="item in validItems" :key="`item-${item.id}`">
        <span @click="deleteItem(item)" style="margin-right: 15px">X</span>
        {{ item.text }}
      </li>
    </ul>

    <h2>Deleted Items:</h2>
    <ul>
      <li v-for="item in deletedItems" :key="`item-${item.id}`">
        {{ item.text }}
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  data() {
    return {
      input: "",
      list: [],
    };
  },

  methods: {
    //method for add item to li
    addItem() {
      //ush the value to the array
      this.list.push({
        id: this.list.length + 1,
        text: this.input,
        is_deleted: false,
      });
      //reset the input field
      this.input = "";
    },
    //for deleting item in list and array
    deleteItem(item) {
      item.is_deleted = true;
    },
  },

  computed: {
    validItems() {
      return this.list.filter((item) => !item.is_deleted);
    },

    deletedItems() {
      return this.list.filter((item) => item.is_deleted);
    },
  },
};
</script>

<style scoped>
.container {
  border: 1px solid black;
  max-width: 900px;
  margin: 0 auto;
  text-align: center;
}
</style>
