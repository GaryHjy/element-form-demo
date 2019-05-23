<template>
  <div class="home">
    <h-form ref="kForm" :model="ruleForm" :rules="rules">
      <h-form-item label="账户" prop="userName">
        <h-input v-model="ruleForm.userName"></h-input>
      </h-form-item>
      <h-form-item label="密码" prop="password">
        <h-input type="password" v-model="ruleForm.password"></h-input>
      </h-form-item>
      <h-form-item>
        <el-button type="primary" @click="submitForm('kForm')"
          >立即创建</el-button
        >
      </h-form-item>
    </h-form>

    <el-form
      :model="ruleForm"
      :rules="rules"
      ref="ruleForm"
      label-width="100px"
      style="margin-top:150px"
    >
      <el-form-item label="账户" prop="userName">
        <el-input v-model="ruleForm.userName"></el-input>
      </el-form-item>
      <el-form-item label="密码" prop="password">
        <el-input type="password" v-model="ruleForm.password"></el-input>
      </el-form-item>
      <el-form-item>
        <el-button type="primary" @click="submitForm('ruleForm')"
          >立即创建</el-button
        >
        <el-button @click="resetForm('ruleForm')">重置</el-button>
      </el-form-item>
    </el-form>
  </div>
</template>

<script>
import HForm from "@/components/h-form";
import HFormItem from "@/components/h-form-item";
import HInput from "@/components/h-input";

export default {
  components: {
    HForm,
    HFormItem,
    HInput
  },
  data() {
    return {
      ruleForm: {
        userName: "",
        password: ""
      },
      rules: {
        userName: [
          { required: true, message: "请输入用户名", trigger: "blur" }
        ],
        password: [{ required: true, message: "请输入密码", trigger: "blur" }]
      }
    };
  },
  methods: {
    submitForm(formName) {
      this.$refs[formName].validate(valid => {
        if (valid) {
          alert("submit!");
        } else {
          console.log("error submit!!");
          return false;
        }
      });
    },
    resetForm(formName) {
      this.$refs[formName].resetFields();
    }
  }
};
</script>
