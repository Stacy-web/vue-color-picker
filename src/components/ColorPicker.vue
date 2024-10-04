<script setup>
import { ref } from 'vue'

import ColorPickerPalette from '@/components/ColorPickerPalette.vue'

const colorPickerActive = ref(false)
const color = ref({
    h: 0,
    s: 100,
    l: 50
})
</script>

<template>
    <div class="color-picker">
        <button class="color-picker__btn" @click="colorPickerActive = !colorPickerActive">
            <span></span>
            {{ color }}
        </button>
        <button class="color-picker__clear">x</button>
        <color-picker-palette v-show="colorPickerActive" v-model="color" />
    </div>
</template>

<style lang="scss">
.color-picker {
    background-color: aliceblue;
    max-width: fit-content;
    padding: 24px 16px;
    border-radius: 12px;
    border: 1px solid rgb(134, 194, 246);
    display: flex;
    align-items: center;
    justify-content: space-between;
    position: relative;

    & button {
        cursor: pointer;
    }

    &__btn {
        border: none;
        background: transparent;
        position: relative;
        display: flex;
        align-items: center;
        justify-content: space-between;
        padding: 0;
        margin-right: 16px;

        &::before {
            content: '';
            position: relative;
            width: 15px;
            height: 15px;
            flex: 0 0 15px;
            border: 1px solid rgb(134, 194, 246);
            border-radius: 2px;
            margin-right: 8px;
        }
    }

    &__clear {
        background: rgb(51, 108, 159);
        color: #fff;
        font-weight: 500;
        border: 0 none;
        border-radius: 2px;
        line-height: 14px;
        font-size: 14px;
        padding: 4px 8px;
    }
}
</style>
