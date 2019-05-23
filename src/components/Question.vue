<template>
  <div class="question-box-container">
  <b-jumbotron>

    <template slot="lead">
      <p v-html="question.question"></p> 
    </template>

    <hr class="my-4">

    <b-list-group class="mb-3">
      <b-list-group-item
        v-for="(answer, index) of answers" 
        :key="index"
      >
        {{answer}}
      </b-list-group-item>
    </b-list-group>

    <b-button variant="success" @click="next" href="#" class="m-1">Next</b-button>
    <b-button variant="primary" href="#" class="m-1">Submit</b-button>
  </b-jumbotron>
</div>
</template>

<script>
  export default {
    props: {
      question: Object,
      next: Function
    },
    computed: {
      answers: function(){
        let answers = [...this.question.incorrect_answers]
        return answers
      }
    }
  }
</script>