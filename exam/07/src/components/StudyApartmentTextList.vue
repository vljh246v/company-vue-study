<template>
  <div role="tablist">
    <b-card v-for="(apartment, index) in propsdata" :key="apartment.name" no-body class="mb-1">
      <b-card-header header-tag="header" class="p-1" role="tab">
        <b-button block v-b-toggle="'accordion-' + index" variant="info">{{apartment.name}}</b-button>
      </b-card-header>
      <b-collapse :id="'accordion-' + index"  accordion="my-accordion" role="tabpanel">
        <b-card-body  v-for="(text, index2) in apartment.value" :key="index2">
          <b-card-text>{{text}}</b-card-text>
          <b-button block @click="deleteApartmentText(apartment.name, index2)">삭제
          </b-button>
        </b-card-body>
      </b-collapse>
    </b-card>
  </div>
</template>

<script>
  export default {
    props:['propsdata'],
    data() {
      return {
      }
    },
    methods: {
        deleteApartmentText(apartmentName, index) {
            this.$emit('deleteApartmentText', apartmentName, index)
        }
    }
  }
</script>

<style scoped>

</style>