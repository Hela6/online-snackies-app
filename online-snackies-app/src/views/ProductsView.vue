<script setup>
import { ref, onMounted } from 'vue'

import Product from '../components/Product.vue'
import axios from 'axios'

const apiProductData = ref(null)
const apiFavProductData = ref(null)

// Cette fonctionnalité sert à savoir si un produit à été mis en favori, si c'est le cas : product.isLiked = true
// ensuite product.isLiked est défini comme props pour être utilisé dans le composant Product.vue
async function fetchData() {
    const userId = JSON.parse(localStorage.getItem("user")).id; // Retrieve user.id from local storage

    const allProducts = axios.get('http://localhost:8080/api/products') // requête GET pour récupérer tout les produits
    const favProducts = axios.get(`http://localhost:8080/api/products/favs?id_employee=${userId}`) // requête GET pour récupérer tout les produits FAVORIS

    await axios.all([allProducts, favProducts]) //  combine les deux requêtes GET dans un tableau d'appels à axios.

        .then(axios.spread(function (resAllProducts, resFavProducts) { // exécute une fonction lorsque les deux appels sont terminés avec succès. Les résultats des requêtes sont passés en tant que paramètres resAllProducts et resFavProducts.

            apiProductData.value = resAllProducts.data; // À l'intérieur de cette fonction, on met à jour les valeurs des références apiProductData et apiFavProductData avec les données reçues des requêtes.
            apiFavProductData.value = resFavProducts.data;

            apiProductData.value.forEach(product => { // On itère sur chaque produit de apiProductData.value en comparant son id avec celui de apiFavProductData.value.
                let matchingIndex = apiFavProductData.value.findIndex(fav => fav.id == product.id)
                if (matchingIndex != -1) {
                    product.isLiked = true // Si une correspondance est trouvée, on assigne la valeur true a product.isLiked 
                } else {
                    product.isLiked = false // si non false
                }
            })
        }))
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
        <Product v-for="item in apiProductData" :key="item.id" :id="item.id" :name="item.name" :price="item.price"
            :img="item.image_path" :quantity="item.quantity" :isLiked="item.isLiked">
            <!-- <= là is_liked est passé en props -->
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
    overflow: scroll;
}
</style>
