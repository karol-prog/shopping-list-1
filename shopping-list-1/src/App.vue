<template>
  <div class="container">
    <h1>Your Shopping list</h1>
    <input v-model="input" type="text" placeholder="What you want to add" />
    <button @click="addItem()">Add to list</button>

    <h2>Items to buy:</h2>
    <ul>
      <li v-for="item in validItems" :key="item.id">
        <span @click="deleteItem(item)">X</span>
        {{ item.text }}
      </li>
    </ul>

    <h2>Deleted Items:</h2>
    <ul>
      <li v-for="item in deletedItems" :key="item.id">
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
      items: [],
    };
  },

  methods: {
    //method for add item to list
    addItem() {
      //push the value to the array if the input have something in it
      if (this.input.length > 0) {
        this.items.push({
          id: this.items.length + 1,
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
      return this.items.filter((item) => !item.is_deleted);
    },
    //filter method for filter the items in array if they have a true (was deleted) value in is_deleted
    deletedItems() {
      return this.items.filter((item) => item.is_deleted);
    },
  },
};
</script>
