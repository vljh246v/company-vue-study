<template>
    <div id="app">
      <b-container>
        <b-row>
          <StudyHeader></StudyHeader>
        </b-row>
        <b-row>
          <b-col sm="4">
            <StudyApartmentList v-bind:propsdata="apartments" v-on:selectApartment="selectApartment"></StudyApartmentList>
          </b-col>
          <b-col sm="8">
            <StudyApartmentInput v-on:addApartmentText="addApartmentText"></StudyApartmentInput>
          </b-col>  
        </b-row>
        <b-row>
          <b-col sm="12">
            <StudyApartmentTextList v-bind:propsdata="apartments" v-on:deleteApartmentText="deleteApartmentText"></StudyApartmentTextList>
          </b-col>
        </b-row>
        <b-row>
          <b-col sm="12">
            <StudyFooter v-on:deleteAllApartmentText="deleteAllApartmentText"></StudyFooter>
          </b-col>
        </b-row>
      </b-container>
    </div>
</template>


<script>
import StudyHeader from './components/StudyHeader.vue'
import StudyApartmentList from './components/StudyApartmentList.vue'
import StudyApartmentInput from './components/StudyApartmentInput.vue'
import StudyApartmentTextList from './components/StudyApartmentTextList.vue'
import StudyFooter from './components/StudyFooter.vue'

export default {
  components: {
    'StudyHeader': StudyHeader,
    'StudyApartmentList': StudyApartmentList,
    'StudyApartmentInput': StudyApartmentInput,
    'StudyApartmentTextList': StudyApartmentTextList,
    'StudyFooter': StudyFooter
  },
  data() {
    return {
      selected:'',
      apartments: [
        {
          'name': '아파트1',
          'value' :["df","dfss"]
        },{
          'name': '아파트2',
          'value' :[]
        },{
          'name': '아파트3',
          'value' :[]
        }]
    }
  },
  created() {
  },
  methods: {
    addApartmentText(text) {
      for(var apartment in this.apartments){
        if(this.apartments[apartment].name == this.selected){
          console.log(this.apartments[apartment])
          this.apartments[apartment].value.push(text);
        }
      }
    },
    selectApartment(name){
      this.selected = name;
    },
    deleteApartmentText(name, index){
      for(var apartment in this.apartments){
        if(this.apartments[apartment].name == name){
          this.apartments[apartment].value.splice(index, 1)
        }
      }
    },
    deleteAllApartmentText(){
      for(var apartment in this.apartments){
        this.apartments[apartment].value = [];
      }
    }
  }
}
</script>

<style>

</style>