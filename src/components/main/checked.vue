<script setup>
import { computed, inject } from "vue"
import ClassConfig from '@/constants/class'

const { data: checked, set: updateChecked } = inject('DATA_CHECKED_CLASS')

const handleDel = key => {
  updateChecked(key)
}

</script>

<template>
  <div class="checked-container">
    <template v-if="checked.size > 0">
      <div class="checked-item" v-for="key in checked.values()" :key="key" :style="{ color: ClassConfig[key].color }">
        <span>{{ ClassConfig[key].title }}</span>
        <span class="checked-item__close" @click="handleDel(key)"></span>
      </div>
    </template>
    <template v-else>
      <div class="checked-item">还未选择首发职业哦OvO!</div>
    </template>
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

.checked-container {
  width: 100%;
  display: flex;
  flex-wrap: wrap;
  gap: 12px;
  align-items: center;
  justify-content: center;
  margin-bottom: 24px;
  font-weight: bolder;
}

.checked-container .checked-item {
  position: relative;
  padding: 4px 12px;
  background-color: #cdcdcd;
  border-radius: 4px;
  text-shadow: 1px 1px 1px rgba(0, 0, 0, 0.5);
}

.checked-container .checked-item .checked-item__close {
  position: absolute;
  right: -5px;
  top: -5px;
  width: 16px;
  height: 16px;
  border-radius: 50%;
  box-sizing: border-box;
  background-color: #554d4d;
  background-image: url('../../assets/close.svg');
  background-repeat: no-repeat;
  background-position: center;
  background-size: 76%;
  cursor: pointer;
}
</style>