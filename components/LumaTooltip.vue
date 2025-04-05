<template>
  <div
    class="tooltip-container"
    @mouseenter="showTooltip"
    @mouseleave="hideTooltip"
    @click="toggleTooltip"
  >
    <slot></slot>
    <transition name="fade">
      <div
        v-if="visible"
        :class="[
          'tooltip',
          `tooltip-${position}`,
          variant ? `tooltip-${variant}` : '',
          'tooltip-animate'
        ]"
        ref="tooltipRef"
      >
        {{ text }}
      </div>
    </transition>
  </div>
</template>

<script setup>
import { ref } from "vue";

const props = defineProps({
  text: {
    type: String,
    required: true,
  },
  position: {
    type: String,
    default: "top", // Варіанти: top, bottom, left, right
  },
  trigger: {
    type: String,
    default: "hover",
  },
  delay: {
    type: Number,
    default: 300, // Затримка в мс перед появою
  },
  variant: {
    type: String,
    default: "", // Варианты: aurora, nimbus, crimson и т.д.
  },
});

const visible = ref(false);
const tooltipTimeout = ref(null);

function showTooltip() {
  if (props.trigger === "hover") {
    tooltipTimeout.value = setTimeout(() => {
      visible.value = true;
    }, props.delay);
  }
}

function hideTooltip() {
  if (props.trigger === "hover") {
    clearTimeout(tooltipTimeout.value);
    visible.value = false;
  }
}

function toggleTooltip() {
  if (props.trigger === "click") {
    visible.value = !visible.value;
  }
}
</script>
