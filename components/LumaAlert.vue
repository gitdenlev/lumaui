<script setup>
import { ref, watch } from "vue";
import { Icon } from "@iconify/vue/dist/iconify.js";
const props = defineProps({
  message: {
    type: String,
    default: "This is an alert message!",
  },
  variant: {
    type: String,
    default: "primary", // Варіанти кольору: primary, success, danger, warning, info
  },
  position: {
    type: String,
    default: "bottom-right", // Варіанти позиції: top-left, top-right, bottom-left, bottom-right, top-center, bottom-center
  },
  duration: {
    type: Number,
    default: 5000, // Час (мс), після якого alert зникне автоматично
  },
  closePosition: {
    type: String,
    default: "top-right", // Позиція кнопки закриття: top-left, top-right, bottom-left, bottom-right
  },
   closeIcon: {
    type: Object,
    default: () => ({ name: "material-symbols-light:close", size: 20 }),
  },
  animation: {
    type: String,
    default: "fade",
  }
});

const visible = ref(true);

function closeAlert() {
  visible.value = false;
}

watch(
  () => visible.value,
  (newVal) => {
    if (newVal && props.duration > 0) {
      setTimeout(() => {
        closeAlert();
      }, props.duration);
    }
  },
  { immediate: true }
);
</script>

<template>
  <transition :name="animation">
    <div
      v-if="visible"
      :class="['alert', `alert-${variant}`, `alert-${position}`]"
    >
      <slot>{{ message }}</slot>
      <Icon
        @click="closeAlert"
        :class="`alert-close-${closePosition}`"
        class="alert-close"
        :icon="closeIcon.name"
        :width="closeIcon.size"
      />
    </div>
  </transition>
</template>
