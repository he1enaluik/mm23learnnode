<script setup>
const props = defineProps({
    active: Boolean,
    url: String,
    title: {
        type: String,
        default: ''
    },
    size: {
        type: String,
        default: 'default',
        validator: (value) => ['small', 'default', 'large', 'full'].includes(value)
    }
});

defineEmits(['close']);
</script>
<template>
    <div class="modal" :class="{ 'is-active': active }">
        <div class="modal-background" @click="$emit('close')"></div>
        <div class="modal-card" :class="{ 
            'is-small': size === 'small',
            'is-large': size === 'large',
            'is-full': size === 'full'
        }">
            <header v-if="title" class="modal-card-head">
                <p class="modal-card-title">{{ title }}</p>
                <button class="delete" aria-label="close" @click="$emit('close')"></button>
            </header>
            
            <section class="modal-card-body">
            <slot>
                    <figure v-if="url" class="image">
                        <img :src="url" alt="Modal content">
                    </figure>
            </slot>
            </section>

            <footer v-if="$slots.footer" class="modal-card-foot">
                <slot name="footer"></slot>
            </footer>
        </div>
    </div>
</template> 

<style scoped>
.modal-card.is-small {
    max-width: 400px;
}

.modal-card.is-large {
    width: 800px;
}

.modal-card.is-full {
    width: 95vw;
    height: 95vh;
}

.modal-card.is-full .modal-card-body {
    height: calc(100% - 120px);
    overflow-y: auto;
}

.image img {
    width: 100%;
    height: auto;
    object-fit: cover;
}

/* Fade transition */
.modal {
    transition: opacity 0.3s ease;
}

.modal:not(.is-active) {
    opacity: 0;
    pointer-events: none;
}
</style> 