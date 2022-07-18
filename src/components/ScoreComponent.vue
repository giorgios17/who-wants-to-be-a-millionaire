<template>
  <div class="score-animation">
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
.score-animation {
  -webkit-animation: swing-in-top-fwd 0.5s
    cubic-bezier(0.175, 0.885, 0.32, 1.275) both;
  animation: swing-in-top-fwd 0.5s cubic-bezier(0.175, 0.885, 0.32, 1.275) both;
  @-webkit-keyframes swing-in-top-fwd {
    0% {
      -webkit-transform: rotateX(-100deg);
      transform: rotateX(-100deg);
      -webkit-transform-origin: top;
      transform-origin: top;
      opacity: 0;
    }
    100% {
      -webkit-transform: rotateX(0deg);
      transform: rotateX(0deg);
      -webkit-transform-origin: top;
      transform-origin: top;
      opacity: 1;
    }
  }
  @keyframes swing-in-top-fwd {
    0% {
      -webkit-transform: rotateX(-100deg);
      transform: rotateX(-100deg);
      -webkit-transform-origin: top;
      transform-origin: top;
      opacity: 0;
    }
    100% {
      -webkit-transform: rotateX(0deg);
      transform: rotateX(0deg);
      -webkit-transform-origin: top;
      transform-origin: top;
      opacity: 1;
    }
  }
}
</style>