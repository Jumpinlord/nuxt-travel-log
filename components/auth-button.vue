<script setup lang="ts">
const authStore = useAuthStore();
</script>

<template>
  <!-- <div v-if="!authStore.loading && authStore.user" class="dropdown">
    <div tabindex="0" role="button" class="btn m-1">
      {{ authStore.user.name }}
    </div>
    <ul tabindex="0" class="dropdown-content menu bg-base-100 rounded-box z-1 w-52 p-2 shadow-sm">
      <li><a>Item 1</a></li>
      <li><a>Item 2</a></li>
    </ul>
  </div> -->
  <div v-if="!authStore.loading && authStore.user">
    <button class="btn" popovertarget="popover-signin" style="anchor-name:--anchor-signin">
      <div v-if="authStore.user.image" class="avatar">
        <div class="w-7 rounded-full">
          <img :src="authStore.user.image" :alt="authStore.user.name">
        </div>
      </div>
      {{ authStore.user.name }}
    </button>
    <ul id="popover-signin" class="dropdown dropdown-end menu w-44 mt-1 rounded-sm bg-slate-100 shadow-sm" popover style="position-anchor:--anchor-signin">
      <li class=" dark:text-slate-800 hover:bg-indigo-100 rounded-sm font-semibold">
        <NuxtLink to="/sign-out">
          <Icon name="tabler:logout-2" size="20" />
          Sign Out
        </NuxtLink>
      </li>
    </ul>
  </div>
  <button v-else :disabled="authStore.loading" class="btn btn-accent" @click="authStore.signIn">
    Sign In With GitHub
    <span v-if="authStore.loading" class="loading loading-spinner loading-md" />
    <Icon v-else name="tabler:brand-github" size="24" />
  </button>
</template>
