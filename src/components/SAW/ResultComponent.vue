<script>
export default {
  name: "ResultComponent",
  props: {
    results: {
      type: Array,
      required: true
    },
    weightedScores: {
      type: Array,
      required: true
    },
    numCriteria: {
      type: Number,
      required: true
    }
  },
  computed: {
    rowColors() {
      const minResult = Math.min(...this.results);
      const maxResult = Math.max(...this.results);

      return this.results.map(result => {
        const percentage = (result - minResult) / (maxResult - minResult);
        const colorValue = Math.floor(255 * (1 - percentage));
        return `rgba(${colorValue}, ${255 - colorValue}, 0, 0.5)`;
      });
    }
  }
};
</script>

<template>
  <div>
    <!-- Calculation Results -->
    <div class="card mb-4 mt-4">
      <div class="card-body">
        <h2 class="h5 mb-3">Calculation Results</h2>
        <div class="table-responsive">
          <table class="table table-bordered">
            <thead>
            <tr>
              <th>Alternative</th>
              <th>Total Score</th>
            </tr>
            </thead>
            <tbody>
            <tr v-for="(result, index) in results" :key="'result-'+index">
              <td :style="{ backgroundColor: rowColors[index] }">Alt {{ index + 1 }}</td>
              <td :style="{ backgroundColor: rowColors[index] }">{{ result.toFixed(4) }}</td>
            </tr>
            </tbody>
          </table>
        </div>
      </div>
    </div>

    <!-- Final Weighted Scores -->
    <div class="card">
      <div class="card-body">
        <h2 class="h5 mb-3">Final Weighted Scores</h2>
        <div class="table-responsive">
          <table class="table table-bordered">
            <thead>
            <tr>
              <th>Alternative</th>
              <th v-for="(criterion, index) in numCriteria" :key="'weighted-criterion-'+index">
                Criterion {{ index + 1 }}
              </th>
              <th>Total Score</th>
            </tr>
            </thead>
            <tbody>
            <tr v-for="(alt, index) in weightedScores" :key="'weighted-row-'+index">
              <td :style="{ backgroundColor: rowColors[index] }">Alt {{ index + 1 }}</td>
              <td v-for="(score, colIndex) in alt.scores" :key="'weighted-score-'+index+'-'+colIndex" :style="{ backgroundColor: rowColors[index] }">
                {{ score.toFixed(4) }}
              </td>
              <td :style="{ backgroundColor: rowColors[index] }">{{ results[index].toFixed(4) }}</td>
            </tr>
            </tbody>
          </table>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.table-responsive {
  margin-top: 1rem;
}
</style>
