<template>
  <div id="app">
    <Header :correct="correct" :total="total" />
    <QuestionBox
      
      v-if="questions.length"
      :correct="correct" :total="total" 
      :indexQ.sync="index"
      :increment="increment"
      :question="questions[index].question" 
      :incorrect_answers="questions[index].incorrect_answers"  
      :correct_answer="questions[index].correct_answer" />
    
  </div>
  
</template>

<script>
import Header from './components/Header.vue'
import QuestionBox from './components/Question.vue'

export default {
  name: 'App',
  data:() => {
    return {
      index:0,
      questions:[],
      isTrue:false,
      correct:0,
      total:0
     
    }
  },
  methods:{
    increment(isCorrect){
      if(isCorrect){
        this.correct++
      }
      this.total++
    }
  },
 

  components: {
    Header,
    QuestionBox
  },

 
  mounted: 
     function() {
      
        fetch('https://opentdb.com/api.php?amount=10&type=multiple',{
          method:'GET'
        })
        .then(response => response.json())
        .then(data => {
         
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
