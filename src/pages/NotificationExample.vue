<script setup>
import { ref } from 'vue';
import Notification from '../components/Notification.vue';
import Btn from '../components/Btn.vue';

const notifications = ref([
    { 
        id: 1, 
        content: 'Primary notification example', 
        isVisible: true,
        props: { color: 'primary', size: 'normal' }
    },
    { 
        id: 2, 
        content: 'Link notification with light theme', 
        isVisible: true,
        props: { color: 'link', light: true }
    },
    { 
        id: 3, 
        content: 'Large info notification with outline', 
        isVisible: true,
        props: { color: 'info', size: 'large', outlined: true }
    },
    { 
        id: 4, 
        content: 'Success notification with auto-close', 
        isVisible: true,
        props: { color: 'success', autoClose: 5000 }
    },
    { 
        id: 5, 
        content: 'Small warning notification', 
        isVisible: true,
        props: { color: 'warning', size: 'small' }
    },
    { 
        id: 6, 
        content: 'Loading danger notification (not closable)', 
        isVisible: true,
        props: { color: 'danger', state: 'loading', closable: false }
    }
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

function addNotification() {
    const colors = ['primary', 'link', 'info', 'success', 'warning', 'danger'];
    const sizes = ['small', 'normal', 'medium', 'large'];
    const randomColor = colors[Math.floor(Math.random() * colors.length)];
    const randomSize = sizes[Math.floor(Math.random() * sizes.length)];
    
    notifications.value.push({
        id: Date.now(),
        content: `New ${randomSize} ${randomColor} notification at ${new Date().toLocaleTimeString()}`,
        isVisible: true,
        props: {
            color: randomColor,
            size: randomSize,
            autoClose: 3000,
            light: Math.random() > 0.5,
            outlined: Math.random() > 0.5
        }
    });
}
</script>

<template>
    <div class="container mt-4">
        <div class="buttons mb-4">
            <Btn color="info" @click="resetNotifications">Reset All Notifications</Btn>
            <Btn color="success" @click="addNotification">Add Random Notification</Btn>
        </div>
        
        <div v-for="notification in notifications" :key="notification.id" v-show="notification.isVisible">
            <Notification
                v-bind="notification.props"
                @close="closeNotification(notification.id)"
            >
                {{ notification.content }}
            </Notification>
        </div>
    </div>
</template>

<style scoped>
.buttons {
    margin-bottom: 1rem;
}
</style>