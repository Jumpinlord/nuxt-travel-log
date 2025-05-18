<script setup lang="ts">
const { data, status } = await useFetch('/api/locations', {
  lazy: true,
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
      v-else-if="data && data.length > 0"
      class="flex flex-wrap gap-2 mt-4"
    >
      <article v-for="location in data" :key="location.id" class="card card-compact w-72 min-h-40 bg-base-300">
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
