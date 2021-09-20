<template>
  <button class="button">{{ text }}</button>
</template>

<script>
export default {
  name: "MyButton",
  props: {
    text: String,
  },
};
</script>

<style lang="scss">
.button {
  height: 45px;
  width: 180px;
  background-color: rgba(25, 165, 39, 0.8);
  border: none;
  border-radius: 5px;
  color: white;
  cursor: pointer;
}
</style>