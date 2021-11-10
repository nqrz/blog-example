<template>
  <div class="bg-gray-900 sticky top-0">
    <div
      class="
        flex
        justify-between
        items-center
        max-w-screen-lg
        mx-auto
        py-2
        px-3
      "
    >
      <NuxtLink class="text-gray-300 hover:text-white" to="/">Home</NuxtLink>
      <div class="flex items-center">
        <NuxtLink class="text-gray-300 hover:text-white" to="/articles">Articles</NuxtLink>
        <div v-if="$strapi.user === null" class="">
          <!-- <NuxtLink class="text-gray-300 hover:text-white ml-3" to="/user/signup">
            <button>Signup</button>
          </NuxtLink> -->
          <NuxtLink class="text-gray-300 hover:text-white ml-3" to="/user/login">
            <button>Login</button>
          </NuxtLink>
        </div>
        <div v-else-if="$strapi.user !== null">
          <NuxtLink class="text-gray-300 hover:text-white ml-3" to="/user">
            Profile
          </NuxtLink>
          <NuxtLink class="text-gray-300 hover:text-white ml-3" to="/articles/create">
            <button>
              Write +
            </button>
          </NuxtLink>
          <button @click="logout" class="ml-3">Logout</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  methods: {
    async logout() {
      await this.$strapi.logout();
      this.$nuxt.$router.push("/");
    },
  },
};
</script>