<template>
  <div :class="['badge', `badge-${variant}`, `badge-${size}`]">
    <span class="badge-label">{{ label > 99 ? "99+" : label }}</span>
    <Icon
      v-if="icon.name"
      :icon="icon.name"
      class="badge-icon"
      :width="icon.size"
    />
  </div>
</template>

<script setup>
import { Icon } from "@iconify/vue";

const props = defineProps({
  label: {
    type: [String, Number], // Изменил тип, чтобы принимать и число
    required: true,
  },
  variant: {
    type: String,
    default: "primary",
  },
  size: {
    type: String,
    default: "medium",
  },
  icon: {
    type: Object,
    default: () => ({ name: "", size: 20 }),
  },
  iconSize: {
    type: [String, Number],
    default: 20,
  }
});
</script>