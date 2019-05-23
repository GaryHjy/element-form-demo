<template>
  <div class="h-input">
    <input v-bind="$attrs" :type="type" :value="value" @input="handleInput" />
  </div>
</template>

<script>
export default {
  name: "HInput",
  componentName: "HInput",
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
    return {};
  },
  methods: {
    handleInput(e) {
      let value = e.target.value;
      this.$emit("input", value);
      this.$parent.$emit("validate");
    }
  }
};
</script>
