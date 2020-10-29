<template>
  <div class="budget-list-wrap">
    <el-card class="box-card" :header="elCardHeader">
      <template v-if="!isEmpty">
        <div class="list-item" v-for="(item, index) in list" :key="index">
          <BudgetListItem :item="item" @deleteItem="deleteItem"/>
        </div>
      </template>
      <el-alert v-else type="info" :title="emptyTitle" :closable="false"></el-alert>
    </el-card>
  </div>
</template>

<script>
import BudgetListItem from './BudgetListItem';

export default {
  name: 'BudgetList',
  components: {
    BudgetListItem
  },
  data: () => ({
    elCardHeader: 'Budget list',
    emptyTitle: 'Empty list',
  }),
  props: {
    list: {
      type: Object,
      default: () => ({}),
    },
  },
  computed: {
    isEmpty() {
      return !Object.keys(this.list).length;
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
  .budget-list-wrap {
    max-width: 500px;
    margin: auto;
  }
  .list-item {
    display: flex;
    padding: 5px 0;
    align-items: center;
  }

</style>