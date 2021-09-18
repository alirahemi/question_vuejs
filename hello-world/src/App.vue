<template>
  <div>
    <Header :correctCount="correctCount" :totalCount="totalCount" />
    <b-row>
      <b-col sm="6" offset="3"> 
        <Content v-if="questionlist.length" :cquestion="questionlist[index]" :next="next" :increment="increment" /> 
      </b-col>     
    </b-row>
  </div>
</template>
<script>

import Content from './components/Content.vue'
import Header from './components/Header.vue'

export default {
  name: 'App',
  components: {
    Header,
    Content
  },
  data(){
    return{
      questionlist : [],
      index: 0,
      correctCount: 0,
      totalCount: 0
    }
  },
  methods: {
    next(){
      if(this.index < 9) {
        this.index++
      }
    },
    increment(is_correct){
      if(is_correct){
        this.correctCount++;
      }
      this.totalCount++;
    }
  },
  mounted: function(){
    fetch("https://opentdb.com/api.php?amount=10&category=11",{
      method: 'get'
    }).then((response)=>{
      return response.json()
    }).then((result)=>{
      this.questionlist = result.results;
    })
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
