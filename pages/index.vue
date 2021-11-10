<template>
  <div>
    <Hero>
      <h1>Hehei not bad</h1>
      <h4>This is Nizar Baihaqi's Blog Example</h4>
    </Hero>
    <Container>
      <Card v-if="$strapi.user !== null">
        <h5>Hello {{ $strapi.user.username }}! Welcome back</h5>
      </Card>
      <Card src="https://source.unsplash.com/random/1024x300/?nature" img="true">
        <p class="text-center">Card with image</p>
      </Card>
      <h3>Example user</h3>
      <p>email: john@nizarbaihaqi.com</p>
      <p>password: 12345678</p>
      <p>email: jane@nizarbaihaqi.com</p>
      <p>password: 12345678</p>
    </Container>
  </div>
</template>

<script>
</script>