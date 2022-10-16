<script setup>
// This starter template is using Vue 3 <script setup> SFCs
// Check out https://vuejs.org/api/sfc-script-setup.html#script-setup
import { provide, reactive, shallowRef, computed, readonly } from 'vue'
import MainPanel from './components/main/index.vue'
import LogPanel from './components/log/index.vue'

const datas = reactive({
  /** 选中的职业列表 */
  dataCheckedClass  : new Set(),
  /** roll日志 */
  dataRollLog       : [],
  /** roll中的职业，因为可能会同时存在多个最高roll点，所有用array */
  dataRollClass     : [],
})

const panel = shallowRef(MainPanel)

function updateChecked (key) {
  if (datas.dataCheckedClass.has(key)) {
    datas.dataCheckedClass.delete(key)
  } else {
    datas.dataCheckedClass.add(key)
  }
}

function addRollLog (log) {
  datas.dataRollLog.push(log)
}

function setRollClass (classes) {
  datas.dataRollClass.push(...classes)
}

function switchPanel (panelKey) {
  const PanelMap = {
    'main'  : MainPanel,
    'log'   : LogPanel,
  }
  panel.value = PanelMap[panelKey]
}

function reset () {
  switchPanel('main')
  datas.dataCheckedClass.clear()
  datas.dataRollLog = []
  datas.dataRollClass = []
}

function roll () {
  const checked = datas.dataCheckedClass

  if (checked.size < 2) return alert('请至少选择两个首发职业OvO！')
  
  switchPanel('log')

  let time         = 2000
  let count        = 0
  let maxRoll      = 0
  let maxRollClass = []

  for (let item of checked) {
    const roll = Math.floor(Math.random() * 100 + 1)
    const upTime = Math.floor(Math.random() * 2 + 1)
    if (roll > maxRoll) {
      maxRoll = roll
      maxRollClass = [item]
    } else if (roll === maxRoll) {
      maxRollClass.push(item)
    }

    setTimeout(() => {
      count++

      addRollLog({ class: item, roll })

      if (count >= checked.size) {
        setRollClass(maxRollClass)
      }
    }, time);

    time += upTime * 1000
  }
}

provide('DATA_ROLL_LOG', {
  data: computed(() => datas.dataRollLog),
  set: addRollLog,
})

provide('DATA_ROLL_CLASS', {
  data: computed(() => datas.dataRollClass),
  set: setRollClass,
})

provide('DATA_CHECKED_CLASS', {
  data: readonly(datas.dataCheckedClass),
  set: updateChecked,
})

provide('FUNCTION', { roll, reset, switchPanel })

</script>

<template>
<div class="main">
  <div class="box">
    <transition name="fade" mode="out-in">
      <component :is="panel" />
    </transition>
    <div class="footer">
      <a href="https://github.com/miiiku/wow-classes-first" target="_blank">wow-first-classes</a>
    </div>
  </div>
</div>
</template>

<style scoped>

@media screen and (min-width: 768px) {
  .box {
    padding: 12px;
  }
}

@media screen and (max-width: 767px) {
  .box {
    padding: 6px;
  }
}

.fade-enter-active, .fade-leave-active {
  transition: opacity 0.5s ease;
}

.fade-enter-from, .fade-leave-to {
  opacity: 0;
}

.main {
  width: 100%;
  height: 100%;
  text-align: center;
}

.box {
  max-width: 1200px;
  margin: auto;
  padding-top: 8vh;
}

.footer {
  margin-top: 16px;
}
</style>
