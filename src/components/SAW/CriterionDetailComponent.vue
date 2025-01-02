<script>
export default {
  name: "CriterionDetailComponent",
  props: {
    title: {
      type: String,
      required: true
    },
    data: {
      type: Array,
      required: true
    }
  }
};
</script>

<template>
  <div class="card mb-4">
    <div class="card-body">
      <h2 class="h5 mb-3">{{ title }}</h2>
      <div class="table-responsive">
        <table class="table table-bordered">
          <thead>
          <tr>
            <th>Criterion</th>
            <th>Type</th>
            <th>Weight (%)</th>
          </tr>
          </thead>
          <tbody>
          <tr v-for="(criterion, index) in data" :key="'criterion-'+index">
            <td>Criterion {{ index + 1 }}</td>
            <td>
              <select
                  v-model="criterion.type"
                  @change="$emit('update-criterion', { index, field: 'type', value: criterion.type })"
                  class="form-select form-select-sm"
              >
                <option value="benefit">Benefit</option>
                <option value="cost">Cost</option>
              </select>
            </td>
            <td>
              <input
                  type="number"
                  v-model="criterion.weight"
                  min="0"
                  max="100"
                  @input="$emit('update-criterion', { index, field: 'weight', value: +criterion.weight })"
                  class="form-control form-control-sm"
              />
            </td>
          </tr>
          </tbody>
        </table>
      </div>
    </div>
  </div>
</template>
