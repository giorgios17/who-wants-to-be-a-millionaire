<template>
  <div>
    <h2>Risposte corrette: {{ correctAnswer }}</h2>
    <h2>Risposte sbagliate:{{ wrongAnswer }}</h2>
  </div>
</template>

<script>
export default {
  name: "ScoreComponent",
  props: {
    correctAnswer: {
      type: Number,
      required: true,
    },
    wrongAnswer: {
      type: Number,
      required: true,
    },
  },
};
</script>

<style lang="scss" scoped>
</style>