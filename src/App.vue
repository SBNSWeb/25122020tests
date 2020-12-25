<template>
  <div id="app">
    <Question v-bind:variants="question.variants">
        {{question.text}}
    </Question>
  </div>
</template>

<script>
import Question from './components/Question.vue'

export default {
  name: 'App',
  components: {
    Question
  }, 
  data(){
    return{
      question: {
        text: 'hello',
        variants: {
          'orange': true, 
          '4': false,
          'giraffe': false,
          'banana': false
        }
        
      }
    }
  }
}
</script>

<style>
body{
  margin:0;
}

#app {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-wrap: wrap;
  min-height: 100vh;
}
</style>
