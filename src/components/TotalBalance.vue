<template>
  <div class="total-value">
    <span :style="getBallanceStatus">
      Balance {{ total }}
    </span>
  </div>
</template>

<script>
export default {
  name: 'TotalBalance',
  props: {
    total: {
      type: Number,
      default: 0
    }
  },
  data: () => ({
    ballanceStatus: 'color: red'
  }),
  computed: {
    getBallanceStatus() {
      if(this.total > 0) {
        return 'color: green'
      } else if(this.total < 0) {
        return 'color: red'
      } else {
        return 'color: black'
      }
    },
  }
}
</script>

<style scoped>
  .total-value {
    font-size: 26px;
    text-align: center;
    padding: 20px;
    text-transform: uppercase;
  }
</style>