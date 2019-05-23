<template>
  <div class="h-form">
    <slot></slot>
  </div>
</template>

<script>
export default {
  name: "HForm",
  componentName: "HForm",
  provide() {
    return {
      HForm: this
    };
  },
  props: {
    model: {
      type: Object,
      default() {
        return {};
      }
    },
    rules: {
      type: Object,
      default() {
        return {};
      }
    }
  },
  methods: {
    async validate(callback) {
      const tasks = this.$children
        .filter(item => item.prop)
        .map(item => item.validate());
      const results = await Promise.all(tasks);
      if (results.some(valid => !valid)) {
        callback(false);
      } else {
        callback(true);
      }
    }
  }
};
</script>
