<template>
  <div>
    <div
      role="button"
      class="flex justify-start my-2 py-6 px-4 text-black text-sm"
      @click="toggle"
    >
      <slot name="item" />
      <span class="ml-auto">
        <angle-down-icon v-show="isActive" />
        <angle-right-icon v-show="!isActive" />
      </span>
    </div>
    <div
      id="accordion"
      ref="accordionRef"
      class="
        -mt-5
        overflow-hidden
        text-gray-600
        transition-height
        ease
        duration-300
      "
      :style="[isActive ? { height: computedHeight } : {}]"
    >
      <slot name="panel" />
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue';
import AngleDownIcon from './AngleDownIcon.vue';
import AngleRightIcon from './AngleRightIcon.vue';

const accordionRef = ref();
const computedHeight = ref('0');
const isActive = ref(false);

const toggle = () => {
  isActive.value = !isActive.value;
};

const initHeight = () => {
  accordionRef.value.style.height = 'auto';
  computedHeight.value = getComputedStyle(accordionRef.value).height;
  accordionRef.value.style.height = '0';
};

onMounted(initHeight);
</script>

<style scoped>
#accordion {
  height: 0;
  overflow: hidden;
  transition: 300ms;
}
</style>
