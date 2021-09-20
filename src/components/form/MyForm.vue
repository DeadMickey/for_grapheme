<template>
  <form class="form">
    <fieldset
      :class="[
        'form__fieldset',
        { 'form__fieldset-line': i >= formData.length - 2 && id === 'form-1' },
      ]"
      v-for="(fieldset, i) in formData"
      :key="`fieldset-${i}`"
    >
      <template v-for="el in fieldset" :key="el.id">
        <CustomInput
          v-if="!el.component"
          :id="el.id"
          :label="el.label"
          :maxlength="el.maxlength"
          :placeholder="el.placeholder"
          :type="el.type"
          v-model="exportValues[el.id]"
          :class="{
            'input-wrapper-empty':
              emptyFileds.includes(el.id) ||
              (!exportValues[el.id] && firstCheck),
          }"
        />
        <CustomSelect
          v-if="el.component === 'select'"
          :id="el.id"
          :label="el.label"
          :options="el.options"
          v-model="exportValues[el.id]"
          :class="{
            'select-wrapper-empty':
              emptyFileds.includes(el.id) ||
              (!exportValues[el.id] && firstCheck),
          }"
        />
      </template>
    </fieldset>
    <Button
      :text="buttontext"
      @click.prevent="$emit('buttonClicked', { exportValues, id }, isClicked())"
    />
  </form>
</template>

<script>
import CustomInput from "@/components/form/CustomInput";
import CustomSelect from "@/components/form/CustomSelect";
import Button from "@/components/form/MyButton";
export default {
  name: "MyForm",
  components: { CustomInput, CustomSelect, Button },
  props: {
    id: String,
    formData: [Array, Object],
    buttontext: String,
    emptyFileds: Array,
  },
  data: () => ({
    exportValues: {},
    firstCheck: false,
  }),
  methods: {
    isClicked() {
      this.firstCheck = true;
    },
  },
};
</script>

<style scoped lang="scss">
.form {
  text-align: left;
  &__fieldset {
    display: grid;
    grid-template-columns: 1fr 1fr;
    row-gap: 10px;
    column-gap: 20px;
    margin-bottom: 20px;
    padding: 0;
    border: 0;
    &-line {
      display: inline-grid;
      max-width: 95px;
      &:nth-last-child(n + 2) {
        margin-right: 30px;
      }
    }
  }
}
.input-wrapper {
  grid-column: 1 / -1;
  &:last-child {
    grid-column: initial;
  }
  &:first-child {
    grid-column: 1 / -1;
  }
}
.input-wrapper-empty {
  ::v-deep(.input-wrapper__input) {
    border-color: #ffadad;
  }
}
.select-wrapper-empty {
  ::v-deep(.select-wrapper__select) {
    border-color: #ffadad;
  }
}
</style>