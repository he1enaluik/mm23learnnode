<script setup>
import { ref } from 'vue';

const notifications = ref([
    { id: 1, type: 'is-primary', message: 'Primary notification example', isVisible: true },
    { id: 2, type: 'is-link', message: 'Link notification example', isVisible: true },
    { id: 3, type: 'is-info', message: 'Info notification example', isVisible: true },
    { id: 4, type: 'is-success', message: 'Success notification example', isVisible: true },
    { id: 5, type: 'is-warning', message: 'Warning notification example', isVisible: true },
    { id: 6, type: 'is-danger', message: 'Danger notification example', isVisible: true }
]);

function closeNotification(id) {
    const notification = notifications.value.find(n => n.id === id);
    if (notification) {
        notification.isVisible = false;
    }
}

function resetNotifications() {
    notifications.value.forEach(n => n.isVisible = true);
}
</script>

<template>
    <div class="container mt-4">
        <button class="button is-info mb-4" @click="resetNotifications">Reset All Notifications</button>
        
        <div v-for="notification in notifications" :key="notification.id" v-show="notification.isVisible">
            <div class="notification" :class="notification.type">
                <button class="delete" @click="closeNotification(notification.id)"></button>
                {{ notification.message }}
            </div>
        </div>
    </div>
</template>

<style scoped>
.notification {
    margin-bottom: 1rem;
}
</style>