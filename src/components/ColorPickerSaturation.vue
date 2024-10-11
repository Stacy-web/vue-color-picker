<script setup>
import { ref, computed, defineEmits } from 'vue'

const coordinates = ref([0, 0])
const mousedown = ref(false)

const props = defineProps({
    hsl: Object
})

const emit = defineEmits(['change-hsl'])

function test(e) {
    if (mousedown.value) {
        const saturationOffset = e.currentTarget.getBoundingClientRect()

        coordinates.value[0] = Math.floor(e.clientX - saturationOffset.left)
        coordinates.value[1] = Math.floor(e.clientY - saturationOffset.top)

        const colorS = Math.floor((coordinates.value[0] / saturationOffset.width) * 100)
        const colorL = Math.floor(50 - (coordinates.value[1] / saturationOffset.height) * 50)

        emit('change-hsl', { s: colorS, l: colorL })
    }
}

const hslFormat = computed(() => {
    return `hsl(${props.hsl.h}deg 100% 50%)`
})
</script>

<template>
    {{ coordinates }}
    <div
        class="color-picker-saturation"
        @mousedown="
            (e) => {
                mousedown = true
                test(e)
            }
        "
        @mousemove="test"
        @mouseup="mousedown = false"
    >
        <span :style="`top: ${coordinates[1]}px; left: ${coordinates[0]}px`"></span>
    </div>
</template>

<style lang="scss">
.color-picker-saturation {
    background: linear-gradient(to right, #fff, v-bind(hslFormat)),
        linear-gradient(to bottom, rgba(0, 0, 0, 0), #000);
    background-blend-mode: multiply;
    width: 300px;
    height: 300px;
    margin-bottom: 20px;
    position: relative;
    cursor: crosshair;

    & span {
        position: absolute;
        width: 10px;
        height: 10px;
        min-width: 10px;
        min-height: 10px;
        display: block;
        top: 0;
        left: 0;
        border-radius: 50%;
        transform: translate(-50%, -50%);
        border: 2px solid #fff;
        box-shadow: 0px 0px 10px -2px #1f1f1f;
    }
}
</style>
