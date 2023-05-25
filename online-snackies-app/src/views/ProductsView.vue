<script>

import axios from 'axios';
export default {
    data() {
        return {
            apiData: null,
        };
    },
    mounted() {
        this.fetchData();
    },
    methods: {
        fetchData() {
            axios
                .get('http://localhost:8080/api/products') // Replace with your API endpoint URL
                .then(response => {
                    this.apiData = response.data;
                    // Handle the retrieved data as needed
                })
                .catch(error => {
                    console.error('Error fetching data:', error);
                    // Handle the error appropriately
                });
        },
    },
};
</script>

<template>
    <div class="search-container">
        <form action="">
            <input type="text" placeholder="entrer le nom d'un produit . . ." name="search">
        </form>
    </div>

    <section>
        <article v-for="item in apiData" :key="item.id">
            <div>
                <img :src="item.image_path" alt="">
            </div>
            <div class="product_info">
                <h3>{{ item.name }}</h3>
                <p> prix : {{ item.price }} crédit(s)</p>
                <button>acheter</button>
            </div>
            <div>
                <img src="" alt="">
            </div>
        </article>
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
    background-color: #212529;
    margin: 0px 10px 0px 10px;
}

article {
    display: flex;
    flex-direction: row;
    padding: 7.5px;
}

img {
    margin-right: 10px;
}

.product_info {
    display: flex;
    flex-direction: column;
    justify-content: space-evenly;
}

button {
    width: 95px;
    height: 25px;
    background-color: #A282CD;
    border: none;
}

button,
p {
    font-size: 12px;
}
</style>
