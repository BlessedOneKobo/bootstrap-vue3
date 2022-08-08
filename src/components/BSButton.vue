<script setup lang="ts">
import { computed } from "vue";
import type { Nullable } from "@/types";

const {
  active = false,
  as = "button",
  disabled = false,
  href = undefined,
  size = undefined,
  type = "button",
  variant = "primary",
  bsPrefix = "btn",
} = defineProps<{
  active?: boolean;
  as?: "button" | "a";
  disabled?: boolean;
  href?: string;
  size?: "sm" | "lg";
  type?: Nullable<"button" | "reset" | "submit">;
  variant?:
    | "primary"
    | "secondary"
    | "success"
    | "danger"
    | "warning"
    | "info"
    | "dark"
    | "light"
    | "link"
    | "outline-primary"
    | "outline-secondary"
    | "outline-success"
    | "outline-danger"
    | "outline-warning"
    | "outline-info"
    | "outline-dark"
    | "outline-light"
    | "link";
  bsPrefix?: string;
}>();

const tagName = computed(() => (href && "a") || as);
const classList = computed(() => {
  const activeClass = active && "active";
  const btnSize = size && `btn-${size}`;
  const btnClass = `${bsPrefix}-${variant}`;
  return [activeClass, bsPrefix, btnSize, btnClass];
});
</script>

<template>
  <component :is="tagName" :class="classList" v-bind="{ disabled, href, type }">
    <slot></slot>
  </component>
</template>
