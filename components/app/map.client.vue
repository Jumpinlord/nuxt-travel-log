<script setup lang="ts">
import { CENTER_CRIMEA } from '~/lib/constants';

const colorMode = useColorMode();
const style = computed(() =>
  colorMode.value === 'dark'
    ? '/styles/dark.json'
    : 'https://tiles.openfreemap.org/styles/liberty');

const zoom = 8;
</script>

<template>
  <MglMap
    :map-style="style"
    :center="CENTER_CRIMEA"
    :zoom="zoom"
  >
    <MglNavigationControl />
  </MglMap>
</template>
