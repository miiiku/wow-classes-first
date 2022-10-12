<script setup>
import { computed } from "vue"
import ClassConfig from '@/constants/class'


const props = defineProps({
  classKey: {
    type: String,
    required: true
  }
})

const classInfo = computed(() => {
  return ClassConfig[props.classKey] || {}
})

</script>

<template>
  <div class="class-tag" :style="{ backgroundColor: classInfo.color }">
    <img :src="classInfo.icon" :alt="classInfo.title" />
    <span>{{ classInfo.title }}</span>
  </div>
</template>

<style scoped>
.class-tag {
  display: flex;
  align-items: center;
  padding: 0 6px;
  border-radius: 6px;
  line-height: 32px;
}

.class-tag img {
  width: 20px;
  height: 20px;
  margin-right: 6px;
}
</style>