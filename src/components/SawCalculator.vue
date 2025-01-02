<script>
import HeaderComponent from "@/components/SAW/HeaderComponent.vue";
import InputControls from "@/components/SAW/InputControls.vue";
import DataTableComponent from "@/components/SAW/DataTableComponent.vue";
import CriterionDetailComponent from "@/components/SAW/CriterionDetailComponent.vue";
import ResultComponent from "@/components/SAW/ResultComponent.vue";
import CalculateButton from "@/components/SAW/CalculateButton.vue";

export default {
  name: "SawCalculator",
  components: {
    HeaderComponent,
    InputControls,
    DataTableComponent,
    CriterionDetailComponent,
    ResultComponent,
    CalculateButton,
  },

  data() {
    return {
      localNumAlternatives: 3,
      localNumCriteria: 3,
      alternatives: [],
      criteria: [],
      results: [],
      weightedScores: [],
      showTables: false,
      showResults: false,
    };
  },

  computed: {
    normalizedWeights() {
      const totalWeight = this.criteria.reduce((sum, crit) => sum + Number(crit.weight), 0);
      return this.criteria.map(crit => Number(crit.weight) / totalWeight);
    },
  },

  methods: {
    handleInputUpdate(type, value) {
      const parsedValue = parseInt(value, 10);
      if (!isNaN(parsedValue) && parsedValue >= 1) {
        this[`localNum${type}`] = parsedValue;
      }
    },

    updateAlternativeValue({ rowIndex, colIndex, value }) {
      const parsedValue = parseFloat(value);
      this.alternatives[rowIndex].values[colIndex] = !isNaN(parsedValue) ? parsedValue : 0;
    },

    updateCriterion({ index, field, value }) {
      this.criteria[index][field] = value;
    },

    handleAddRow() {
      this.alternatives.push({
        values: Array(this.localNumCriteria).fill(0),
      });
    },

    handleRemoveRow() {
      if (this.alternatives.length > 1) {
        this.alternatives.pop();
      }
    },

    generateTable() {
      this.alternatives = Array.from({ length: this.localNumAlternatives }, () => ({
        values: Array(this.localNumCriteria).fill(0),
      }));

      this.criteria = Array.from({ length: this.localNumCriteria }, () => ({
        type: "benefit",
        weight: 0,
      }));

      this.showTables = true;
      this.showResults = false;
    },

    clearAll() {
      this.alternatives = [];
      this.criteria = [];
      this.results = [];
      this.weightedScores = [];
      this.showTables = false;
      this.showResults = false;
      this.localNumAlternatives = 1;
      this.localNumCriteria = 1;
    },

    calculateNormalizedScore(value, maxValue, minValue, criterionType) {
      return criterionType === 'benefit'
          ? value / maxValue
          : minValue / value;
    },

    calculate() {
      const matrix = this.alternatives.map(alt => alt.values.map(Number));

      const maxValues = matrix.reduce((max, row) => {
        row.forEach((val, j) => {
          max[j] = Math.max(max[j], val);
        });
        return max;
      }, Array(this.localNumCriteria).fill(0));

      const minValues = matrix.reduce((min, row) => {
        row.forEach((val, j) => {
          min[j] = Math.min(min[j], val);
        });
        return min;
      }, Array(this.localNumCriteria).fill(Infinity));

      this.weightedScores = matrix.map(row => ({
        scores: row.map((val, j) => {
          const normalized = this.calculateNormalizedScore(
              val,
              maxValues[j],
              minValues[j],
              this.criteria[j].type
          );
          return normalized * this.normalizedWeights[j];
        })
      }));

      this.results = this.weightedScores.map(row =>
          row.scores.reduce((sum, score) => sum + score, 0)
      );

      this.showResults = true;
    },
  },
};
</script>

<template>
  <div class="saw-calculator container py-4">
    <HeaderComponent />

    <InputControls
        :numAlternatives="localNumAlternatives"
        :numCriteria="localNumCriteria"
        @update:numAlternatives="handleInputUpdate('Alternatives', $event)"
        @update:numCriteria="handleInputUpdate('Criteria', $event)"
        @generate-table="generateTable"
        @clear-all="clearAll"
    />

    <template v-if="showTables">
      <DataTableComponent
          title="Data Input Table"
          rowHeader="Alternative"
          columnPrefix="Criterion"
          rowPrefix="Alt"
          :numColumns="localNumCriteria"
          :data="alternatives"
          @add-row="handleAddRow"
          @remove-row="handleRemoveRow"
          @update-value="updateAlternativeValue"
      />

      <CriterionDetailComponent
          title="Criterion Details"
          :data="criteria"
          @update-criterion="updateCriterion"
      />

      <CalculateButton @calculate="calculate" />
    </template>

    <ResultComponent
        v-if="showResults"
        :results="results"
        :weightedScores="weightedScores"
        :numCriteria="localNumCriteria"
    />
  </div>
</template>

<style scoped>
.saw-calculator {
  max-width: 1200px;
  margin: 0 auto;
}
</style>
