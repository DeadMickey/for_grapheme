<template>
  <div class="select-wrapper">
    <label v-if="label" class="select-wrapper__label" :for="id">{{
      label
    }}</label>
    <select class="select-wrapper__select" :id="id" @change="sendValue">
      <option selected disabled>Страна</option>
      <template v-for="option in options" :key="option">
        <option :value="option">{{ option }}</option>
      </template>
    </select>
    <i class="select-wrapper__chevron fal fa-chevron-down"></i>
  </div>
</template>

<script>
export default {
  name: "CustomSelect",
  props: {
    id: String,
    label: String,
    def: String,
    options: [Array, Object],
    /*  modelValue: String, */
  },
  methods: {
    sendValue(e) {
      this.$emit("update:modelValue", e.target.value);
    },
  },
};
</script>

<style scoped lang="scss">
.select-wrapper {
  position: relative;
  text-align: left;
  &__label {
    margin-bottom: 6px;
    display: inline-block;
    font-size: 18px;
  }
  &__select {
    height: 40px;
    width: 100%;
    padding: 10px 15px;
    background: #ffffff;
    border: 1px solid #dedcdc;
    border-radius: 5px;
    -moz-appearance: none;
    -webkit-appearance: none;
    appearance: none;
    &:focus {
      border-color: #c9c5c5;
      outline: 0;
    }
    &::placeholder {
      color: #6b6b6b;
    }
  }
  &__chevron {
    position: absolute;
    right: 15px;
    top: calc(50% - 8px);
  }
}
</style>