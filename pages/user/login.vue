<template>
  <div>
    <Container>
      <h1 class="border-b-2 border-gray-100 pb-5">Login</h1>
      <form @submit="loginUser" class="mb-2 max-w-screen-md mx-auto">
        <Alert v-show="error !== ''" class="max-w-screen-md">
          <p>{{ error }}</p>
        </Alert>
        <div class="flex flex-col mt-5">
          <label for="email">Email</label>
          <input
            type="email"
            v-model="identifier"
            placeholder="ex. doe@onepiece.xyz"
          />
        </div>
        <div class="flex flex-col">
          <label for="password">Password</label>
          <input type="password" v-model="password" />
        </div>
        <div class="flex justify-end py-2">
          <button
            :disabled="identifier === '' || password === ''"
            type="submit"
            class="py-2"
          >
            Login
          </button>
        </div>
      </form>
    </Container>
  </div>
</template>

<script>
export default {
  data() {
    return {
      identifier: "",
      password: "",
      error: "",
    };
  },
  methods: {
    async loginUser(e) {
      e.preventDefault();
      try {
        const user = await this.$strapi.login({
          identifier: this.identifier,
          password: this.password,
        });
        console.log(user);
        if (user !== null) {
          this.error = "";
          this.$nuxt.$router.push("/articles");
        }
      } catch (error) {
        this.error = "error in login credentials";
      }
    },
  },
  middleware: "authenticated",
};
</script>