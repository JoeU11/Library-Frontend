<script>
import axios from "axios"

export default {
  data: function () {
    return {
      message: "Welcome to Vue.js!",
      books: []
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
    }
  }
};
</script>

<template>
  <div class="home">
    <h1>{{ message }}</h1>
    <div v-for="book in books">
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