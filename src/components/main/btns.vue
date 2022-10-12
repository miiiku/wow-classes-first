<script setup>
import { inject } from "vue"

const checked      = inject('CHECKED_CLASS')
const addRollLog   = inject('ADD_ROLL_LOG')
const setRollClass = inject('SET_ROLL_CLASS')
const setShowPanel = inject('SET_SHOW_PANEL')

function handleRollOnly () {
  if (checked.size < 2) return alert('请至少选择两个首发职业OvO！')
  
  setShowPanel('log')

  let time         = 2000
  let count        = 0
  let maxRoll      = 0
  let maxRollClass = []

  for (let item of checked) {
    const roll = Math.floor(Math.random() * 100 + 1)
    const upTime = Math.floor(Math.random() * 3 + 2)
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

function handleRollTen () {

}

</script>

<template>
  <div class="btns-container">
    <button class="btn-item">
      <i class="btn-icon"></i>
      <span class="btn-text" @click="handleRollOnly">ROLL一次</span>
    </button>
    <button class="btn-item">
      <i class="btn-icon"></i>
      <span class="btn-text" @click="handleRollTen">ROLL十次</span>
    </button>
  </div>
</template>

<style scoped>
.btns-container {
  display: flex;
  gap: 24px;
  align-items: center;
  justify-content: center;
  margin-bottom: 24px;

}

.btns-container .btn-item {
  outline: none;
  border: 1px solid #f9f9f9;
  line-height: 56px;
  font-weight: bolder;
  background: #ffffff;
  box-shadow:  5px 5px 12px #d6d6d6,
              -5px -5px 12px #ffffff;
}

.btns-container .btn-item:hover {
  background: linear-gradient(145deg, #e6e6e6, #ffffff);
  box-shadow:  5px 5px 12px #d6d6d6,
              -5px -5px 12px #ffffff;
}

.btns-container .btn-icon {
  width: 56px;
  height: 56px;
  display: inline-block;
  background-image: url('../../assets/dice.png');
  background-repeat: no-repeat;
  background-position: center;
  background-size: 100%;
  vertical-align: middle;
  margin-right: 6px;
}
</style>