<script setup>
import { ref } from 'vue';
import Modal from '../components/Modal.vue';

const imageModal = ref(false);
const formModal = ref(false);
const videoModal = ref(false);
const fullscreenModal = ref(false);

// Form data
const formData = ref({
    name: '',
    email: '',
    message: ''
});

function submitForm() {
    alert(`Form submitted with: ${JSON.stringify(formData.value, null, 2)}`);
    formModal.value = false;
    // Reset form
    formData.value = {
        name: '',
        email: '',
        message: ''
    };
}
</script>

<template>
    <div class="container mt-4">
        <div class="buttons">
            <button class="button is-primary" @click="imageModal = true">
                <span class="icon"><i class="fas fa-image"></i></span>
                <span>Image Modal</span>
            </button>
            
            <button class="button is-info" @click="formModal = true">
                <span class="icon"><i class="fas fa-paper-plane"></i></span>
                <span>Contact Form Modal</span>
            </button>
            
            <button class="button is-success" @click="videoModal = true">
                <span class="icon"><i class="fas fa-video"></i></span>
                <span>Video Modal</span>
            </button>
            
            <button class="button is-warning" @click="fullscreenModal = true">
                <span class="icon"><i class="fas fa-expand"></i></span>
                <span>Fullscreen Modal</span>
            </button>
        </div>

        <!-- Image Modal -->
        <Modal 
            :active="imageModal" 
            @close="imageModal = false"
            title="Beautiful Nature"
            size="large"
            url="https://images.unsplash.com/photo-1682687220742-aba13b6e50ba"
        >
            <template #footer>
                <button class="button is-success" @click="imageModal = false">Done</button>
            </template>
        </Modal>

        <!-- Form Modal -->
        <Modal 
            :active="formModal" 
            @close="formModal = false"
            title="Contact Us"
            size="small"
        >
            <div class="field">
                <label class="label">Name</label>
                <div class="control">
                    <input class="input" type="text" v-model="formData.name" placeholder="Your name">
                </div>
            </div>

            <div class="field">
                <label class="label">Email</label>
                <div class="control">
                    <input class="input" type="email" v-model="formData.email" placeholder="Your email">
                </div>
            </div>

            <div class="field">
                <label class="label">Message</label>
                <div class="control">
                    <textarea class="textarea" v-model="formData.message" placeholder="Your message"></textarea>
                </div>
            </div>

            <template #footer>
                <button class="button is-success" @click="submitForm">Submit</button>
                <button class="button" @click="formModal = false">Cancel</button>
            </template>
        </Modal>

        <!-- Video Modal -->
        <Modal 
            :active="videoModal" 
            @close="videoModal = false"
            title="Sample Video"
            size="large"
        >
            <div class="video-container">
                <iframe 
                    width="100%" 
                    height="400" 
                    src="https://www.youtube.com/embed/dQw4w9WgXcQ" 
                    frameborder="0" 
                    allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" 
                    allowfullscreen
                ></iframe>
            </div>
            <template #footer>
                <button class="button is-info" @click="videoModal = false">Close</button>
            </template>
        </Modal>

        <!-- Fullscreen Modal -->
        <Modal 
            :active="fullscreenModal" 
            @close="fullscreenModal = false"
            title="Fullscreen Content"
            size="full"
        >
            <div class="content">
                <h1>Large Content Area</h1>
                <p>This modal is perfect for displaying large amounts of content or complex interfaces.</p>
                <div class="columns">
                    <div class="column">
                        <div class="box">
                            <h3>Section 1</h3>
                            <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Aenean efficitur sit amet massa fringilla egestas.</p>
                        </div>
                    </div>
                    <div class="column">
                        <div class="box">
                            <h3>Section 2</h3>
                            <p>Nullam vel sem. Nullam vel sem. Integer ante arcu, accumsan a, consectetuer eget, posuere ut, mauris.</p>
                        </div>
                    </div>
                    <div class="column">
                        <div class="box">
                            <h3>Section 3</h3>
                            <p>Sed cursus turpis vitae tortor. Sed aliquam ultrices mauris. Integer ante arcu, accumsan a.</p>
                        </div>
                    </div>
                </div>
            </div>
            <template #footer>
                <button class="button is-warning" @click="fullscreenModal = false">Close Fullscreen</button>
            </template>
        </Modal>
    </div>
</template>

<style scoped>
.video-container {
    position: relative;
    padding-bottom: 56.25%; /* 16:9 aspect ratio */
    height: 0;
    overflow: hidden;
}

.video-container iframe {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
}

.buttons {
    margin-bottom: 2rem;
}
</style>