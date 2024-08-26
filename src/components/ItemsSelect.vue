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
const toArray = (val) => type === 'radio' ? [val] : val;
const selectHandler = () => emit('update:data', toArray(selectVal.value));
</script>

<template lang="pug">
.select
    ul.select__list
        li(v-for="item in items" :key="item.id").select__item
            label.select__label 
                span {{ item.name }}
                input.select__input(
                    :type="type" 
                    :value="item.name" 
                    v-model="selectVal" 
                    @change="selectHandler")
             
</template>

<style scoped lang="scss">
@import "@/assets/styles/base/mixins.scss";

.select {
    width: calc(50% - 5px);

    .select__list {
        display: grid;
        grid-template-columns: repeat(auto-fill, 100px);
        grid-gap: 10px;
        justify-content: space-between;
        grid-auto-rows: min-content;
        width: 100%;
        height: 100%;
        padding: 10px;
        border: 5px solid #555555;
        box-sizing: border-box;

        @media (max-width: 600px) {
            justify-content: center;
        }
    }

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
        top: -50px;
        left: -50px;
    }
}
</style>