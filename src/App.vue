<template>
  <div id="app">
    <Header></Header>
    <b-container>
      <b-row>
        <b-col sm="6" offset="3">
          <Question />
        </b-col>
      </b-row>
    </b-container>
  </div>
</template>

<script>
import Header from './components/Header.vue'
import Question from './components/Question.vue'

export default {
  name: 'app',
  components: {
    Header,
    Question
  },
  mounted: function(){
    console.log('mounted');
    fetch('https://opentdb.com/api.php?amount=10&category=27&type=multiple', {method: 'get'})
    .then(r => console.log(r.json));
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
