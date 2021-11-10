<template>
  <div>
    <Container>
      <h1 class="border-b-2 border-gray-100 pb-5">Sign up</h1>
      <Alert v-show="error !== ''" class="max-w-screen-md">
        <p>{{ error }}</p>
      </Alert>
      <form @submit="createUser" class="mb-2 max-w-screen-md mx-auto">
        <div class="flex flex-col mt-5">
          <label for="email">Email</label>
          <input
            type="email"
            v-model="email"
            placeholder="ex. doe@onepiece.xyz"
            class=""
          />
        </div>
        <div class="flex flex-col">
          <label for="username">Username</label>
          <input
            type="username"
            v-model="username"
            placeholder="ex. superdoe"
          />
        </div>
        <div class="flex flex-col">
          <label for="password">Password</label>
          <input type="password" v-model="password" />
        </div>
        <div class="flex justify-end py-2">
          <button
            :disabled="email === '' || password === '' || username === ''"
            type="submit"
            class="py-2"
          >
            Signup
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
      email: "",
      username: "",
      password: "",
      error: "",
    };
  },
  methods: {
    async createUser(e) {
      e.preventDefault();
      try {
        const newUser = await this.$strapi.register({
          email: this.email,
          username: this.username,
          password: this.password,
        });
        console.log(newUser);
        if (newUser !== null) {
          this.error = "";
          this.$nuxt.$router.push("/articles");
        }
      } catch (error) {
        this.error = error.message;
      }
    },
  },
  middleware: "authenticated",
};
</script>