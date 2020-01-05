<template>
  <div>
    <label v-if="label">{{ label }}</label>
    <div>
      <slot></slot>
      <p v-if="validateStatus === 'error'">{{ errorMessage }}</p>
    </div>
  </div>
</template>

<script>
import schema from "async-validator";

export default {
  inject: ["form"],
  props: ["label", "prop"],
  data() {
    return {
      validateStatus: "",
      errorMessage: ""
    };
  },
  mounted() {
    if (this.prop) {
      this.$parent.$emit("addField", this);
    }
  },
  created() {
    this.$on("validate", this.validate);
  },
  methods: {
    validate() {
      return new Promise(resolve => {
        const descriptor = { [this.prop]: this.form.rules[this.prop] };
        const validator = new schema(descriptor);
        validator.validate(
          { [this.prop]: this.form.model[this.prop] },
          errors => {
            if (errors) {
              this.validateStatus = "error";
              this.errorMessage = errors[0].message;
              resolve(false);
            } else {
              this.validateStatus = "";
              this.errorMessage = "";
              resolve(true);
            }
          }
        );
      });
    }
  }
};
</script>

<style scoped></style>
