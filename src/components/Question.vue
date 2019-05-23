<template>
  <div class="question-box-container">
  <b-jumbotron>

    <template slot="lead">
      <p v-html="question.question"></p> 
    </template>

    <hr class="my-4">

    <b-list-group class="mb-3">
      <b-list-group-item
        v-for="(answer, index) in shuffledAnswers" 
        :key="index"
        @click="selectAnswer(index)"
        :class="answerClass(index)"
      >
        {{answer}}
      </b-list-group-item>
    </b-list-group>

    <b-button variant="success" @click="next" href="#" class="m-1">Next</b-button>
    <b-button variant="primary" @click="submitAnswer" href="#" class="m-1"
      :disabled="selectedIndex === null || answered"
    >Submit</b-button>
  </b-jumbotron>
</div>
</template>

<script>
  import _ from 'lodash'

  export default {
    props: {
      question: Object,
      next: Function,
      increment: Function
    },
    data(){
      return {
        selectedIndex: null,
        shuffledAnswers: [],
        correctIndex: null,
        answered: false
      }
    },
    watch: {
      question: {
        immediate: true,
        handler(){
          this.selectedIndex = null
          this.shuffleAnswers()
          this.answered = false
        }
      }
    },
    methods: {
      selectAnswer(index) {
        this.selectedIndex = index
      },
      shuffleAnswers(){
        let answers = [...this.question.incorrect_answers, this.question.correct_answer]
        this.shuffledAnswers = _.shuffle(answers)
        this.correctIndex = this.shuffledAnswers.indexOf(this.question.correct_answer)
      },
      submitAnswer() {
        let isCorrect = false

        if(this.selectedIndex === this.correctIndex) {
          console.log('you correct!')
          isCorrect = true
        }

        this.answered = true

        this.increment(isCorrect)
      },
      answerClass(index) {
        let answerClass = ''
        
        if(!this.answered && this.selectedIndex === index) {
          answerClass = 'selected'
        }
        else if(this.answered && this.correctIndex === index) {
          answerClass = 'correct'
        }
        else if(this.answered && this.selectedIndex === index && this.correctIndex !== index) {
          answerClass = 'incorrect'
        }

        return answerClass
      }
    },
    computed: {
      answers: function(){
        let answers = [...this.question.incorrect_answers]
        return answers
      }
    }
  }
</script>
<style scoped>
  .list-group-item:hover {
    background-color:#e9ecef;
    cursor:pointer;
  }
  .selected{
    background-color:lightblue;
  }
  .correct{
    background-color:lightgreen;
  }
  .incorrect{
    background-color: lightcoral;
  }
</style>