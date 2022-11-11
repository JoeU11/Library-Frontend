<script>
import axios from 'axios';

export default {
  data: function () {
    return {
      message: "Your Current Rentals",
      cartedItems: []
    };
  },
  created: function () {
    this.getItems()
  },
  methods: {
    getItems() {
      console.log("carting item")
      axios.get("/rented_books.json", { params: { rented: true } }).then(response => {
        console.log(response.data)
        this.cartedItems = response.data
      })
    },
    humanReadableTime: function (parsedTime) {
      var hour = parsedTime[4].slice(0, -3).split(':')[0]
      var time = ""
      if (hour > 12) {
        time = `${hour - 12}:${parsedTime[4].slice(0, -3).split(':')[1]} PM`
      }
      else if (hour == 12) {
        time = `${hour}:${parsedTime[4].slice(0, -3)} PM`
      }
      else {
        if (hour[0] === '0') { hour = hour.slice(1) }
        time = `${hour}:${parsedTime[4].slice(0, -3).split(':')[1]} AM`
      }
      return `${parsedTime[0]}, ${parsedTime[1]} ${parsedTime[2]} ${time} ${parsedTime[6]} ${parsedTime[7]} ${parsedTime[8]}`
    }
  },
};
</script>

<template>
  <div class="home">
    <h1>{{ message }}</h1>
    <div v-for="item, index in cartedItems">
      <h2>{{ item.book.title }}</h2>
      <p>Due: {{ humanReadableTime(new Date(item.due_date).toString().split(' ')) }}</p>
    </div>
  </div>
</template>

<style>

</style>