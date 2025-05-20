<script setup lang="ts">
import { CENTER_CRIMEA } from '~/lib/constants';
import { useMapStore } from '~/stores/map';

const colorMode = useColorMode();
const mapStore = useMapStore();
const style = computed(() =>
  colorMode.value === 'dark'
    ? '/styles/dark.json'
    : 'https://tiles.openfreemap.org/styles/liberty');

const zoom = 8;

onMounted(() => {
  mapStore.init();
});
</script>

<template>
  <MglMap
    :map-style="style"
    :center="CENTER_CRIMEA"
    :zoom="zoom"
  >
    <MglNavigationControl />
    <MglMarker v-for="point in mapStore.mapPoints" :key="point.id" :coordinates="[point.long, point.lat]">
      <template #marker>
        <div class="tooltip tooltip-top" :data-tip="point.label">
          <Icon
            name="tabler:map-pin-filled"
            size="24"
            class="text-primary"
          />
        </div>
      </template>
    </MglMarker>
  </MglMap>
</template>
