<template>
  <div class="question-box-container">
  <b-jumbotron>

    <template slot="lead">
      {{question.question}} 
    </template>

    <hr class="my-4">

    <p>
      List of answers
    </p>

    <b-button variant="primary" href="#" class="m-1">Submit</b-button>
    <b-button variant="success" @click="next" href="#" class="m-1">Next</b-button>
  </b-jumbotron>
</div>
</template>

<script>
  export default {
    props: {
      question: Object,
      next: Function
    }
  }
</script>