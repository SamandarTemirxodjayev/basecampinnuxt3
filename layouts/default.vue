<template>
  <nav class="flex items-center justify-between flex-wrap bg-teal-500 p-6">
    <div class="flex items-center flex-shrink-0 text-white mr-6">
      <span class="font-semibold text-xl tracking-tight">
        <NuxtLink to="/">My Base Camp</NuxtLink>
      </span>
    </div>
    <div class="block lg:hidden">
      <button class="flex items-center px-3 py-2 border rounded text-teal-200 border-teal-400 hover:text-white hover:border-white">
        <svg class="fill-current h-3 w-3" viewBox="0 0 20 20" xmlns="http://www.w3.org/2000/svg"><title>Menu</title><path d="M0 3h20v2H0V3zm0 6h20v2H0V9zm0 6h20v2H0v-2z"/></svg>
      </button>
    </div>
    <div class="w-full block lg:flex lg:items-center lg:w-auto">
      <div class="text-sm lg:flex lg:items-center lg:w-auto">
        <div class="block mt-4 lg:inline-block lg:mt-0 text-white hover:text-white mr-4 text-2xl font-bold" @click="logout">Log out</div>
        <NuxtLink to="/create/project" class="block mt-4 lg:inline-block lg:mt-0 text-white hover:text-white text-2xl font-bold">
          Create a new project
        </NuxtLink>
      </div>
    </div>
  </nav>
</template>
<script setup>
function logout() {
  localStorage.removeItem("id");
  navigateTo('/login')
}
</script>
