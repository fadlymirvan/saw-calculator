<script>
export default {
  name: "CalculateButton",
  emits: ["calculate"],
  methods: {
    onCalculate() {
      this.$emit("calculate");
    }
  }
};
</script>

<template>
  <button @click="onCalculate" class="btn btn-primary calculate-btn">
    Calculate
  </button>
</template>

<style scoped>
.calculate-btn {
  width: 100%;
}
</style>
