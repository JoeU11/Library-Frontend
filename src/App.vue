<template>
  <nav>
    <div style="display: flex;">
      <img src="./assets/pixel_book.png" class="nav-logo" alt="book logo" />
      <h1 style="padding-left: 5px;">Library App</h1>
    </div>
    <div style="display: flex;">
      <router-link to="/">Home</router-link>
      <router-link to="/about">About</router-link>
      <router-link to="/cart">Cart</router-link>
      <router-link to="/rented-books">Rented Books</router-link>
      <router-link to="/login">Login</router-link>
      <router-link to="/signup">Sign up</router-link>
      <router-link to="/logout">Logout</router-link>
    </div>
  </nav>
  <div id="main">
    <router-view />
  </div>
</template>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

nav {
  padding: 30px;
  background-color: lightgrey;
  display: flex;
  align-items: center;
  justify-content: space-between;
}

nav a {
  font-weight: bold;
  color: #2c3e50;
  display: flex;
  padding: 5px;

}

nav a.router-link-exact-active {
  color: #42b983;
}

#main {
  margin-left: 40px;
  margin-right: 40px;
  padding-top: 40px;
}

.nav-logo {
  width: 40px;
  padding-bottom: 7px;
}
</style>
