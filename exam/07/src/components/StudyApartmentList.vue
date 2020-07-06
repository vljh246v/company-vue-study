<template>

<div>
    <b-form-select v-model="selected"  v-on:change="getSelectedApartment">                   
        <option v-for="(apartment, index) in options"
            :key="apartment.name"
            value-field="name"
            :value="apartment.name">
            {{ apartment.name }}
        </option>
    </b-form-select>
</div>
</template>

<script>
export default {
    props:['propsdata'],
    methods: {
        changeApartmentName(apartmentName, index) {
            console.log(apartmentName, index)
            this.$refs.dropdown.text = apartmentName;
        },
        getSelectedApartment() {
            this.$emit('selectApartment', this.selected)
        }
    },
    created() {
        this.options = this.propsdata
        this.selected = this.options[0].name
        this.getSelectedApartment();
        
    },
    data() {
        return {
            selected:'',
            options: []
        }
    }
}
</script>

<style scoped>

</style>