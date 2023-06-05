<script setup>

import axios from 'axios';
import { ref } from 'vue'

const email = ref("")
const password = ref("")

const submitForm = async (event) => {
    event.preventDefault(); // Prevent default form submission behavior

    try {
        const response = await axios.post('http://localhost:8080/api/auth', { "email": email.value, "password": password.value });
        console.log(response.data)

        localStorage.setItem("user", JSON.stringify(response.data))
        window.location.href = '/';
    } catch (error) {
        console.error(error); // Handle error
    }
};


</script>


<template>
    <div>
        <form @submit="submitForm" class="form">
            <div>
                <input type="email" name="email" placeholder="email" v-model="email">
            </div>
            <div>
                <input type="password" name="password" placeholder="mot de passe" v-model="password">
            </div>
            <div>
                <button type="submit">se connecter</button>
            </div>
        </form>
        <pre id="log"></pre>
    </div>
</template>

<style scoped>
* {
    border-radius: 10px;
    font-weight: bold;
    font-family: Nunito, sans-serif;
}

.form {
    display: flex;
    flex-direction: column;
    align-items: center;
    margin-top: 30px;
}

input {
    width: 300px;
    height: 36px;
    margin: 10px;
    padding: 10px;
    border: none;
}

button {
    width: 95px;
    height: 30px;
    background-color: #A282CD;
    border: none;
    margin-top: 15px;
}

button,
p {
    font-size: 12px;
}
</style>