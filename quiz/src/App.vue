<template>
  <div id="app">
    <HeaderComponent />
    <b-row>
      <b-col sm="6" offset="3">
        <QuestionBoxComponent 
          v-if="this.questions.length > 0"
          :currentQuestion="questions[index]"
          :next="next"
        />
      </b-col>
    </b-row>
  </div>
</template>

<script>
import HeaderComponent from './components/HeaderComponent.vue';
import QuestionBoxComponent from './components/QuestionBoxComponent.vue';

export default {
  name: 'App',
  components: {
    HeaderComponent,
    QuestionBoxComponent,
  },
  data() {
    return {
      questions: [],
      index: 0
    }
  },
  methods: {
    next() {
      this.index++;
    }
  },
  mounted: function() {
    fetch('https://opentdb.com/api.php?amount=10&category=27&type=multiple', {
      method: 'get'
    })
      .then((response) => {
        return response.json();
      })
      .then((data) => {
        console.log(data);
        this.questions = data.results
      });
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
