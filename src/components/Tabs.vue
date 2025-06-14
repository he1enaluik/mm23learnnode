<script setup>
import { useRoute, useRouter } from 'vue-router';
const route = useRoute();
const router = useRouter();
</script>

<template>
    <nav class="navbar is-primary">
        <div class="navbar-menu">
            <div class="navbar-start">
                <RouterLink 
                    v-for="r in router.getRoutes()" 
                    :key="r.path"
                    :to="r.path"
                    class="navbar-item"
                    :class="{ 'is-active': route.path === r.path }"
                >
                    {{ r.name }}
                </RouterLink>
            </div>
        </div>
    </nav>
</template>

<style scoped>
.navbar-item.is-active {
    background-color: rgba(0, 0, 0, 0.1);
    font-weight: bold;
}
</style>