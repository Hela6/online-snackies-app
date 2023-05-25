<script setup>
import { RouterLink } from 'vue-router'
</script>


<template>
  <header>
    <div class="block_logo">
      <div><img class='img_logo' src="../public/img/donut_logo.png" alt=""></div>
      <p class="text_logo">ONLINE SNACKIES</p>
    </div>

    <div>
      <p>Nom Prénom</p>
      <p>($ credits)</p>
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
.block_logo,
header,
main,
nav {
  display: flex;
}

nav,
header {
  width: 100%;
  background-color: #212529;
  flex-direction: row;
  color: #A282CD;
}

header {
  height: 67.5px;
  border-bottom: 1px solid #A282CD;
  justify-content: space-between;
  padding: 15px;
}

.img_logo {
  width: 38px;
}

.text_logo {
  width: 123px;
  font-size: 16px;
  font-family: Chango, sans-serif;
  text-align: center;
  font-weight: 16px;
}

p {
  font-family: Nunito, sans-serif;
}

main {
  background-color: #19181B;
  height: 676.5px;
  flex-direction: column;
}

nav {
  justify-content: space-evenly;
  align-items: center;
  bottom: 0;
  height: 56px;
  border-top: 1px solid #A282CD;
}

.links {
  width: 30px;
}
</style>
