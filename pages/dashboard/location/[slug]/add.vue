<script lang="ts" setup>
import type { InsertLocationLog } from '~/lib/db/schema';

import { CENTER_CRIMEA } from '~/lib/constants';

const route = useRoute();
const { currentLocation } = useLocationStore();

const { $csrfFetch } = useNuxtApp();

async function onSubmit(values: InsertLocationLog) {
  await $csrfFetch(`/api/locations/${route.params.slug}/add`, {
    method: 'post',
    body: values,
  });
}

function submitComplete() {
  navigateTo({
    name: 'dashboard-location-slug',
    params: {
      slug: route.params.slug,
    },
  });
}
</script>

<template>
  <div>
    <h2>Location Log Add Page!</h2>
    <LocationLogForm
      submit-label="Add Location Log"
      submit-icon="tabler:map-pin-plus"
      :on-submit="onSubmit"
      :on-submit-complete="submitComplete"
      :initial-values="{
        name: '',
        description: '',
        startedAt: Date.now() - (24 * 60 * 60 * 1000),
        endedAt: Date.now(),
        long: currentLocation?.long || (CENTER_CRIMEA as [number, number])[0],
        lat: currentLocation?.lat || (CENTER_CRIMEA as [number, number])[1],
      }"
    />
  </div>
</template>
