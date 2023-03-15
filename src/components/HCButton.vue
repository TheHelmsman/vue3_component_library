<template>
  <div
    class="kms-ui-kit hc-button"
    :class="{ 'button--error': isError, 'button--disabled': isDisabled }"
    :style="cssVars"
  >
    <div class="title" :class="{ 'title--disabled': isDisabled }">
      {{ title }}
    </div>
  </div>
</template>

<script setup lang="ts">
import { computed } from "vue";

export interface Props {
  title?: string;
  outlined?: boolean;
  color?: string;
  bgcolor?: string;
  width?: string;
  height?: string;
  padding?: string;
  fontColor?: string;
  fontWeight?: string;
  isDisabled?: boolean;
  isError?: boolean;
  name: string;
}

const props = withDefaults(defineProps<Props>(), {
  name: "HCButton",
});

interface Style {
  [key: string]: string;
}

const cssVars = computed((): Style | undefined => {
  const result: unknown = {
    "--color": props.outlined ? props.bgcolor : props.color,
    "--bgcolor": props.outlined ? props.color : props.bgcolor,
    "--width": props.width ?? "auto",
    "--height": props.height ?? "48px",
    "--padding": props.padding ?? "0px 10px",
    "--fontcolor": getFontColor,
    "--fontWeight": props.fontWeight ?? "bold",
  };
  return result as Style;
});

const getFontColor = computed(() => {
  let result = props.color;
  if (props.outlined) {
    result = props.fontColor ? props.fontColor : props.bgcolor;
  }
  return result;
});
</script>

<style scoped lang="scss">
.hc-button {
  position: relative;
  display: inline-flex;
  align-items: center;
  justify-content: center;
  width: var(--width);
  height: var(--height);
  margin: 0 0 0 0;
  text-align: center;
  cursor: pointer;
  background-color: var(--bgcolor);
  border: 1px solid var(--color);
  border-radius: 4px;
  &--disabled {
    color: $light-grey;
    cursor: default;
    background-color: $background-beige;
    border: 1px solid $light-grey;
  }
  &--error {
    border: 1px solid $red;
  }
}
.title {
  display: inline-block;
  padding: var(--padding);
  font-weight: var(--fontWeight);
  color: var(--fontcolor);
  &--disabled {
    color: $light-grey;
  }
}
</style>
