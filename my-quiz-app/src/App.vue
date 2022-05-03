<template>
  <main>
    <div class="container">
      <section v-if="!finishQuiz">
        Score: {{score}} / {{questions.length}}
        <quiz-list
          :current-question="questions[currentQuestion]"
          @setAnswer="setAnswer"/>  
        <quiz-button @click="updateQuestion" :disabled="activeButton">
          {{ currentQuestion === questions.length - 1  ? 'Finish' : 'Next'}}
        </quiz-button>
      </section>
      <section v-else>
        You are finished this Quiz!
        Your resilt: {{score}} / {{questions.length}}
      </section>
    </div>
  </main>
</template>

<script>

import QuizList from './components/Quiz-list.vue';
import QuizButton from './components/Quiz-button.vue'

export default {
  components: {
    QuizList,
    QuizButton
  },

  data() {
    return {
      questions: [
        {
          question: 'What is Vue?',
          answer: 0,
          options: [
            'A framework',
            'A library',
            'A type of hat'
          ]
        },

        {
          question: 'What is Vuex used for?',
          answer: 2,
          options: [
            'Eating a delicious snack',
            'Viewing things',
            'State management'
          ]
        },

        {
          question: 'What is Vue Router?',
          answer: 1,
          options: [
            'An ice cream maker',
            'A routing library for Vue',
            'Burger sauce'
          ]
        }],

        currentQuestion: 0,
        score: 0,
        activeButton: false,
        finishQuiz: false,
    }
  },

  methods: {
    setAnswer(event) {
      if (event)  {
        this.score++;
      }
      
      this.activeButton = true;
    },

    updateQuestion() {
      if (this.currentQuestion == this.questions.length - 1) {
        this.finishQuiz = true;
        return;
      }
      this.activeButton = false;
      this.currentQuestion++;
    }
  },
}
</script>

<style scope>
  *  {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
  }

  body {
    background-color: #3c2a4d;

    font-family: 'Roboto', sans-serif;
    color: #e0f0ea;
  }

  main {
    width: 100vw;
    height: 100vh;
  }

  .container {
    min-height: 100%;

    display: flex;
    justify-content: center;
    align-items: center;
  }
</style>