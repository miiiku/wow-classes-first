<script setup>
import { computed } from "vue"


const props = defineProps({
  text: {
    type: String,
    required: true
  },
  backgroundColor: {
    type: String,
  },
  color: {
    type: String,
  }
})

const tagStyle = computed(() => {
  const style = {}
  if (props.backgroundColor) {
    style.backgroundColor = props.backgroundColor
  }
  if (props.color) {
    style.color = props.color
  }
  return style
})

</script>

<template>
  <div class="btn-tag" :style="tagStyle">
    <span>{{ props.text }}</span>
  </div>
</template>

<style scoped>
.btn-tag {
  user-select: none;
  padding: 0 6px;
  border-radius: 6px;
  line-height: 32px;
  background-color: #FF577F;
  color: #FFFFFF;
  cursor: pointer;
  box-shadow: 0 0 6px #FF577F;
}
</style>