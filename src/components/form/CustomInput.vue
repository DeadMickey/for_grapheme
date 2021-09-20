<template>
  <div class="input-wrapper">
    <label v-if="label" class="input-wrapper__label" :for="id">{{
      label
    }}</label>
    <input
      class="input-wrapper__input"
      :type="type ?? 'text'"
      :id="id"
      :value="modelValue"
      @input="sendValue"
      :placeholder="placeholder"
      :maxlength="maxlength"
      @keydown.delete="backspacePush = true"
      @keyup.delete="backspacePush = false"
    />
  </div>
</template>

<script>
export default {
  name: "CustomInput",
  props: {
    id: String,
    label: String,
    type: String,
    maxlength: Number,
    placeholder: String,
    modelValue: [String, Number],
  },
  data: () => ({
    backspacePush: false,
  }),
  methods: {
    sendValue(e) {
      let value;
      if (this.id === "card-number" && !this.backspacePush) {
        value = e.target.value.replace(/[^\d^ ]/g, "");
        switch (value.length) {
          case 4:
            value += " ";
            break;
          case 9:
            value += " ";
            break;
          case 14:
            value += " ";
            break;
          case 19:
            value += " ";
            break;
          default:
            break;
        }
        e.target.value = value;
      } else {
        value = e.target.value;
      }
      if (this.id === "card-term" && !this.backspacePush) {
        if (value.length == 2) {
          value += " / ";
        }
      }
      this.$emit("update:modelValue", value);
    },
  },
};
</script>

<style scoped lang="scss">
.input-wrapper {
  text-align: left;
  &__label {
    margin-bottom: 6px;
    display: inline-block;
    font-size: 18px;
  }
  &__input {
    height: 40px;
    width: 100%;
    padding: 10px 15px;
    background: #ffffff;
    border: 1px solid #dedcdc;
    border-radius: 5px;
    &:focus {
      border-color: #c9c5c5;
      outline: 0;
    }
    &::placeholder {
      color: #6b6b6b;
    }
  }
}
</style>