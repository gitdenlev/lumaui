<script setup>
import {
  LumaButton,
  LumaBadge,
  LumaTooltip,
  LumaSwitch,
  LumaAlert,
} from "./index.ts";
import "animate.css";
import { ref } from "vue";

const isChecked = ref(false);
</script>

<template>
  <div>
    <h1>Buttons</h1>
    <LumaButton variant="halo" animation="fadeInTopLeft">Halo</LumaButton>
    <LumaButton variant="aurora">Aurora</LumaButton>
    <LumaButton variant="verdant">Verdant</LumaButton>
    <LumaButton variant="crimson">Crimson</LumaButton>
    <LumaButton variant="nimbus">Nimbus</LumaButton>
    <LumaButton variant="azure">Azure</LumaButton>
    <LumaButton variant="solaris">Solaris</LumaButton>
    <LumaButton variant="obsidian">Obsidian</LumaButton>
    <LumaButton variant="ivory" disabled>Ivory</LumaButton>

    <h1>Badges</h1>
    <LumaBadge
      label="New"
      variant="success"
      :icon="{
        name: 'ic:round-check',
        size: 30,
      }"
      size="large"
    />

    <h1>Tooltip</h1>
    <div class="tooltip-container">
      <LumaTooltip text="Bottom" trigger="hover" position="right" variant="default">
        <LumaBadge label="Tooltip" variant="danger" />
      </LumaTooltip>
    </div>

    <h1>Switch</h1>
    <LumaSwitch v-model="isChecked" variant="info" />
    <LumaAlert
      message="This is an alert message!"
      :icon="{ name: '', size: 20 }"
      animation="zoom"
    />
  </div>
</template>
