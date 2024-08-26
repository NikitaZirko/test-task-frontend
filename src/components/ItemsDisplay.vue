<script setup>
import {toRefs} from 'vue';

const props = defineProps({
    items: {
        type: Array,
        default: [''],
        required: true
    },
    single: {
        type: Boolean,
        default: false,
    },
    quantity: {
        type: Number,
        default: 0,
    }
})

const { items, single, quantity } = toRefs(props);
const isMultiType = single.value ? false : true;
</script>

<template lang="pug">
.display
    .display__multi(v-if="isMultiType")
        ul.display__list
            li(v-for="(item, i) in items" :key="i").display__item
                span {{ item }}
        span.display__info selected: {{ items.length }}/{{ quantity }}

    .display__single(v-else)
        span {{ items[0] || 'selected \nitem' }}

</template>

<style scoped lang="scss">
@import "@/assets/styles/base/mixins.scss";

.display {
    @include center;
    min-width: 200px;
    max-width: calc(50% - 5px);
    min-height: 150px;
    padding: 10px;
    border: 5px solid #555555;
    box-sizing: border-box;
    &:last-child() {
        margin-left: 10px;
    }

    .display__multi {
        width: 100%;
        height: 100%;
        display: flex;
        flex-direction: column;
        justify-content: space-between;
    }

    .display__list {
        display: flex;
        flex-wrap: wrap;
    }

    .display__item {
        @include center;
        width: 100px;
        height: 100px;
        padding: 10px;
        margin: 0 20px 10px 0;
        border: 5px solid #555555;
        box-sizing: border-box;
    }

    .display__single {
        white-space: pre-wrap;
        text-align: center;
        text-transform: uppercase;
    }

    .display__info {
        text-align: center;
        margin-top: 20px;
    }
}
</style>