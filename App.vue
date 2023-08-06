<template>
  <div class="canvas-bg">
   <canvas ref="topRulerRef" class="canvas-ruler top" :style="topStyle"></canvas>
    <canvas ref="leftRulerRef" class="canvas-ruler left" :style="leftStyle"></canvas>
    <i class="canvas-ruler-cross"></i>
  </div>
</template>

<script lang="ts" setup>
  import {ref, onMounted,nextTick } from 'vue';
  import { drawRuler } from './drawRuler.ts';
      const topRulerRef = ref();
      const leftRulerRef = ref();
      let isRuler = false;
      const refreshRuler = () => {
        if (!isRuler) {
          isRuler = true;
          nextTick(() => {
            drawRuler('left', topRulerRef.value, 100,400, 24, 24);
            drawRuler('top', leftRulerRef.value, 100,400, 24, 24);
            isRuler = false;
          });
        }
      };
    onMounted(() => {
        refreshRuler();
      });
</script>

<style lang="scss" scoped>
  .canvas-ruler-cross {
    display: inline-block;
    width: 24px;
    height: 24px;
    position: absolute;
    bottom:0px;
    left: 0px;
    background-color: var(--ruler-bg);
  }
  .canvas-bg{
    position: relative;
    width:800px;
    height:500px;
  }
  .canvas-ruler {
    position: absolute;
    transform-origin: left top;
    background-color: var(--ruler-bg);

    &.left {
      bottom: -24px;
      left: 0px;
    }

    &.top {
      top: 0px;
      left: -24px;
    }
  }
</style>
