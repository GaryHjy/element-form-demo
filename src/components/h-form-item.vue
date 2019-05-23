<template>
  <div class="h-form-item">
    <label v-if="label">
      {{ label }}
    </label>
    <slot></slot>
    <p v-if="validateMessage">{{ validateMessage }}</p>
  </div>
</template>

<script>
import AsyncValidator from "async-validator";

export default {
  name: "HFormItem",
  componentName: "HFormItem",
  provide() {
    return {
      HFormItem: this
    };
  },
  inject: ["HForm"],
  props: {
    label: String,
    prop: String
  },
  data() {
    return {
      validateMessage: ""
    };
  },
  created() {
    this.$on("validate", this.validate);
  },
  methods: {
    validate() {
      return new Promise(resolve => {
        const descriptor = { [this.prop]: this.HForm.rules[this.prop] };

        const validator = new AsyncValidator(descriptor);

        validator.validate(
          { [this.prop]: this.HForm.model[this.prop] },
          errors => {
            if (errors) {
              this.validateMessage = errors[0].message;
              resolve(false);
            } else {
              this.validateMessage = "";
              resolve(true);
            }
          }
        );
      });
    }
  }
};
</script>
