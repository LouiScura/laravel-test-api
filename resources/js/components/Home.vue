<script setup>
import axios from 'axios';
import { onMounted, ref } from 'vue';
import CreateCategory from './CreateCategory.vue';

const categories = ref({})
const products = ref({})

const getCategories = async () => {
    await axios.get('/api/categories')
        .then(response => {
            categories.value = response.data.data
        })
        .catch((error) => console.log(error))
}

const getProducts = async () => {
    await axios.get('/api/products')
        .then(response => {
            products.value = response.data.data
        })
        .catch((error) => console.log(error))
}

onMounted(async () => {
    await getCategories();
    await getProducts();
});

</script>

<template>
    <h1>Testing API</h1>

    <div class="grid grid-cols-4 gap-4">
        <div class="space-y-2" v-for="product in products" :key="product.id">
<!--            <a href="#">-->
<!--                <img src="http://placehold.it/300x400" :alt="product.name" />-->
<!--            </a>-->
            <a class="text-slate-500 text-xl font-semibold hover:underline">
                {{ product.name }}
            </a>
            <p>${{ product.price }}</p>
            <p class="prose-slate">{{ product.description }}</p>
        </div>
    </div>
    <div>
        <h2>Create a category from Vue</h2>
        <create-category />
    </div>

</template>
