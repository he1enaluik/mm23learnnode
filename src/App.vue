<script setup>
import 'bootstrap/dist/css/bootstrap.min.css';
import '@fortawesome/fontawesome-free/css/all.min.css';
import Tabs from './components/Tabs.vue';
import Footer from './components/Footer.vue';
import { RouterView } from 'vue-router';
</script>

<template>
    <div class="app">
        <Tabs />
        <main class="container">
            <RouterView />
        </main>
        <Footer />
    </div>
</template>

<style>
.app {
    min-height: 100vh;
    display: flex;
    flex-direction: column;
}
.container {
    padding: 1rem;
    flex: 1;
}
</style>