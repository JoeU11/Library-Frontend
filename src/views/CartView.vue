<script>
import axios from 'axios';

export default {
  data: function () {
    return {
      message: "Welcome to Vue.js!",
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
    removeItem(item) {
      console.log("removing item")
      console.log(item)
      axios.delete(`/rented_books/ ${item}.json`).then(response => {
        console.log(response.data)
        this.$router.go()
      })
    }
  },
};
</script>

<template>
  <div class="home">
    <h1>{{ message }}</h1>
    <div v-for="item in cartedItems"> {{ item.book.title }}

      <button v-on:click="removeItem(item.carted_item_id)"> Remove from Cart </button>
    </div>
  </div>
</template>

<style>

</style>