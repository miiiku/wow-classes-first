<script setup>
import { inject } from "vue"

const { roll } = inject('FUNCTION')


function handleRollOnly () {
  roll()
}

</script>

<template>
  <div class="btns-container">
    <button class="btn-item" @click="handleRollOnly">
      <i class="btn-icon"></i>
      <span class="btn-text">R O L L</span>
    </button>
  </div>
</template>

<style scoped>

@media screen and (min-width: 768px) {
  .btns-container {
    margin-bottom: 24px;
  }
}

@media screen and (max-width: 767px) {
  .btns-container {
    margin-bottom: 12px;
  }
}

.btns-container {
  display: flex;
  align-items: center;
  justify-content: center;

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
  width: 48px;
  height: 48px;
  display: inline-block;
  background-image: url('../../assets/dice.png');
  background-repeat: no-repeat;
  background-position: center;
  background-size: 100%;
  vertical-align: middle;
  margin-right: 6px;
}
</style>