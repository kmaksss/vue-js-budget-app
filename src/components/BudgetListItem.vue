<template>
  <div class="budget-list-item">
    <span class="budget-comment">{{ item.comment }}</span>
    <span class="budget-value">{{ item.value }}</span>
    <el-button type="danger" size="mini" @click="deleteItem(item.id)">Delete</el-button>
  </div>
</template>

<script>
export default {
  name: 'BudgetListItem',
  props: {
    item: {
      type: Object,
      default: () => ({}),
    },
  },
  methods: {
    deleteItem(id) {
      this.$emit('deleteItem', id)
    }
  }

}
</script>

<style scoped>
  .budget-value {
    font-weight: bold;
    margin-left: auto;
    margin-right: 20px;
  }
  .budget-list-item {
    width: 100%;
    display: flex;
    justify-content: space-between;
  }
</style>