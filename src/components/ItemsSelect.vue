<script setup>
import { ref } from 'vue';

const {items, single} = defineProps({
    items: {
        type: Array,
        default: [],
        required: true
    },
    single: {
        type: Boolean,
        default: false,
    },
    data: {
        type: Array,
        default: [],
        required: true
    }
})
const emit = defineEmits(['update:data']);
const type = single ? 'radio' : 'checkbox';
const selectVal = ref([]);
</script>

<template lang="pug">
ul.select
    li(v-for="item in items" :key="item.id").select__item
        label.select__label 
            span {{ item.name }}
            input.select__input(
                :type="type" 
                :value="item.id" 
                v-model="selectVal" 
                @change="emit('update:data', selectVal.value)")
             
</template>

<style scoped lang="scss">
@import "@/assets/styles/base/mixins.scss";


.select {
    display: grid;
    grid-template-columns: repeat(auto-fill, 100px);
    grid-gap: 10px;
    justify-content: space-between;
    grid-auto-rows: min-content;
    width: calc(50% - 5px);
    padding: 10px;
    border: 5px solid #555555;
    box-sizing: border-box;

    .select__item {
        height: 100px;

        &:hover label {
            border: 5px solid #eab300;
        }
    }

    .select__label {
        @include center;
        width: 100%;
        height: 100%;
        min-height: auto;
        background-color: #5274ff;
        cursor: pointer;
        transition: border .5s;
        border: 5px solid #555555;
        box-sizing: border-box;
        text-align: center;
        &:has(> .select__input:checked) { 
            border: 5px solid #9dff60;
        }
    }

    .select__input {
        opacity: 0;
        position: absolute;
    }

    @media (max-width: 600px) {
        justify-content: center;
    }
}
</style>