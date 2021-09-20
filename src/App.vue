<template>
  <FormContainer />
</template>

<script>
import FormContainer from "@/components/FormContainer";
export default {
  name: "App",
  components: {
    FormContainer,
  },
};
</script>

<style lang="scss">
@import url("assets/fontawesome/all.min.css");
#app {
  min-height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
  font-family: "Helvetica Neue", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  background-color: #d7e8f4;
}

* {
  box-sizing: border-box;
}

body {
  margin: 0;
  padding: 0;
}
</style>
