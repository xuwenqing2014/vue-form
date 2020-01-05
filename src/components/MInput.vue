<template>
  <input v-model="inputValue" :type="type" />
</template>

<script>
export default {
  props: {
    value: {
      type: String,
      default: ""
    },
    type: {
      type: String,
      default: "text"
    }
  },
  data() {
    return {
      inputValue: this.value
    };
  },
  watch: {
    inputValue(newValue) {
      this.$emit("input", newValue);
      this.$parent.$emit("validate");
    }
  }
};
</script>

<style scoped></style>
