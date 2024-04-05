<template>
  <div class="container">
    <h1>Your Shopping list</h1>
    <input v-model="input" type="text" placeholder="What you want to add" />
    <button @click="addItem()">Add to list</button>

    <h2>Items to buy:</h2>
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
      //define the input and list array
      input: "",
      list: [],
    };
  },

  methods: {
    //method for add item to li
    addItem() {
      //push the value to the array if the input have something in it
      if (this.input.length > 0) {
        this.list.push({
          id: this.list.length + 1,
          text: this.input,
          is_deleted: false,
        });
      }
      //reset the input field
      this.input = "";
    },
    //method for deleting item in list and array
    // pass the current items of array list to the function and after deleting change the boolean value to true
    deleteItem(item) {
      item.is_deleted = true;
    },
  },

  computed: {
    //filter method for filter the items in array if they have a false value in is_deleted
    validItems() {
      return this.list.filter((item) => !item.is_deleted);
    },
    //filter method for filter the items in array if they have a true (was deleted) value in is_deleted
    deletedItems() {
      return this.list.filter((item) => item.is_deleted);
    },
  },
};
</script>
