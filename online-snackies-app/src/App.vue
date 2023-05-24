<script setup>
import { RouterLink } from 'vue-router'
</script>


<template>
  <header>
    <div><img src="" alt=""></div>
    <div>
      <p></p>
    </div>
  </header>

  <main>
    <RouterView></RouterView>
  </main>

  <footer>
    <nav>
      <RouterLink to="/"><img class='links' src="../public/img/home_page.png" alt=""></RouterLink>
      <RouterLink to="/favs"><img class='links' src="../public/img/favs.png" alt=""></RouterLink>
      <RouterLink to="/contact"><img class='links' src="../public/img/contact_us.png" alt=""></RouterLink>
    </nav>
  </footer>
</template>


<style scoped>
header {
  height: 67.5px;
  width: 100%;
  background-color: #212529;
  border-bottom: 1px solid #A282CD;
}

main {
  background-color: #19181B;
  height: 676.5px;
  display: flex;
  flex-direction: column;
  padding: 10px;
}

nav {
  width: 100%;
  display: flex;
  box-sizing: border-box;
  justify-content: space-evenly;
  flex-direction: row;
  align-items: center;
  margin: 0 auto;
  padding: 30px;
  position: sticky;
  bottom: 0;
  z-index: 100;
  background-color: #212529;
  height: 56px;
  border-top: 1px solid #A282CD;
}

.links {
  width: 35px;
}
</style>
