<template>
  <div class="bg_content">
    <div id="logo-container" class="p-4">
      <img alt="logo" src="../assets/logo.png" />
    </div>
    <div>
      <QuestionComponent />
      <AnswersComponent />
    </div>
  </div>
</template>

<script>
import QuestionComponent from "./QuestionComponent.vue";
import AnswersComponent from "./AnswersComponent.vue";
export default {
  name: "ContainerApp",
  components: {
    QuestionComponent,
    AnswersComponent,
  },
};
</script>

<style lang="scss" scoped>
#logo-container {
  background-color: #141589;
  img {
    width: 300px;
  }
}
.bg_content {
  background-color: #11093a;
  height: 100vh;
}
</style>