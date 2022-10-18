<script setup>
import { computed, inject, nextTick, ref, watch } from "vue"
import ClassConfig from '@/constants/class'
import ClassTag from './tag.vue'
import BtnTag from './btn.vue'

const { data: rollLog }       = inject('DATA_ROLL_LOG')
const { data: rollClass }     = inject('DATA_ROLL_CLASS')
const { switchPanel, reset }  = inject('FUNCTION')

const panelScrollEl = ref(null)

const showResult = computed(() => {
  return rollClass.value && rollClass.value.length
})

watch(rollLog.value, () => {
  nextTick(() => {
    panelScrollEl.value.scrollIntoView({
      behavior: "smooth",
      block   : "center",
      inline  : "nearest",
    });
  })
})

function handleReset () {
  reset()
}

function handleGoLink (link) {
  console.log(link)
  window.open(link, '_blank')
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
        <template v-for="item in rollClass" :key="item">
          <div class="console-log__item">
            <div>结果已产生，你的首发职业为：</div>
            <class-tag :class-key="item" />
          </div>

          <div class="console-log__item">
            <btn-tag text="官方介绍" @click="handleGoLink(ClassConfig[item]?.link)" />
            <btn-tag text="NGA板块" @click="handleGoLink(ClassConfig[item]?.nga)" />
            <btn-tag text="不算，不算，重来OvO" @click="handleReset" />
          </div>
        </template>
      </template>

      <div class="hide-el" ref="panelScrollEl"></div>
    </div>
  </div>
</template>

<style scoped>

@media screen and (min-width: 768px) {
  .log-panel {
    padding: 16px 25px;
    height: 50vh;
  }
}

@media screen and (max-width: 767px) {
  .log-panel {
    padding: 16px 10px;
    height: 70vh;
  }
}

.log-panel {
  margin: 20px auto;
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
  flex-wrap: wrap;
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
  color: #333333;
}

.log-panel .console-log__item .link {
  color: aquamarine;
  cursor: pointer;
}
</style>