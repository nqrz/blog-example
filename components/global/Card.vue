<template>
  <div class="bg-gray-200 text-black lg:rounded-lg my-2 overflow-hidden">
    <img :src="src" v-show="img" alt="Nature photo from unsplash">
    <div class="py-1 px-4">
      <slot />
    </div>
  </div>
</template>

<script>
export default {
  props: {
    src: String,
    img: Boolean
  }
}
</script>