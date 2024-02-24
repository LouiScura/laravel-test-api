<template>
    <form @submit.prevent="submit">
        <label for="name">Name:</label>
        <input id="name" v-model="name" type="text" placeholder="Enter category name">
        <button type="submit">Submit</button>
    </form>
</template>

<script setup>
import axios from 'axios';
import { ref } from 'vue';

const name = ref('')

const submit = () => {

    axios.post('/api/categories', {
        name: name.value
    })
        .then(response => {
            console.log('New Category ID: ' + response.data.data.id)
        })
}
</script>
