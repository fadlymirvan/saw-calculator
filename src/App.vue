<script>
import SawCalculator from "@/components/SawCalculator.vue";
import FooterComponent from "@/components/FooterComponent.vue";

export default {
  name: 'App',
  components: {
    FooterComponent,
    SawCalculator,
  }
}
</script>

<template>
  <div class="app d-flex flex-column vh-100">
    <header>
      <!-- Place Holder for future header -->
    </header>

    <main class="content">
      <SawCalculator />
    </main>

    <FooterComponent />
  </div>
</template>

<style>
.app {
  display: flex;
  flex-direction: column;
  min-height: 100vh;
}
</style>
