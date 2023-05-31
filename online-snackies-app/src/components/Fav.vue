<script setup>

import { ref, defineProps } from 'vue';
import emptyHeartImage from "@/assets/img/empty_heart.png";
import filledHeartImage from "@/assets/img/filled_heart.png";

const props = defineProps({
  name: String,
  price: String,
  img: String,
  id: String,
  quantity: String,
})

const isFilled = ref(false);

const toggleHeart = () => {
  isFilled.value = !isFilled.value;
};

async function decrementProductQuantity() {
  try {
    // Make the API request to decrement the product's quantity
    const response = await fetch(`http://localhost:8080/api/product/consume?id=${props.id}`, {
      method: 'GET',
      // Add any necessary headers or authentication tokens
    });

    if (response.ok) {
      // Update the local product quantity variable

    } else {
      // Handle any errors or display an error message
    }
  } catch (error) {
    console.log(error)
    // Handle any network or other errors
  }
}


</script>


<template>
  <article>

    <div>
      <img :src="img" alt="">
    </div>
    <div class="product_info">
      <h3>{{ name }}</h3>
      <p> prix : {{ price }} crédit(s)</p>
      <button @click="decrementProductQuantity">
        {{ props.quantity <= '0' ? 'manquant' : 'acheter' }} </button>
    </div>
    <div>
      <img class="fav" :src="isFilled ? filledHeartImage : emptyHeartImage" alt="" @click="toggleHeart" />
      <!-- lorsque le user clique pour enlever le fav de sa liste, mettre à jour la base de données avec une nouvelle route API-->
    </div>
  </article>
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

article {
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  padding: 7.5px;
}

.product_info {
  display: flex;
  flex-direction: column;
  justify-content: space-evenly;
  margin-right: 50px;
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

.fav {
  width: 28px;
  margin: 5px 5px auto auto;
}
</style>