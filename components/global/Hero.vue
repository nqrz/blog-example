<template>
  <div
    class="
      flex flex-col
      justify-center
      items-center
      py-40
      px-2
      text-center
      bg-gray-600
      background
    "
  >
    <div class="bg-black bg-opacity-50 p-3 rounded">
      <slot />
    </div>
  </div>
</template>

<style scoped>
.background {
  background: url(https://source.unsplash.com/random/460x600/?nature) no-repeat bottom center / cover;
}
@media (min-width: 1024px) {
  .background {
    background: url(https://source.unsplash.com/random/1024x600/?nature) no-repeat bottom center / cover;
  }
}
@media (min-width: 1536px) {
  .background {
    background: url(https://source.unsplash.com/random/1536x600/?nature) no-repeat bottom center / cover;
  }
}
</style>