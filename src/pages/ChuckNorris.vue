<script setup>
import { ref, onMounted, onBeforeUnmount } from 'vue';

const joke = ref('Loading...');
let intervalId = null;

async function fetchNewJoke() {
    try {
        const response = await fetch('https://api.chucknorris.io/jokes/random');
        const data = await response.json();
        joke.value = data.value;
    } catch (error) {
        joke.value = 'Failed to load joke. Please try again.';
        console.error('Error fetching joke:', error);
    }
}

onMounted(() => {
    // Fetch initial joke
    fetchNewJoke();
    
    // Set up interval to fetch new joke every 10 seconds
    intervalId = setInterval(fetchNewJoke, 10000);
});

onBeforeUnmount(() => {
    // Clean up interval when component is unmounted
    if (intervalId) {
        clearInterval(intervalId);
    }
});
</script>

<template>
    <div class="container mt-4">
        <div class="box">
            <div class="content">
                <h2 class="title is-4">Chuck Norris Joke</h2>
                <p class="subtitle is-5">{{ joke }}</p>
                <button class="button is-primary" @click="fetchNewJoke">Get New Joke</button>
            </div>
        </div>
        <p class="help mt-2">Jokes automatically update every 10 seconds, or click the button for a new one</p>
    </div>
</template>

<style scoped>
.box {
    max-width: 600px;
    margin: 0 auto;
}
</style>