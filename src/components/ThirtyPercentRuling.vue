<template>
  <div class="thirtyPercent">
    <input type="checkbox" id="foreigner" v-model="foreigner"> <label for="foreigner">Foreign</label> <br/>
    <input type="checkbox" id="belowThirty" v-model="belowThirty"> <label for="belowThirty">Below 30</label> <br/>
    <input type="checkbox" id="masterDegree" v-model="masterDegree"> <label for="masterDegree">Masters degree</label> <br/>
    {{ thirtyPercentLimit }}
  </div>
</template>

<script>

export default {
  name: 'thirty-percent-ruling',
  data () {
    return {
      foreigner: false,
      belowThirty: false,
      masterDegree: false
    }
  },
  computed: {
    thirtyPercentLimit: function () {
      let limit = 0
      if (this.foreigner) {
        if (this.belowThirty && this.masterDegree) {
          // Emit the number value through the input event
          limit = 28125
        } else {
          limit = 37000
        }
      }

      this.$emit('change', limit)
      return limit
    }
  }
}
</script>
