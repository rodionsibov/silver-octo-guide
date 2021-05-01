<template>
  <div class="h-screen w-screen bg-purple-800">
    <div class="p-14">
      <router-link class="flex justify-center text-4xl text-yellow-400" to="/">
        User<span class="font-bold text-purple-100">Picker</span>
      </router-link>
    </div>
    <router-view />
  </div>
</template>

