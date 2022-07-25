<script setup lang="ts">
import { inject } from "vue";
import SFComponent from "./sf_component.vue";

const sf: any = inject("sf");

const { DataFrame, SQL, Time, View } = sf.sqlframes;
const df = DataFrame.fromURL(
  "https://earthquake.usgs.gov/earthquakes/feed/v1.0/summary/all_month.csv"
);
</script>

<template>
  <SFComponent :component="df" />
</template>
