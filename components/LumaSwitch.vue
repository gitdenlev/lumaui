<template>
  <div
    :class="[
      'switch',
      `switch-${variant}`,
      { 'switch-checked': modelValue, 'switch-disabled': disabled },
    ]"
    @click="toggleSwitch"
    :aria-checked="modelValue.toString()"
    role="switch"
    :aria-disabled="disabled.toString()"
  >
    <div class="switch-track">
      <div class="switch-thumb"></div>
    </div>
  </div>
</template>

<script setup>
import { defineProps, defineEmits } from "vue";

const props = defineProps({
  modelValue: {
    type: Boolean,
    default: false,
  },
  disabled: {
    type: Boolean,
    default: false,
  },
  variant: {
    type: String,
    default: "default",
  },
});

const emit = defineEmits(["update:modelValue"]);

function toggleSwitch() {
  if (!props.disabled) {
    emit("update:modelValue", !props.modelValue);
  }
}
</script>
