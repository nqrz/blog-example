<template>
  <div>
    <Hero>
      <h1>{{ article.title }}</h1>
    </Hero>
    <article>
      <Container>
        <p>Author: {{ article.user.username }}</p>
        <p>Published: {{ article.date }}</p>
        <div v-html="$md.render(article.content)"></div>
        <button
          v-if="$strapi.user && article.user.id === $strapi.user.id"
          @click="deletePost"
        >
          Delete
        </button>
      </Container>
    </article>
  </div>
</template>

<script>
export default {
  async asyncData({ $strapi, route }) {
    const id = route.params.id;
    const article = await $strapi.$articles.findOne(id);
    console.log(article);
    return { article };
  },
  methods: {
    async deletePost(id) {
      await this.$strapi.articles.delete(id);
      this.nuxt.$router.push("/articles");
    },
  },
  middleware({ $strapi, redirect }) {
    if ($strapi.user === null) {
      redirect("/articles");
    }
  },
};
</script>