<script>
export default {
  name: 'FooterComponent',
}
</script>

<template>
  <footer class="app-footer py-3 text-center">
    <div class="container">
      <p class="mb-0">
        &copy; {{new Date().getFullYear()}}. All rights reserved.
      </p>
      <p>
        Made by Fadly M Irvan
      </p>
    </div>
  </footer>
</template>

<style scoped>
.app-footer{
  background-color: #f8f9fa;
  border-top: 1px solid #dee2e6;
  font-size: 0.9rem;
}
</style>