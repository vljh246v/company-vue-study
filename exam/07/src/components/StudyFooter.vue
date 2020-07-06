<template>
    <b-button block variant="primary" @click="deleteAllApartmentText">전체 삭제</b-button>
</template>


<script>
export default {
    methods: {
        deleteAllApartmentText() {
            this.$emit('deleteAllApartmentText')
        }
    }
}
</script>

<style scoped>

</style>