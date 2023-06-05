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
  isLiked: Boolean
})


const isFav = ref(props.isLiked);

const toggleHeart = async () => {
  if (!isFav.value) {
    addToFavs();
    isFav.value = true;
  } else {
    removeFromFavs();
    isFav.value = false;
  }
};


const userId = JSON.parse(localStorage.getItem("user"))?.id;

async function addToFavs() {
  try {
    const response = await fetch(`http://localhost:8080/api/products/addToFavs?id_product=${props.id}&id_employee=${userId}`);
    if (!response.ok) {
      throw new Error("Failed to add product to favs");
    }

  } catch (error) {
    console.log(error);
  }
}

async function removeFromFavs() {
  try {
    const response = await fetch(`http://localhost:8080/api/products/removeFromFavs?id_product=${props.id}&id_employee=${userId}`);
    if (!response.ok) {
      throw new Error("Failed to remove product from favs");
    }
  } catch (error) {
    console.log(error)
  }
}

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
      <img class="fav" :src="!isFav ? emptyHeartImage : filledHeartImage" alt="" @click="toggleHeart" />
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