<template>
   <v-container fluid grid-list-md>
      <v-layout row wrap>
         <v-flex xs8>
            <question v-for="question in questions" :key="question.path" :question=question>

            </question>
         </v-flex>
         sidebar
      </v-layout>
   </v-container>
</template>

<script>
import Question from './Question.vue'
export default {
    components: {Question},
    data: function(){
       return{
          questions: {}
       }
    },
    created(){
       axios.get('/api/question')
       .then(res => this.questions = res.data.data)
       .catch(error => console.log(error.response.data))
    }
}
</script>

<style lang="">
    
</style>