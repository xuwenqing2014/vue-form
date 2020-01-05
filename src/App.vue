<template>
  <div id="app">
    <m-form :model="ruleForm" :rules="rules" ref="loginForm">
      <form-item label="用户名" prop="name">
        <m-input v-model="ruleForm.name"></m-input>
      </form-item>
      <form-item label="密码" prop="password">
        <m-input v-model="ruleForm.password" type="password"></m-input>
      </form-item>
      <form-item>
        <button @click="submit">提交</button>
      </form-item>
    </m-form>
    {{ ruleForm }}
  </div>
</template>

<script>
import MInput from "./components/MInput.vue";
import FormItem from "./components/FormItem.vue";
import MForm from "./components/MForm.vue";

export default {
  name: "app",
  components: {
    MInput,
    FormItem,
    MForm
  },
  data() {
    return {
      ruleForm: {
        name: "",
        password: ""
      },
      rules: {
        name: [
          { required: true, message: "请输入用户名" },
          { min: 6, max: 10, message: "用户名的长度在6-10" }
        ],
        password: [{ required: true, message: "请输入密码" }]
      }
    };
  },
  methods: {
    submit(e) {
      e.preventDefault();
      this.$refs.loginForm.validate(valid => {
        console.log(valid);
      });
    }
  }
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
