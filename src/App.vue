<template>
  <div id="app">
    <TotalBalance :total="totalBalance"/>
    <BudgetList :list="list" @deleteItem="onDeleteItem"/>
    <Form @submitForm="onFormSubmit"/>
  </div>
</template>

<script>

import BudgetList from './components/BudgetList';
import TotalBalance from './components/TotalBalance';
import Form from './components/Form';

export default {
  name: 'App',
  components: {
    BudgetList,
    TotalBalance,
    Form
  },
  data: () => ({
    list: {
      1: {
        type: 'INCOME',
        value: 100,
        comment: 'Some comment',
        id: 1,
      },
      2: {
        type: 'OUTCOME',
        value: -50,
        comment: 'Some out comment',
        id: 2,
      }
    }
  }),
  computed: {
    totalBalance() {
      return Object.values(this.list).reduce((acc, item) => acc + item.value, 0)
    }
  },
  methods: {
    onDeleteItem(id) {
      const confirmDelete = confirm('Вы действительно хотите удалить эту запись?');
      if(!confirmDelete) return;
      this.$delete(this.list, id)
    },
    onFormSubmit(data) {
      const newObj = {
        ...data,
        id: String(Math.random())
      };
      this.$set(this.list, newObj.id, newObj)
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
