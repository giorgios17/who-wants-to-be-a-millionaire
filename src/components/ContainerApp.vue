<template>
  <div class="bg_content">
    <div id="logo-container" class="p-4">
      <img alt="logo" src="../assets/logo.png" />
    </div>
    <div>
      <QuestionComponent />
    </div>
  </div>
</template>

<script>
import QuestionComponent from "./QuestionComponent.vue";
export default {
  name: "ContainerApp",
  components: {
    QuestionComponent,
  },
};
</script>

<style lang="scss" scoped>
#logo-container {
  background-color: #141589;
  img {
    width: 200px;
    @media screen and (min-width: 576px) {
      width: 300px;
    }
    @media screen and (max-height: 670px) {
      width: 100px;
    }
  }
}
.bg_content {
  background-color: #11093a;
  height: 100vh;
  overflow-y: hidden;
}
</style>