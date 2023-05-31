<script setup>
import { ref, onMounted } from 'vue'

import Fav from '../components/Fav.vue'
import axios from 'axios'

const apiData = ref(null)

async function fetchData() {
    axios
        .get('http://localhost:8080/api/fav')
        .then(response => {
            apiData.value = response.data;
        })
        .catch(error => {
            console.error('Error fetching data:', error);
        });
}

onMounted(() => {
    fetchData();
})


</script>

<template>
    <div class="search-container">
        <form action="">
            <input type="text" placeholder="entrer le nom d'un produit . . ." name="search">
        </form>
    </div>

    <section>
        <Fav v-for="item in apiData" :key="item.id" :id="item.id" :name="item.name" :price="item.price"
            :img="item.image_path" :quantity="item.quantity">
        </Fav>
    </section>
</template>

<style scoped>
* {
    border-radius: 10px;
    font-weight: bold;
    font-family: Nunito, sans-serif;
}

input {
    width: 335px;
    height: 36px;
    margin: 10px;
    padding: 10px;
    border: none;
}

section {
    margin: 0px 10px 0px 10px;

}
</style>