<script>
export default {
  name: "DataTableComponent",
  props: {
    title: {
      type: String,
      required: true
    },
    rowHeader: {
      type: String,
      required: true
    },
    columnPrefix: {
      type: String,
      required: true
    },
    rowPrefix: {
      type: String,
      required: true
    },
    numColumns: {
      type: Number,
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
            <th>{{ rowHeader }}</th>
            <th v-for="n in numColumns" :key="'col-'+n">
              {{ columnPrefix }} {{ n }}
            </th>
          </tr>
          </thead>
          <tbody>
          <tr v-for="(row, rowIndex) in data" :key="'row-'+rowIndex">
            <td>{{ rowPrefix }} {{ rowIndex + 1 }}</td>
            <td v-for="(value, colIndex) in row.values" :key="'col-'+rowIndex+'-'+colIndex">
              <input
                  type="number"
                  :value="value"
                  @input="$emit('update-value', { rowIndex, colIndex, value: +$event.target.value })"
                  class="form-control form-control-sm"
              />
            </td>
          </tr>
          </tbody>
        </table>
      </div>
      <div class="d-flex gap-2 mt-3">
        <button @click="$emit('add-row')" class="btn btn-secondary">Add Row</button>
        <button @click="$emit('remove-row')" class="btn btn-secondary">Remove Row</button>
      </div>
    </div>
  </div>
</template>
