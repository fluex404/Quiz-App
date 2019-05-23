<template>
  <div id="app">
    <Header></Header>
    <b-container>
      <b-row>
        <b-col sm="6" offset="3">
          <Question 
          v-if="questions.length"
          :question="questions[index]"
          :next="next"
          >
          </Question>
        </b-col>
      </b-row>
    </b-container>
  </div>
</template>

<script>
import Header from './components/Header.vue'
import Question from './components/Question.vue'
import axios from 'axios'

export default {
  name: 'app',
  components: {
    Header,
    Question
  },
  data(){
    return {
      questions: [],
      index: 0
    }
  },
  methods: {
    next: function(){
      this.index++;
      if(this.index > 9) {
        this.index = 0;
      }
    }
  },
  mounted: function(){
    axios.get('https://opentdb.com/api.php?amount=10&category=27&type=multiple')
    .then(r => this.questions = r.data.results)
    .catch(err => console.log("error: "+err))
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
