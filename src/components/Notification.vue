<!-- A reusable notification component that can be used anywhere in the application -->
<script setup>
import { computed } from 'vue';

const props = defineProps({
    color: {
        type: String,
        required: false,
        validator(value) {
            return [
                'primary',
                'link',
                'info',
                'success',
                'warning',
                'danger',
                'white',
                'light',
                'dark'
            ].includes(value);
        }
    },
    light: {
        type: Boolean,
        required: false,
    },
    size: {
        type: String,
        required: false,
        validator(value) {
            return [
                'small',
                'normal',
                'medium',
                'large'
            ].includes(value);
        }
    },
    autoClose: {
        type: Number,
        default: 0
    },
    closable: {
        type: Boolean,
        default: true
    },
    outlined: {
        type: Boolean,
        required: false,
    },
    state: {
        type: String,
        required: false,
        validator(value) {
            return [
                'active',
                'loading'
            ].includes(value);
        }
    }
});

const emit = defineEmits(['close']);

// If autoClose is set, close the notification after the specified time
if (props.autoClose > 0) {
    setTimeout(() => {
        emit('close');
    }, props.autoClose);
}

const classNames = computed(() => {
    const names = ['notification'];
    
    if (props.color) {
        names.push('is-' + props.color);
    }
    if (props.light) {
        names.push('is-light');
    }
    if (props.size) {
        names.push('is-' + props.size);
    }
    if (props.outlined) {
        names.push('is-outlined');
    }
    if (props.state) {
        names.push('is-' + props.state);
    }
    
    return names.join(' ');
});
</script>

<template>
    <div :class="classNames">
        <button v-if="closable" class="delete" @click="$emit('close')"></button>
        <slot></slot>
    </div>
</template>

<style scoped>
.notification {
    margin-bottom: 1rem;
    animation: fadeIn 0.3s ease-in;
}

@keyframes fadeIn {
    from {
        opacity: 0;
        transform: translateY(-10px);
    }
    to {
        opacity: 1;
        transform: translateY(0);
    }
}

/* Size modifiers */
.notification.is-small {
    padding: 0.75rem;
    font-size: 0.875rem;
}

.notification.is-medium {
    padding: 1.5rem;
    font-size: 1.25rem;
}

.notification.is-large {
    padding: 2rem;
    font-size: 1.5rem;
}

/* Loading state */
.notification.is-loading {
    position: relative;
    pointer-events: none;
    opacity: 0.8;
}

.notification.is-loading::after {
    content: "";
    position: absolute;
    top: calc(50% - 0.5em);
    left: calc(50% - 0.5em);
    width: 1em;
    height: 1em;
    border: 2px solid transparent;
    border-radius: 50%;
    border-top-color: currentColor;
    border-left-color: currentColor;
    animation: spinAround 500ms infinite linear;
}

@keyframes spinAround {
    from { transform: rotate(0deg); }
    to { transform: rotate(359deg); }
}
</style> 