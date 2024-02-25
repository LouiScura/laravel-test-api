<template>
    <form @submit.prevent="submitForm">
        <div>
            <label for="name">Name:</label>
            <input id="name" v-model="formData.name" type="text" required>
        </div>
        <div>
            <label for="description">Description:</label>
            <textarea id="description" v-model="formData.description" required></textarea>
        </div>
        <div>
            <label for="photo">Photo:</label>
            <input id="photo" type="file" @change="handleFileUpload" required>
        </div>
        <button type="submit">Submit</button>
    </form>
</template>

<script setup>
import { ref } from 'vue';
import axios from 'axios';

const formData = ref({
    name: '',
    description: '',
    photo: null
});

function handleFileUpload(event) {
    formData.value.photo = event.target.files[0];
}

async function submitForm() {
    const formPayload = new FormData();
    formPayload.append('name', formData.value.name);
    formPayload.append('description', formData.value.description);

    if (formData.value.photo) {
        formPayload.append('photo', formData.value.photo);
    }

    try {
        const response = await axios.post('/api/categories', formPayload, {
            headers: {
                'Content-Type': 'multipart/form-data'
            }
        });
        console.log('Form submitted:', response.data);
        // Handle successful form submission (e.g., show a message or clear the form)
    } catch (error) {
        console.error('Form submission error:', error);
        // Handle errors (e.g., show error messages)
    }
}
</script>
