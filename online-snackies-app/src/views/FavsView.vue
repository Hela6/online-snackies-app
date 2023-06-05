<script setup>

import { ref, onMounted } from 'vue'
import Product from '../components/Product.vue'
import axios from 'axios'

// On récupère les favoris avec l'endpoint adapté
const apiFavsProductData = ref(null)

async function fetchFavsData() {

    const userId = JSON.parse(localStorage.getItem("user")).id; // Retrieve user.id from local storage
    axios
        .get(`http://localhost:8080/api/products/favs?id_employee=${userId}`)
        .then(response => {
            apiFavsProductData.value = response.data;
            apiFavsProductData.value.forEach(product => {
                product.isLiked = true;
            })
        })
        .catch(error => {
            console.error('Error fetching data:', error);
        });
}

onMounted(() => {
    fetchFavsData();
})

</script>

<template>
    <div class="search-container">
        <form action="">
            <input type="text" placeholder="entrer le nom d'un produit . . ." name="search">
        </form>
    </div>

    <section>
        <Product v-for="item in apiFavsProductData" :key="item.id" :id="item.id" :name="item.name" :price="item.price"
            :img="item.image_path" :quantity="item.quantity" :isLiked="item.isLiked">
        </Product>
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