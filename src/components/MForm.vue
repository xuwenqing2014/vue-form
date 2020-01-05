<template>
  <form>
    <slot></slot>
  </form>
</template>

<script>
export default {
  provide() {
    return { form: this };
  },
  props: {
    model: {
      type: Object,
      required: true
    },
    rules: {
      type: Object
    }
  },
  data() {
    return {
      fields: []
    };
  },
  created() {
    this.fields = [];
    this.$on("addField", item => this.fields.push(item));
  },
  methods: {
    async validate(callback) {
      const tasks = this.fields.map(item => item.validate());
      const result = await Promise.all(tasks);
      let ret = true;
      result.forEach(item => {
        if (!item) {
          ret = false;
        }
      });
      if (ret) {
        callback(true);
      } else {
        callback(false);
      }
    }
  }
};
</script>

<style scoped></style>
