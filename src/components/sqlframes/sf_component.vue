<script setup lang="ts">
import { ref, inject, onMounted, onBeforeUnmount } from "vue";

const props = defineProps({ component: Object });

const root = ref(null);

const sf: any = inject("sf");
const { View } = sf.sqlframes;

onMounted(() => {
  View.render(root.value, props.component);
});

onBeforeUnmount(() => {
  View.render(root.value, null);
});
</script>

<template>
  <div ref="root" class="sf"></div>
</template>
