<script setup lang="ts">
import { MyButton } from "my-component-lib";
import { HCButton } from "my-component-lib";
import "/node_modules/my-component-lib/dist/style.css";
</script>

<template>
  <div><MyButton>Click me</MyButton></div>
  <div>
    <HCButton
      color="#EAEAEA"
      bgcolor="#CCCCCC"
      fontColor="#FF0000"
      title="Hello world!"
      fontWeight="normal"
      outlined
    />
  </div>
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
