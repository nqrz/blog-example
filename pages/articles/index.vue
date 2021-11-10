<template>
  <div>
    <Hero>
      <h1>Articles</h1>
      <h4>This is Nizar Baihaqi's Blog Example</h4>
    </Hero>
    <Container>
      <Alert v-show="error !== ''">
        <p>{{ error }}</p>
        <button @click="resetError()">Ok</button>
      </Alert>
      <article v-for="(article, i) in data" :key="i">
        <Card :src=article.hero img="true">
          <h1>{{ article.title }}</h1>
          <p>{{ article.user.username }} {{ article.date }} <a @click="readPost(article)">Read more &rarr;</a></p>
        </Card>
      </article>
    </Container>
  </div>
</template>

<script>
export default {
  async asyncData({ $strapi, $md }) {
    const data = await $strapi.$articles.find();
    return { data };
  },
  data() {
    return {
      error: "",
    };
  },
  methods: {
    readPost(article) {
      if (this.$strapi.user) {
        this.error = "";
        this.$nuxt.$router.push(`/articles/${article.id}`);
      } else {
        this.error = "Please login to read articles";
      }
    },
    resetError() {
      this.error = "";
    },
  },
};
</script>