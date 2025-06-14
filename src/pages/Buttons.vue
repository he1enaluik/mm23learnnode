<script setup>
import { ref } from 'vue';
import Btn from '../components/Btn.vue';

const isLoading = ref(false);

function toggleLoading() {
    isLoading.value = !isLoading.value;
    if (isLoading.value) {
        setTimeout(() => {
            isLoading.value = false;
        }, 2000);
    }
}
</script>
<template>
    <div class="container mt-4">
        <div class="buttons">
            <Btn color="primary" dark size="large" rounded :state="isLoading ? 'loading' : ''" @click="toggleLoading">
                Toggle Loading
            </Btn>
            
            <Btn color="info" size="medium">Normal Button</Btn>
            
            <Btn color="success" outlined>Outlined Button</Btn>
            
            <Btn color="warning" light>Light Button</Btn>
            
            <Btn color="danger" inverted>Inverted Button</Btn>
        </div>
        
        <div class="mt-4">
            <p class="help">Click the first button to see loading state (auto-resets after 2 seconds)</p>
        </div>
    </div>
</template>