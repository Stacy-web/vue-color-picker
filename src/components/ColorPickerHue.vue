<script setup>
import { ref, defineEmits } from 'vue'

const coordinateX = ref(0, 0, 100)

const emit = defineEmits(['change-hsl'])

function test(e) {
    const hueOffset = e.target.getBoundingClientRect()

    coordinateX.value = Math.floor(e.clientX - hueOffset.left)
    const colorH = Math.floor((coordinateX.value / hueOffset.width) * 360)

    emit('change-hsl', { h: colorH })
}
</script>

<template>
    {{ coordinateX }}
    <div class="color-picker__hue" @mousedown="test">
        <span :style="`left: ${coordinateX}px`"></span>
    </div>
</template>

<style lang="scss">
.color-picker__hue {
    width: 100%;
    height: 25px;
    background: linear-gradient(
        to right,
        rgba(255, 0, 0),
        rgba(255, 0, 255),
        rgba(0, 0, 255),
        rgba(0, 255, 255),
        rgba(0, 255, 0),
        rgba(255, 255, 0),
        rgba(255, 0, 0)
    );
    cursor: crosshair;
    position: relative;

    & span {
        position: absolute;
        top: 50%;
        left: 0;
        transform: translate(-50%, -50%);
        width: 25px;
        height: 25px;
        min-width: 25px;
        min-height: 25px;
        display: block;
        background-color: #fff;
        border-radius: 50%;
        box-shadow: 0px 0px 10px -4px #303030;
        transition: 0.3s linear;
    }
}
</style>
