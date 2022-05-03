<template>
    <div>
        <h2 class="quiz-question">{{ currentQuestion.question }}</h2>
        <form class="quiz-list">
            <quiz-item
            v-for="(option, index) in currentQuestion.options" 
            :key="index"
            :option="option" 
            :index="index"
            :correctAnswer="currentQuestion.answer"
            :haveAnswer="haveAnswer"
            @setAnswer="setAnswer"/>
        </form>
    </div>
</template>

<script>
import QuizItem from './Quiz-item.vue'

export default {
    props: {
        currentQuestion: {
            type: Object,
            require: false
        }
    },

    components: {
        QuizItem,
    },

    data() {
        return {
            haveAnswer: false,
        }
    },

    methods: {
        setAnswer(event) {
            this.$emit('setAnswer', this.currentQuestion.answer === event);
            this.haveAnswer = true;
        }
    },

    watch: {
        currentQuestion() {
            this.haveAnswer = false;
        }
    },
}
</script>

<style>
.quiz-list {
    display: flex;
    flex-direction: column;

    margin: 10px 0;
} 

.quiz-question {
    margin-top: 20px;
}

</style>