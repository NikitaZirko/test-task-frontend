<script setup>
import ItemsDisplay from '@/components/ItemsDisplay.vue'
import ItemsSelect from '@/components/ItemsSelect.vue'
import userItems from '@/data/user-items.json'
import ourItems from '@/data/our-items.json'
import { ref } from "vue";

const selectUserItems = ref([]);
const selectOurItems = ref([]);

</script>

<template lang="pug">
.wrapper
    .card
        .card__display 
            ItemsDisplay(
                :items="selectUserItems")

            ItemsDisplay(
                :items="selectOurItems")

        .card__select
            ItemsSelect(
                :items="userItems" 
                v-model:data="selectUserItems")

            ItemsSelect(
                :items="ourItems" 
                v-model:data="selectOurItems"
                :single="true")
</template>

<style scoped lang="scss">
.wrapper {
    min-height: 100vh;
    display: flex;
    justify-content: center;
    padding: 10px;
    box-sizing: border-box; 
}

.card {
    min-height: 100%;
    width: 1024px;
    display: flex;
    flex-direction: column;
    border: 5px solid #555555;

    .card__display,
    .card__select {
        display: flex;
        justify-content: space-between;
        margin: 10px;
    }
    .card__display {
        margin-bottom: 0;
    }
    .card__select {
        flex: 1 1 auto;
    }
}
</style>