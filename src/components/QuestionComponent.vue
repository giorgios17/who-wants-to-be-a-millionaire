<template>
  <div>
    <div class="container py-3">
      <div class="row justify-content-center">
        <div class="col-10 border p-2 rounded-pill">
          <div v-if="currentQuestion">
            <h5>{{ currentQuestion.text }}</h5>
          </div>
          <div v-else>
            <h5>{{ currentQuestion }}</h5>
          </div>
        </div>
        <div class="row py-5 justify-content-between">
          <button
            v-for="(item, index) in currentQuestion.answers"
            :key="index"
            class="col-5 border p-2 rounded-pill my-3 btn_answer"
            @click="verifyAnswer(item.correct)"
            :class="{
              'bg-green': showAnswer && item.correct,
              'bg-red': showAnswer && !item.correct,
            }"
            :disabled="showAnswer"
          >
            {{ item.answer }}
          </button>
        </div>
        <div v-show="showAnswer && question.length != questionDone.length">
          <button @click="nextQuestion()" type="button" class="btn btn-light">
            Prossima domanda
          </button>
        </div>
        <div v-show="question.length == questionDone.length">
          <div v-if="correctAnswer > wrongAnswer">
            <h3>Hai vinto!</h3>
          </div>
          <div v-else-if="(correctAnswer = wrongAnswer)">
            <h3>Pareggio, riprova.</h3>
          </div>
          <div v-else>
            <h3>Hai perso!</h3>
          </div>
          <ScoreComponent
            :correctAnswer="correctAnswer"
            :wrongAnswer="wrongAnswer"
          />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import ScoreComponent from "./ScoreComponent.vue";

export default {
  name: "QuestionComponent",
  data() {
    return {
      question: [
        {
          text: "Quale calciatore ha vinto più palloni d'oro?",
          answers: [
            { answer: "Messi", correct: true },
            { answer: "Maradona", correct: false },
            { answer: "Cristiano Ronaldo", correct: false },
            { answer: "Van Basten", correct: false },
          ],
        },
        {
          text: "Qual è il fiore nazionale del Giappone?",
          answers: [
            { answer: "Ninfee", correct: false },
            { answer: "Tulipani", correct: false },
            { answer: "Fiore di ciliegio", correct: true },
            { answer: "Cuore sanguinante", correct: false },
          ],
        },
        {
          text: "Qual è l’animale nazionale dell’Australia?",
          answers: [
            { answer: "Vedova nera", correct: false },
            { answer: "Canguro rosso", correct: true },
            { answer: "Quokka", correct: false },
            { answer: "Koala", correct: false },
          ],
        },
        {
          text: "Quale dei seguenti imperi non aveva una lingua scritta?",
          answers: [
            { answer: "Inca", correct: true },
            { answer: "Azteco", correct: false },
            { answer: "Egiziano", correct: false },
            { answer: "Romano", correct: false },
          ],
        },
        {
          text: "Quale paese ha il maggior numero di isole al mondo?",
          answers: [
            { answer: "Spagna", correct: false },
            { answer: "America", correct: false },
            { answer: "Australia", correct: false },
            { answer: "Svezia", correct: true },
          ],
        },
      ],
      currentQuestion: "",
      questionDone: [],
      correctAnswer: 0,
      wrongAnswer: 0,
      showAnswer: false,
    };
  },
  components: {
    ScoreComponent,
  },
  mounted() {
    this.getRandomQuestion();
  },
  methods: {
    // genera una domanda casuale dall'array di domande e se è già stata fatta ne genera una nuova
    getRandomQuestion() {
      let random =
        this.question[Math.floor(Math.random() * this.question.length)];
      if (this.questionDone.includes(random)) {
        this.getRandomQuestion();
      } else {
        this.currentQuestion = random;
      }
    },
    //verifica la risposta e genera una nuova domanda
    verifyAnswer(item) {
      if (item) {
        this.correctAnswer++;
        this.questionDone.push(this.currentQuestion);
        this.showAnswer = true;
      } else {
        this.wrongAnswer++;
        this.questionDone.push(this.currentQuestion);
        this.showAnswer = true;
      }
    },
    nextQuestion() {
      this.showAnswer = false;
      this.getRandomQuestion();
    },
  },
};
</script>

<style lang="scss" scoped>
.btn_answer {
  background-color: transparent;
  color: white;
  &:hover {
    transform: scale(1.1);
  }
}
.bg-green {
  background-color: green;
}
.bg-red {
  background-color: red;
}
#next-question {
  background-color: white;

  &:hover {
    transform: scale(1.1);
  }
}
</style>