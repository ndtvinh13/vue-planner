<template>
  <nav class="main-nav">
    <router-link :to="{ name: 'Home' }">Projects</router-link>
    <router-link :to="{ name: 'AddProject' }">Add a new project</router-link>
  </nav>
</template>

<script>
export default {};
</script>

<style>
.main-nav {
  text-align: center;
  margin: 30px auto;
}

.main-nav a {
  display: inline-block;
  text-decoration: none;
  margin: 0 20px;
  font-size: 20px;
  color: #35495e;
  transition: 0.2s;
}

.main-nav a:hover {
  color: #6185aa;
}

.router-link-active {
  border-bottom: 2px solid #42b883;
  padding-bottom: 5px;
}
</style>
