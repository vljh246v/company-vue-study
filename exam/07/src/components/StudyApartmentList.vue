<template>

<div>
    <b-form-select v-model="selected">                   
    <option v-for="(apartment, index) in propsdata"
        :key="apartment.name"
        :value="apartment.name"
    >
        {{ apartment.name }}
    </option>
</b-form-select>
</div>
    <!-- <b-dropdown ref="dropdown" id="dropdown" text="선택" class="m-md-2" >
        <b-dropdown-item v-for="(apartment, index) in propsdata" :key="apartment.name" @click="changeApartmentName(apartment.name, index)">{{ apartment.name }}</b-dropdown-item>
    </b-dropdown> -->
</template>

<script>
export default {
    props:['propsdata'],
    methods: {
        changeApartmentName(apartmentName, index) {
            console.log(apartmentName, index)
            this.$refs.dropdown.text = apartmentName;
        }
    },
    created() {
        if(localStorage.length > 0) {
            for (var i = 0; i< localStorage.length; i++){
                this.todoItems.push(localStorage.key(i));
            }
        }
    },
    data() {
        return {
            selected:''
        }
    }
}
</script>

<style scoped>

</style>