<template>
    <div class="custom-button" @mousemove="move" @mouseenter="enter" @mouseleave="leave">
        <span class="follow" ref="followRef"
            :style="{ transform: `translate(${loc.X}px, ${loc.Y}px) scale(${isShowCircle ? 1 : 0})`, transitionDuration: tds }"></span>
        <span class="text">
            <slot></slot>
        </span>
    </div>
</template>
<script setup lang="ts">
import { reactive, ref } from 'vue';

const isShowCircle = ref(false)
const followRef = ref()
const loc = reactive({
    X: 0,
    Y: 0
})
const tds = ref('0.2s')
const enter = () => {
    isShowCircle.value = true
    setTimeout(() => {
        tds.value = '0s';
    }, 200);
}
const leave = () => {
    isShowCircle.value = false
    tds.value = '0.2s';
}
const move = (e: MouseEvent) => {
    const { offsetX, offsetY } = e
    loc.X = offsetX - 90;
    loc.Y = offsetY - 90;
}

</script>
<style scoped>
.custom-button {
    height: 80px;
    width: 400px;
    background: linear-gradient(to right, #39D5FF, #868bff);
    color: #fff;
    border: none;
    border-radius: 5px;
    cursor: pointer;
    overflow: hidden;
    display: flex;
    justify-content: center;
    align-items: center;
    position: relative;
}

.follow {
    width: 180px;
    height: 180px;
    background: radial-gradient(circle, #868bff 0%, transparent 70%, transparent 100%);
    transform-origin: center;
    pointer-events: none;
    position: absolute;
    left: 0;
    top: 0;
}

.text {
    z-index: 1;
    pointer-events: none;
}
</style>