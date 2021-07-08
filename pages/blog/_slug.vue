<template>
  <main class="post individual">
    <h1 v-if="post">{{ post.title.rendered }}</h1>
    <small class="date" v-if="post">{{ post.date | dateformat }}</small>
    <section v-html="post.content.rendered" v-if="post"></section>
  </main>
</template>

<script>
export default {
  computed: {
    posts() {
      return this.$store.state.posts;
    },
    post() {
      return this.posts.find(el => el.slug === this.slug);
    }
  },
  data() {
    return {
      slug: this.$route.params.slug
    };
  },

  async fetch() {
    this.data = await fetch(
      "https://css-tricks.com/wp-json/wp/v2/posts?page=1&per_page=20&_embed=1"
    ).then(res => res.json());
    this.$store.dispatch("test", this.data);
  }
};
</script>
