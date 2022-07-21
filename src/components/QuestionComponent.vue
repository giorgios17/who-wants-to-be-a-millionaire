<template>
  <div>
    <div class="container py-3">
      <div class="row justify-content-center">
        <div class="col-10 border p-2 rounded-pill">
          <!-- DOMANDA -->
          <div v-if="currentQuestion">
            <h5>{{ currentQuestion.text }}</h5>
          </div>
          <div v-else>
            <h5>{{ currentQuestion }}</h5>
          </div>
        </div>
        <!-- FINE DOMANDA -->
        <!-- RISPOSTE -->
        <div class="row py-3 justify-content-between">
          <button
            v-for="(item, index) in currentQuestion.answers"
            :key="index"
            class="col-12 col-md-5 border p-2 rounded-pill my-1 btn_answer"
            @click="verifyAnswer(item.correct, index)"
            :class="{
              'bg-green': showAnswer && item.correct,
              'bg-red': showAnswer && !item.correct && indexClicked === index,
              'blink-me': blink && indexClicked === index,
            }"
            :disabled="answered"
          >
            {{ item.answer }}
          </button>
          <!-- FINE RISPOSTE -->
        </div>

        <!-- REWARDS -->
        <div class="d-flex flex-column align-items-end">
          <div
            class="col-3 border border-light"
            v-for="(item, index) in rewards"
            :key="'reward' + index"
            :class="{ 'bg-green': index === correctAnswer }"
          >
            €{{ item }}
          </div>
        </div>
        <!-- FINE REWARDS -->

        <div
          v-show="showAnswer && question.length != questionDone.length && !lose"
        >
          <button
            @click="nextQuestion()"
            type="button"
            class="btn btn-light btn_next-question"
          >
            Prossima domanda
          </button>
        </div>
        <!-- SE VINCI -->
        <div v-show="question.length == questionDone.length">
          <!-- <ScoreComponent
            :correctAnswer="correctAnswer"
            :wrongAnswer="wrongAnswer"
          /> -->
          <h3>HAI VINTO €1.000.000!</h3>
          <button type="button" class="btn btn-light mt-1" @click="playAgain()">
            Gioca di nuovo!
          </button>
        </div>
        <!-- SE PERDI  -->
        <div v-show="lose">
          <h3>HAI PERSO!</h3>
          <button type="button" class="btn btn-light mt-1" @click="playAgain()">
            Gioca di nuovo!
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
// import ScoreComponent from "./ScoreComponent.vue";

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
      rewards: [0, 10000, 50000, 100000, 500000, 1000000],
      currentQuestion: "",
      questionDone: [],
      correctAnswer: 0,
      wrongAnswer: 0,
      showAnswer: false,
      blink: false,
      indexClicked: null,
      answered: false,
      lose: false,
    };
  },
  components: {
    // ScoreComponent,
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
    verifyAnswer(item, index) {
      this.indexClicked = index;
      this.answered = true;
      // lampeggia button per due secondi
      this.blink = true;
      setTimeout(() => {
        this.blink = false;
      }, 2000);
      setTimeout(() => {
        if (item) {
          this.correctAnswer++;
        } else {
          this.wrongAnswer++;
          this.lose = true;
        }
        this.questionDone.push(this.currentQuestion);
        this.showAnswer = true;
      }, 2000);
    },
    nextQuestion() {
      this.showAnswer = false;
      this.answered = false;
      this.getRandomQuestion();
    },
    playAgain() {
      this.correctAnswer = 0;
      this.wrongAnswer = 0;
      this.questionDone = [];
      this.showAnswer = false;
      this.answered = false;
      this.currentQuestion = "";
      this.lose = false;
      this.getRandomQuestion();
    },
  },
};
</script>

<style lang="scss" scoped>
.btn_answer {
  background-color: transparent;
  color: white;
  transition: all 0.2s linear;
  @media screen and (min-width: 576px) {
    &:hover:enabled {
      transform: scale(1.1);
    }
  }
}

.bg-green {
  background-color: green;
}
.bg-red {
  background-color: red;
}

.blink_me {
  animation: blinker 1s linear infinite;
}

@keyframes blinker {
  50% {
    opacity: 0;
  }
}
.blink-me {
  animation: blinker 1s linear infinite;
}

@keyframes blinker {
  50% {
    background-color: rgb(206, 206, 7);
  }
}
.btn_next-question {
  -webkit-animation: scale-up-center 0.4s linear both;
  animation: scale-up-center 0.4s linear both;
  @-webkit-keyframes scale-up-center {
    0% {
      -webkit-transform: scale(0.5);
      transform: scale(0.5);
    }
    100% {
      -webkit-transform: scale(1);
      transform: scale(1);
    }
  }
  @keyframes scale-up-center {
    0% {
      -webkit-transform: scale(0.5);
      transform: scale(0.5);
    }
    100% {
      -webkit-transform: scale(1);
      transform: scale(1);
    }
  }
}
</style>