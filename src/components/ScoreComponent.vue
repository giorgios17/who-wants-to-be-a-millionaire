<template>
  <div>
    <h3>Hai terminato le domande! Il tuo risultato:</h3>
    <h4>Risposte corrette: {{ correctAnswer }}</h4>
    <h4>Risposte sbagliate: {{ wrongAnswer }}</h4>
  </div>
</template>

<script>
export default {
  name: "ScoreComponent",
  props: {
    correctAnswer: Number,
    wrongAnswer: Number,
  },
};
</script>

<style lang="scss" scoped>
</style>