<script>
import HeaderComponent from "@/components/SAW/HeaderComponent.vue";

export default {
  name: 'SawCalculator',
  components: {HeaderComponent},
  props: {},
  methods: {},
  data() {}
}
</script>

<template>
  <div class="saw-calculator container py-4">
    <HeaderComponent />
  </div>
</template>

<style scoped>
.saw-calculator {
  max-width: 1200px;
}
</style>