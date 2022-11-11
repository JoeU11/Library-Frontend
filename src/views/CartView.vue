<script>
import axios from 'axios';

export default {
  data: function () {
    return {
      message: "Your Cart",
      cartedItems: []
    };
  },
  created: function () {
    this.getItems()
  },
  methods: {
    getItems() {
      console.log("carting item")
      axios.get("/rented_books.json", { params: { cart: true } }).then(response => {
        console.log(response.data)
        this.cartedItems = response.data
      })
    },
    removeItem(item, index) {
      console.log("removing item")
      console.log(item)
      axios.delete(`/rented_books/${item.id}`).then(response => {
        console.log(response.data)
        this.cartedItems.splice(index, 1)
      })
    }
  },
};
</script>

<template>
  <div class="home">
    <h1>{{ message }}</h1>
    <div v-for="item, index in cartedItems"> {{ item.book.title }}

      <button v-on:click="removeItem(item, index)"> Remove from Cart </button>
    </div>
  </div>
</template>

<style>

</style>