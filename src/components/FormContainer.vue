<template>
  <div class="form-container">
    <FormStepper
      v-if="currentStep < 2"
      :step="currentStep"
      @backStepCall="backStep"
    />
    <div v-if="currentStep < 2" class="form-container__headline">
      {{ currentStep ? "Оплата" : "Информация для доставки" }}
    </div>
    <template v-for="(form, i) in someData" :key="`form-${i}`">
      <Form
        :id="`form-${i}`"
        v-show="currentStep === i"
        :formData="form"
        :buttontext="i < someData.length - 1 ? 'Продолжить' : 'Оплатить'"
        @buttonClicked="swapStep"
        :emptyFileds="emptyFileds"
      />
    </template>
    <div v-if="currentStep === 2" class="verified">
      <i class="verified__icon fal fa-check-circle"></i>
      <span>Спасибо!</span>
    </div>
  </div>
</template>

<script>
import FormStepper from "@/components/stepper/FormStepper";
import Form from "@/components/form/MyForm";
export default {
  name: "FormContainer",
  components: { FormStepper, Form },
  data: () => ({
    currentStep: 1,
    emptyFileds: [],
    someData: [
      [
        [{ id: "fio", placeholder: "ФИО", label: "Получатель" }],
        [
          { id: "city", placeholder: "Город", label: "Адрес" },
          { id: "address", placeholder: "Адрес" },
          {
            id: "country",
            options: ["Россия", "Украина", "США"],
            component: "select",
          },
          { id: "postcode", placeholder: "Индекс", type: "number" },
        ],
      ],
      [
        [
          {
            id: "card-name",
            placeholder: "Konstantin Ivanov",
            label: "Имя на карте",
          },
        ],
        [
          {
            id: "card-number",
            placeholder: "XXXX XXXX XXXX XXXX XXXX",
            label: "Номер карты",
            maxlength: 24,
          },
        ],
        [
          {
            id: "card-term",
            placeholder: "MM / YY",
            maxlength: 7,
            label: "Срок",
          },
        ],
        [{ id: "card-CVV", placeholder: "", label: "CVV", type: "number" }],
      ],
    ],
    sendMsg: "payment-info=",
  }),
  methods: {
    checkFormFields(obj, array) {
      Object.keys(array).forEach((el) => {
        if (!obj[el]) {
          this.emptyFileds.push(el);
          delete obj[el];
        }
      });
    },
    checkFormFieldsLegth(number) {
      return this.someData[number].reduce((acc, el) => {
        return (acc += el.length);
      }, 0);
    },
    swapStep(formInfo) {
      this.checkFormFields(formInfo.exportValues, formInfo.exportValues);
      const formNumber = Number(formInfo.id.slice(-1));
      const formValues = Object.keys(formInfo.exportValues);

      if (this.checkFormFieldsLegth(formNumber) == formValues.length) {
        ++this.currentStep;
      }
    },
    backStep() {
      if (this.currentStep) {
        --this.currentStep;
      }
    },
  },
};
</script>

<style scoped lang="scss">
.form-container {
  width: 400px;
  height: 520px;
  padding: 20px 40px;
  background-color: white;
  box-shadow: 0px 0px 10px #ebf0ff;
  border-radius: 24px;
  color: #101d94;
  &__headline {
    margin-top: 30px;
    margin-bottom: 20px;
    font-size: 25px;
    font-weight: 300;
    text-align: left;
  }
}
.verified {
  height: 100%;
  display: flex;
  flex-flow: column;
  gap: 10px;
  align-items: center;
  justify-content: center;
  font-weight: 300;
  font-size: 26px;
  color: black;
  &__icon {
    font-size: 54px;
  }
}
</style>
