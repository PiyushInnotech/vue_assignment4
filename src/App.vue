<template>
  <div class="formBody">
    <signup_form />
  </div>
</template>

<script>
import signup_form from "./components/signup_form.vue";
export default {
  name: "App",
  data() {
    return {};
  },
  components: { signup_form },
};
</script>

<style scoped>
.formBody{
  height: 94vh;
  width: 95%;
  margin-left: 2.5%;
  background-color: white;
  margin-top: 1.5%;
  border-radius: 10px;
  color: #bec2c4;
}
</style>
