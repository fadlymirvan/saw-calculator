<script>
export default {
  name: "InputControls",
  props: {
    numAlternatives: {
      type: Number,
      required: true
    },
    numCriteria: {
      type: Number,
      required: true
    }
  },

  data() {
    return {
      localNumAlternatives: this.numAlternatives,
      localNumCriteria: this.numCriteria
    }
  },

  methods: {
    updateAlternatives(value) {
      this.localNumAlternatives = parseInt(value) || 1;
    },

    updateCriteria(value) {
      this.localNumCriteria = parseInt(value) || 1;
    },

    handleGenerateTable() {
      this.$emit('update:numAlternatives', this.localNumAlternatives);
      this.$emit('update:numCriteria', this.localNumCriteria);
      this.$emit('generate-table');
    }
  }
};
</script>

<template>
  <div class="row g-3 align-items-end mb-4">
    <div class="col-md-3">
      <label class="form-label">Number of Alternatives:</label>
      <input
          type="number"
          :value="localNumAlternatives"
          @input="updateAlternatives($event.target.value)"
          min="1"
          class="form-control"
      >
    </div>
    <div class="col-md-3">
      <label class="form-label">Number of Criteria:</label>
      <input
          type="number"
          :value="localNumCriteria"
          @input="updateCriteria($event.target.value)"
          min="1"
          class="form-control"
      >
    </div>
    <div class="col-md-3">
      <button @click="handleGenerateTable" class="btn btn-primary w-100">Generate Table</button>
    </div>
    <div class="col-md-3">
      <button @click="$emit('clear-all')" class="btn btn-secondary w-100">Clear All</button>
    </div>
  </div>
</template>

<style scoped>
.row > .col-md-3 {
  padding: 0 8px;
}
</style>
