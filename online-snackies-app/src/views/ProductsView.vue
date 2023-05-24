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

    <article v-for="item in apiData" :key="item.id">
        <div>
            <img :src="item.image_path" alt="">
        </div>
        <div>
            <h3>{{ item.name }}</h3>
            <p> prix : {{ item.price }} crédit(s)</p>
            <button>acheter</button>
        </div>
        <div>
            <img src="" alt="">
        </div>

    </article>
</template>

<style scoped>
input {
    width: 335px;
    height: 36px;
    border-radius: 10px;
}

article {
    display: flex;
    flex-direction: row;
    padding: 10px;
    font-family: Nunito, sans-serif;
}

img {
    border-radius: 10px;
    margin-right: 10px;
}

button {
    border-radius: 10px;
    background-color: #A282CD;

}
</style>
