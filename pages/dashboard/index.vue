<script setup lang="ts">
import { useLocationStore } from '~/stores/locations';

const mapStore = useMapStore();

const locationsStore = useLocationStore();
const { locations, status } = storeToRefs(locationsStore);

onMounted(() => {
  locationsStore.refresh();
});
</script>

<template>
  <div class="p-4">
    <h2 class="text-2xl">
      Locations
    </h2>
    <div v-if="status === 'pending'">
      <span class="loading loading-spinner loading-xl" />
    </div>
    <div
      v-else-if="locations && locations.length > 0"
      class="flex flex-nowrap gap-2 mt-4 overflow-auto"
    >
      <article
        v-for="location in locations"
        :key="location.id"
        class="card card-compact overflow-auto border w-72 min-h-40 mb-2 bg-base-300 shrink-0 hover:cursor-pointer"
        :class="{
          'border-accent': location === mapStore.selectedPoint,
          'border-transparent': location !== mapStore.selectedPoint,
        }"
        @mouseenter="mapStore.selectedPoint = location"
        @mouseleave="mapStore.selectedPoint = null"
      >
        <div class="card-body">
          <h3 class="text-xl">
            {{ location.name }}
          </h3>
          <p>{{ location.description }}</p>
        </div>
      </article>
    </div>
    <div v-else class="flex flex-col gap-2 mt-4">
      <p>
        Add a location to get started
      </p>
      <NuxtLink to="/dashboard/add" class="btn btn-primary w-40">
        Add Location
        <Icon name="tabler:circle-plus-filled" size="24" />
      </NuxtLink>
    </div>
  </div>
</template>
