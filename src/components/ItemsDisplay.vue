<script setup>
const {dark} = defineProps({
    items: {
        type: Array,
        default: '#'
    },
    dark: {
        type: Boolean,
        default: false
    },
    button: {
        type: Boolean,
        default: false
    },
})
</script>

<template lang="pug">
.display
    p шоу
</template>

<style scoped lang="scss">

</style>