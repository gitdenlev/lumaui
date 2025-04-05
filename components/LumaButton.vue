<template>
  <button
    :class="[
      'button', 
      `button-${variant}`, 
      animation ? `animate__animated animate__${animation}` : ''
    ]"
    :disabled="disabled"
    @animationend="onAnimationEnd"
  >
    <slot></slot>
  </button>
</template>

<script setup>
import { ref, watch } from 'vue';

const props = defineProps({
  variant: {
    type: String,
    default: "aurora", // Кастомный стиль кнопки
  },
  disabled: {
    type: Boolean,
    default: false,
  },
  animation: {
    type: String, // Например: bounce, fadeIn, zoomIn
    default: "",
  },
});

const animationActive = ref(false);

function onAnimationEnd(event) {
  // Сбрасываем состояние после завершения анимации
  if (event.animationName === `animate__${props.animation}`) {
    animationActive.value = false;
  }
}

watch(
  () => props.animation,
  (newAnimation) => {
    if (newAnimation) {
      animationActive.value = true;
    }
  }
);
</script>
