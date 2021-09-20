<template>
  <div class="stepper">
    <template v-for="(item, i) in steps" :key="item">
      <span
        :class="['stepper__item', { 'stepper__item-active': step === i }]"
        @click="$emit('backStepCall')"
        >{{ item }}</span
      >
      <i v-if="i < steps.length - 1" class="icon fal fa-chevron-right"></i>
    </template>
  </div>
</template>

<script>
export default {
  name: "FormStepper",
  props: {
    step: Number,
  },
  
  data: () => ({
    steps: ["Доставка", "Оплата"],
  }),
};
</script>

<style scoped lang="scss">
.stepper {
  display: flex;
  justify-content: flex-start;
  font-size: 12px;
  &__item {
    color: #979797;
    cursor: pointer;
    &-active {
      color: #101d94;
    }
  }
}
.icon {
  margin: 0 15px;
  color: #979797;
}
</style>