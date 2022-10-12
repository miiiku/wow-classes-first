<script setup>
// This starter template is using Vue 3 <script setup> SFCs
// Check out https://vuejs.org/api/sfc-script-setup.html#script-setup
import { provide, reactive, ref, shallowRef } from 'vue'
import MainPanel from './components/main/index.vue'
import LogPanel from './components/log/index.vue'
import ResultPanel from './components/result/index.vue'
import ClassConfig from './constants/class'

const datas = reactive({
  /** 选中的职业列表 */
  checkedClass: new Set(),
  /** roll日志 */
  rollLog: [],
  /** roll中的职业，因为可能会同时存在多个最高roll点，所有用array */
  rollClass: [],
})

  /** 展示首页面板 */
const showMainPanel = ref(true)
  /** 展示日志面板 */
const showLogPanel = ref(false)
  /** 展示结果面板 */
const showResultPanel = ref(false)

const panel = shallowRef(MainPanel)

function updateChecked (key) {
  if (datas.checkedClass.has(key)) {
    datas.checkedClass.delete(key)
  } else {
    datas.checkedClass.add(key)
  }
}

function addRollLog (log) {
  datas.rollLog.push(log)
}

function setRollClass (data) {
  datas.rollClass.push(...data)
}

function setShowPanel (panelKey) {
  const PanelMap = {
    'main'  : MainPanel,
    'log'   : LogPanel,
    'result': ResultPanel,
  }
  panel.value = PanelMap[panelKey]
}

provide('ROLL_LOG', datas.rollLog)
provide('ROLL_CLASS', datas.rollClass)
provide('CHECKED_CLASS', datas.checkedClass)

provide('UPDATE_CHECKED_CLASS', updateChecked)
provide('ADD_ROLL_LOG', addRollLog)
provide('SET_ROLL_CLASS', setRollClass)
provide('SET_SHOW_PANEL', setShowPanel)

</script>

<template>
<div class="main">
  <h1 class="page-title">WOW首发职业模拟器</h1>
  <div class="box">
    <transition name="fade" mode="out-in">
      <component :is="panel" />
    </transition>
  </div>
</div>
</template>

<style scoped>
.fade-enter-active, .fade-leave-active {
  transition: opacity 0.5s ease;
}

.fade-enter-from, .fade-leave-to {
  opacity: 0;
}

.main {
  width: 100%;
  height: 100%;
}

.box {
  max-width: 1200px;
  margin: auto;
}

.page-title {
  text-align: center;
  font-weight: bolder;
}
</style>
