<script>
import axios from "axios"

export default {
  data: function () {
    return {
      message: "Welcome to Vue.js!",
      books: [],
      searchTerm: "",
      myCart: {},

    };
  },
  created: function () {
    this.getBooks()
  },
  methods: {
    getBooks: function () {
      console.log("getting books")
      axios.get("/books.json").then(response => {
        console.log(response.data)
        this.books = response.data
      })
    },
    showBooks() {
      return this.books.filter(book => {
        var lowerSearchTerm = this.searchTerm.toLowerCase();
        var lowerBookTitle = book.title.toLowerCase();
        return lowerBookTitle.includes(lowerSearchTerm);
      })
    },
    addBookToCart(book) {
      console.log(book)
      console.log("add book to cart")
      var params = {
        book_id: book
      }
      axios.post("/rented_books.json", params).then(response => {
        console.log(response.data)
        this.myCart = response.data
        this.$router.push("/cart")
      })
    }
  }
};
</script>

<template>
  <div class="home">

    <div class="Book-Search">
      Search:<input type="text" v-model="searchTerm" />

    </div>

    <div v-for="book in showBooks()">
      <p>Title: {{ book.title }}<br />
        Author: {{ book.author.name }} <br />

        Genres:
      <p class="inline" v-for="category, index in book.categories">
      <p class="inline" v-if="index < book.categories.length - 1">{{ category.name }}, </p>
      <p class="inline" v-else>{{ category.name }}</p>

      </p>
      </p>
      <button v-on:click="addBookToCart(book.id)">Add to cart</button>
    </div>
  </div>
</template>

<style>
.inline {
  display: inline;
}
</style>