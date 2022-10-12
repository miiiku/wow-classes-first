<script setup>
import { computed, inject } from "vue"
import ClassConfig from '@/constants/class'

const rollClass    = inject('ROLL_CLASS')


const classInfo = computed(() => {
  return ClassConfig[rollClass[0]] || {}
})

</script>

<template>
<div class="result-panel">
  <div class="result-title">
    <h1 :style="{ color: classInfo.color }">你的首发职业为：{{ classInfo.title }}</h1>
  </div>
  <button>官方介绍</button>
  <button>从新来过</button>
</div>
</template>

<style scoped>

.result-panel {
  width: 680px;
  height: 420px;
  border-radius: 4px;
  overflow: hidden;
  display: flex;
  flex-direction: column;
  align-items: center;
}

.result-title {
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.result-bg {
  display: block;
  width: 100%;
  border-radius: 4px;
  overflow: hidden;
}

</style>