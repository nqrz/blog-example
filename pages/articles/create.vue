<template>
  <Container>
    <h1 class="border-b-2 border-gray-100 pb-5">Create post</h1>
    <form ref="form" @submit="createPost" class="max-w-screen-lg flex flex-col mt-3">
      <input v-model="form.title" name="title" type="text" placeholder="title"/>
      <input v-model="form.description" name="description" type="text" placeholder="description"/>
      <textarea v-model="form.content" name="content" cols="30" rows="10" class="my-3 rounded-lg bg-gray-600 p-2"></textarea>
      <div class="flex justify-end py-3">
        <button :disabled=" form.title === '' || form.description === '' || form.content === ''" type="submit">
          Create
        </button>
      </div>
    </form>
  </Container>
</template>

<script>
export default {
  data() {
    return {
      form: {
        title: "",
        description: "",
        content: "",
        users_permissions_user: this.$strapi.user,
      }
    };
  },
  methods: {
    async createPost(e) {
      const formData = new FormData();
      let file;
      const formElements = this.$refs.form.elements;
      formElements.forEach((el, i) => {
        if (el.type === "file") {
          file = el.files[0];
        }
      });
      formData.append(`files.image`, file, file.name);
      formData.append("data", JSON.stringify(this.form));
      e.preventDefault();
      await this.$strapi.$articles.create(formData);
      this.$nuxt.$router.push("/articles");
    },
  },
  middleware({ $strapi, redirect }) {
    if (!$strapi.user) {
      redirect("/articles");
    }
  },
};
</script>