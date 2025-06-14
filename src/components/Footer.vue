<template>
  <footer class="bg-dark text-white py-5">
    <div class="container">
      <div class="row justify-content-center text-center">
        <div class="col-lg-8">
          <h2 class="display-4 mb-4">Let's work together on your next project</h2>
          <p class="lead mb-4 text-light">
            Lorem ipsum dolor sit amet, consectetur adipiscing elit. Ut elit tellus, luctus nec ullamcorper mattis, pulvinar dapibus leo.
          </p>
          <button class="btn btn-primary btn-lg mb-5">Learn More</button>
          
          <div class="social-links mb-4">
            <a href="#" class="text-white mx-3 text-decoration-none fs-4">
              <i class="fab fa-facebook"></i>
            </a>
            <a href="#" class="text-white mx-3 text-decoration-none fs-4">
              <i class="fab fa-twitter"></i>
            </a>
            <a href="#" class="text-white mx-3 text-decoration-none fs-4">
              <i class="fab fa-instagram"></i>
            </a>
          </div>
          
          <p class="text-muted small">Copyright {{ currentYear }} – Neve FSE theme</p>
        </div>
      </div>
    </div>
  </footer>
</template>

<script>
export default {
  name: 'Footer',
  computed: {
    currentYear() {
      return new Date().getFullYear();
    }
  }
}
</script>

<style scoped>
.social-links a:hover {
  color: var(--bs-primary) !important;
  transition: color 0.3s;
}
</style> 