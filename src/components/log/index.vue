<script setup>
import { computed, inject, nextTick, ref, watch } from "vue"
import ClassConfig from '@/constants/class'
import ClassTag from './tag.vue'

const rollLog      = inject('ROLL_LOG')
const rollClass    = inject('ROLL_CLASS')
const setShowPanel = inject('SET_SHOW_PANEL')

const panelScrollEl = ref(null)

const showResult = computed(() => {
  return rollClass && rollClass.length
})

watch(rollLog, () => {
  nextTick(() => {
    panelScrollEl.value.scrollIntoView({
      behavior: "smooth",
      block   : "center",
      inline  : "nearest",
    });
  })
})

function handleView () {
  setShowPanel('result')
}

</script>

<template>
  <div class="log-panel">
    <div class="log-panel-inner">
      <div class="console-log__item">大乱斗中......</div>

      <div class="console-log__item" v-for="item in rollLog" :key="item">
        <class-tag :class-key="item.class" />
        <div class="roll-dice"></div>
        <div class="roll-text">{{ item.roll }}</div>
      </div>

      <template v-if="showResult">
        <div class="console-log__item" v-for="item in rollClass" :key="item">
          结果已产生：
          <class-tag :class-key="item" />
          <div class="link" @click="handleView">点 击 查 看</div>
        </div>
      </template>

      <div class="hide-el" ref="panelScrollEl"></div>
    </div>
  </div>
</template>

<style scoped>
.log-panel {
  margin: 20px auto;
  padding: 25px;
  width: 820px;
  height: 300px;
  background-color: black;
  border-radius: 4px;
  color: #FFFFFF;
}

.log-panel-inner {
  width: 100%;
  height: 100%;
  overflow-y: scroll;
}

.log-panel-inner::-webkit-scrollbar {
  display: none;
}

.log-panel .console-log__item {
  line-height: 32px;
  display: flex;
  align-items: center;
  gap: 12px;
}

.log-panel .console-log__item:not(:first-child) {
  margin-top: 16px;
}

.log-panel .console-log__item .roll-dice {
  display: block;
  width: 32px;
  height: 32px;
  border-radius: 6px;
  background-color: bisque;
  background-image: url('../../assets/dice.png');
  background-repeat: no-repeat;
  background-size: contain;
  background-position: center;
}

.log-panel .console-log__item .roll-text {
  padding: 0 10px;
  border-radius: 6px;
  line-height: 32px;
  background-color: aquamarine;
}

.log-panel .console-log__item .link {
  color: aquamarine;
  cursor: pointer;
}
</style>