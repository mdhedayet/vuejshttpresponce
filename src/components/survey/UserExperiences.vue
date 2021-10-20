<template>
  <section>
    <base-card>
      <h2>Submitted Experiences</h2>
      <div>
        <base-button @click="loadExperiences">Load Submitted Experiences</base-button>
      </div>
      <p v-if="isLoading">Loading....</p>
      <ul v-if="!isLoading">
        <survey-result
          v-for="result in results"
          :key="result.id"
          :name="result.name"
          :rating="result.rating"
        ></survey-result>
      </ul>
    </base-card>
  </section>
</template>

<script>
import SurveyResult from './SurveyResult.vue';

export default {
  // props: ['results'],
  data(){
    return{
      results:[],
      isLoading: false

    }
  },
  components: {
    SurveyResult,
  },
 
  methods:{
    loadExperiences(hello){
      this.isLoading = true;
      fetch('https://vue-hhtp-demo-h-default-rtdb.asia-southeast1.firebasedatabase.app/survey.json')
      .then((response) => response.json())
      .then((json) =>
        {
          this.isLoading = false;
          const result = [];
          for(const id in json){
            result.unshift({
              id:id,
              name: json[id].name,
              rating:json[id].rating,
            });
           }
          console.log(result);
          this.results = result;
        }).catch()
        console.log(hello);
        }
  },

  mounted(){
    this.loadExperiences();
    console.log('hedayet');
  }
};
</script>

<style scoped>
ul {
  list-style: none;
  margin: 0;
  padding: 0;
}
</style>