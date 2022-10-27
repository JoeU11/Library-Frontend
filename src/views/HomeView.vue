<script>
import axios from "axios"

export default {
  data: function () {
    return {
      message: "Welcome to Vue.js!",
      books: [],
      searchTerm: ""
    };
  },
  created: function () {
    this.getBooks()
  },
  methods: {
    getBooks: function () {
      console.log("getting books")
      axios.get("http://localhost:3000/books.json").then(response => {
        console.log(response.data)
        this.books = response.data
      })
    },
    filterBooks() {
      return this.books.filter(recipe => {
        return recipe.title.includes(this.searchTerm);
      })
    },
    search() {
      console.log("searching")
      axios.get(`/books.json?search=${this.searchTerm}`).then(response => {
        console.log(response.data)
        this.books = response.data
      })

    }
  }
};
</script>

<template>
  <div class="home">

    <div class="Book-Search">
      <input type="text" v-model="searchTerm" />
      <button v-on:click="search()"> Search </button>
    </div>

    <div v-for="book in filterBooks()">
      <p>Title: {{ book.title }}<br />
        Author: {{ book.author.name }} <br />
        Genres:
      <p class="inline" v-for="category, index in book.categories">
      <p class="inline" v-if="index < book.categories.length - 1">{{ category.name }}, </p>
      <p class="inline" v-else>{{ category.name }}</p>
      </p>
      </p>
    </div>
  </div>
</template>

<style>
.inline {
  display: inline;
}
</style>