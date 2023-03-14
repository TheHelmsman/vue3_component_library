<script setup lang="ts">
import { MyButton } from "my-component-lib";
import { HCButton } from "my-component-lib";
import "/node_modules/my-component-lib/dist/style.css";
</script>

<template>
  <div><MyButton>Click me</MyButton></div>
  <div><HCButton title="Hello world!" /></div>
</template>

<style>
@import "./assets/base.css";

#app {
  max-width: 1280px;
  margin: 0 auto;
  padding: 2rem;
  font-weight: normal;
}
</style>
