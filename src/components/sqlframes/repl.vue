<script setup lang="ts">
import { inject } from "vue";
import SFComponent from "./sf_component.vue";

const sf: any = inject("sf");

const { REPL } = sf.repl;
const repl = new REPL();
</script>

<template>
  <SFComponent :component="repl" />
</template>
