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
  }
  // created() {
  //   this.$store.dispatch("getPosts");
  // }
};
</script>
