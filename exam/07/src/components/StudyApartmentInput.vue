<template>
    <b-input-group>
        <b-form-input v-model="message"></b-form-input>
        <b-input-group-append>
          <b-button variant="outline-success" @click="insertApartmentText">삽입</b-button>
        </b-input-group-append>
  </b-input-group>
</template>

<script>
export default {
  methods: {
      insertApartmentText() {
          console.log(this.message)
      },
      addApartmentText(){
        this.$emit('addApartmentText', this.message)
      }
  },
  data() {
    return {
      message:''
    }
  },
}
</script>

<style scoped>

</style>