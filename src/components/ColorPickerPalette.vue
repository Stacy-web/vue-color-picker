<script setup>
import { defineModel } from 'vue'

import ColorPickerSaturation from '@/components/ColorPickerSaturation.vue'
import ColorPickerHue from '@/components/ColorPickerHue.vue'

const color = defineModel()

function changeHsl(args) {
    Object.assign(color.value, args)
    console.log(color.value)
}
</script>

<template>
    <div class="color-picker-palette">
        <color-picker-saturation :hsl="color" @change-hsl="changeHsl" />
        <color-picker-hue @change-hsl="changeHsl" />
    </div>
</template>

<style lang="scss">
.color-picker-palette {
    position: absolute;
    bottom: -10px;
    left: 0;
    background: #fff;
    transform: translateY(100%);
    box-shadow: 0px 0px 10px -2px #919191;
    border-radius: 4px;
    padding: 20px;
}
</style>
