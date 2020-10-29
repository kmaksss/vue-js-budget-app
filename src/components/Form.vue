<template>
  <el-card class="form-card">
    <el-form :model="formData" :rules="rules" ref="addItemForm">
      <el-form-item label="Type" prop="type">
        <el-select v-model="formData.type" placeholder="choose type..." class="type-select">
          <el-option lable="Income" value="INCOME" />
          <el-option lable="Outcome" value="OUTCOME" />
        </el-select>
      </el-form-item>
      <el-form-item label="Comment" prop="comment">
        <el-input v-model="formData.comment" placeholder="your comment..."/>
      </el-form-item>
      <el-form-item label="Value" prop="value">
        <el-input v-model.number="formData.value" placeholder="your value"/>
      </el-form-item>
      <el-button type="primary" @click="onSubmit">Submit</el-button>
    </el-form>
  </el-card>
</template>

<script>
export default {
  name: 'Form',
  data: () => ({
    formData: {
      type: 'INCOME',
      comment: '',
      value: 0
    },
    rules: {
      comment: [
        {required: true, message: 'Please input comment', trigger: 'blur'}
      ],
      value: [
        {required: true, message: 'Please input value', trigger: 'blur'},
        {type: 'number', message: 'Value must be a number', trigger: 'blur'},
      ]
    },
  }),
  methods: {
    onSubmit() {
      this.$refs.addItemForm.validate((valid) => {
        if(valid) {
          this.$emit('submitForm', {...this.formData});
          this.$refs.addItemForm.resetFields();
        }
      })
    }
  }
}
</script>

<style scoped>
  .form-card {
    max-width: 500px;
    margin: auto;
  }

  .type-select {
    width: 100%;
  }
</style>