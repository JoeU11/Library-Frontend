<script>
import axios from 'axios';

export default {
  data: function () {
    return {
      message: "Your Cart",
      cartedItems: [],
      error: ""
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
    },
    checkout() {
      console.log("renting books")
      axios.post("/rentals", this.cartedItems).then(response => {
        console.log(response.data)
        this.$router.push("/rented-books")
      }).catch(error => {
        console.log(error.response.data)
        this.error = error.response.data.error
        document.querySelector("#error").showModal()
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
    <p v-if="cartedItems.length === 0">You don't have any books in your cart</p>
    <button v-else v-on:click="checkout()">Rent All</button>
  </div>

  <dialog id="error">
    <form method="dialog">
      {{ error }} <br />
      <button>OK</button>
    </form>
  </dialog>
</template>

<style>

</style>