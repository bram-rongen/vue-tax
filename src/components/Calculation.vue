<template>
  <div class="calculation">
    <input v-model.number="income" type="number" step="1" placeholder="">
    <input type="checkbox" v-model="monthly" name="monthly"> <label for="monthly">Montly</label>
    <thirty-percent-ruling :value="thirtyPercentLimit"
  @change="value => { thirtyPercentLimit = value }"></thirty-percent-ruling>

    <result-table :yearly-salary="yearlySalary" :thirty-percent-limit="thirtyPercentLimit"></result-table>
  </div>
</template>

<script>

import ResultTable from './ResultTable'
import thirtyPercentRuling from './thirtyPercentRuling'

export default {
  name: 'calculation',
  data () {
    return {
      income: 36000,
      monthly: false,
      thirtyPercentLimit: 0
    }
  },
  computed: {
    yearlySalary: function () {
      let multi = 1
      if (this.monthly) {
        multi = 12
      }
      return this.income * multi
    }
  },
  components: {
    ResultTable,
    thirtyPercentRuling
  }
}
</script>
