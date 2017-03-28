<template>
  <table>
    <tr><td>Salary</td><td>{{ yearlySalary }}</td><td>{{ yearlySalary / 12 }}</td></tr>
    <tr><td>30%</td><td>{{ thirtyPercent }}</td><td>{{ thirtyPercent / 12 }}</td></tr>
    <tr><td>Taxable Incomef</td><td>{{ taxableIncome }}</td><td>{{ taxableIncome / 12 }}</td></tr>
    <tr><td>Tax</td><td>{{ tax }}</td><td>{{ tax / 12 }}</td></tr>
    <tr><td>General Tax Credit</td><td>{{ generalCredit }}</td><td>{{ generalCredit / 12 }}</td></tr>
    <tr><td>Labour Tax Credit</td><td>{{ labourCredit }}</td><td>{{ labourCredit / 12 }}</td></tr>
    <tr><td>Net</td><td>{{ net }}</td><td>{{ net / 12 }}</td></tr>
  </table>
</template>

<script>

let taxBrackets = [
  {
    start: 0,
    length: 19981,
    percentage: 0.3655
  },
  {
    start: 19981,
    length: 33790 - 19981,
    percentage: 0.408
  },
  {
    start: 33790,
    length: 67071 - 33790,
    percentage: 0.408
  },
  {
    start: 67071,
    length: Infinity,
    percentage: 0.52
  }
]

export default {
  name: 'result-table',
  props: {
    yearlySalary: Number,
    thirtyPercentLimit: Number
  },
  computed: {
    tax: function () {
      let tax = 0
      for (let i = 0; i < taxBrackets.length; i++) {
        let bracket = taxBrackets[i]
        var amount = this.taxableIncome - bracket.start
        if (amount > 0) {
          tax += Math.min(amount, bracket.length) * bracket.percentage
        }
      }
      return tax
    },
    net: function () {
      return this.yearlySalary - this.tax + this.generalCredit + this.labourCredit
    },
    thirtyPercent: function () {
      if (this.thirtyPercentLimit === 0) {
        return 0
      }
      if (this.yearlySalary * 0.7 > this.thirtyPercentLimit) {
        return this.yearlySalary * 0.30
      } else if (this.yearlySalary > this.thirtyPercentLimit) {
        return this.yearlySalary - this.thirtyPercentLimit
      }
      return 0
    },
    taxableIncome: function () {
      return this.yearlySalary - this.thirtyPercent
    },
    generalCredit: function () {
      if (this.yearlySalary < 2254) {
        return this.yearlySalary
      }
      if (this.yearlySalary < 19982) {
        return 2254
      }
      if (this.yearlySalary < 66417) {
        return 2254 - (this.yearlySalary - 19982) * 4.787 / 100
      }
      return 0
    },
    labourCredit: function () {
      if (this.yearlySalary < 9309) {
        return 0.01772 * this.yearlySalary
      }
      if (this.yearlySalary < 19758) {
        return 165 + 0.28317 * (this.yearlySalary - 9309)
      }
      if (this.yearlySalary < 32444) {
        return 3223
      }
      if (this.yearlySalary < 111590) {
        return 3223 - (this.yearlySalary - 32444) * 0.036
      }

      return 0
    }
  }
}
</script>
