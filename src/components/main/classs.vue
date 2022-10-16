<script setup>
import { computed, inject } from 'vue'
import ClassConfig from '@/constants/class'

const { data: checked, set: updateChecked } = inject('DATA_CHECKED_CLASS')

const frameStyle = computed(() => {
  return function (key) {
    return { backgroundColor: ClassConfig[key].color }
  }
})

const isChecked = computed(() => {
  return function (key) {
    return checked.has(key)
  }
})

const handleClick = (key) => {
  updateChecked(key)
}

</script>

<template>
  <div class="class-container">
    <template v-for="key in Object.keys(ClassConfig)" :key="key">
      <div class="wow-class-frame" :class="{ checked: isChecked(key) }" :style="frameStyle(key)" @click="handleClick(key)">
        <div class="wow-class__icon"><img :src="ClassConfig[key].icon" :alt="ClassConfig[key].title"></div>
        <div class="wow-class__title">{{ ClassConfig[key].title }}</div>
        <div class="wow-class__checked" v-if="isChecked(key)">
          <i class="icon-checked"></i>
        </div>
      </div>
    </template>
  </div>
</template>

<style scoped>

@media screen and (min-width: 768px) {
  .class-container {
    gap: 12px;
    grid-template-columns: repeat(4, 1fr);
    grid-template-rows: repeat(3, 1fr);
  }

  .wow-class-frame {
    gap: 16px;
    height: 160px;
  }

  .wow-class__icon {
    width: 64px;
    height: 64px;
  }

  .wow-class__title {
    width: 110px;
    font-size: 24px;
  }
}

@media screen and (max-width: 767px) {
  .class-container {
    gap: 6px;
    grid-template-columns: repeat(3, 1fr);
    grid-template-rows: repeat(4, 1fr);
  }

  .wow-class-frame {
    gap: 6px;
    height: 86px;
  }

  .wow-class__icon {
    width: 32px;
    height: 32px;
  }

  .wow-class__title {
    width: 18vw;
    font-size: 16px;
  }
}
.class-container {
  display: grid;
}

.wow-class-frame {
  position: relative;
  overflow: hidden;
  display: flex;
  align-items: center;
  justify-content: center;
  border-radius: 4px;
  overflow: hidden;
  box-shadow: 0 1px 2px rgba(0, 0, 0, 0.4);
  cursor: pointer;
  user-select: none;
}

.wow-class__icon {
  transition: transform 0.3s ease;
}

.wow-class__icon img {
  display: block;
  width: 100%;
  height: 100%;
  object-fit: cover;
  -webkit-user-drag: none;
}

.wow-class__title {
  color: #000000;
  font-weight: bolder;
  text-align: left;
  text-shadow: 1px 1px 1px rgba(255, 255, 255, 0.5);
}

.wow-class-frame.checked .wow-class__checked {
  display: flex;
  align-items: center;
  position: absolute;
  bottom: -21px;
  right: 0px;
  width: 22px;
  height: 42px;
  transform-origin: right center;
  transform: rotateZ(45deg);
  background-color: #38E54D;
}

.wow-class-frame.checked .wow-class__checked .icon-checked {
  width: 16px;
  height: 16px;
  display: block;
  background-image: url('../../assets/checked.png');
  background-repeat: no-repeat;
  background-size: contain;
  background-position: center;
  transform: rotateZ(-45deg);
}

.wow-class-frame:hover .wow-class__icon {
  transform: scale(1.15);
}
</style>