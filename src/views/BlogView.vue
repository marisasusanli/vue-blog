<script setup>
import BlogPost from '../components/BlogPost.vue';

defineProps({
  blogs: {
    type: Array,
    required: true
  }
});

</script>

<template>
  <main>
    <ul class="blogs">
      <li v-for="blog in blogs" :key="blog.sys.id" class="blog-container">
        <BlogPost :blog="blog"/>
      </li>
    </ul>
  </main>
</template>

<style scoped>

main {
  min-height: 100vh;
  flex: 1;
}

.blogs {
  display: flex;
  flex-wrap: wrap;
  list-style: none;
  padding: 0;
  margin: auto;
  max-width: 1280px;
}

.blog-container {
  margin: 20px 100px;
}

@media (width <= 480px) {
  .blog-container {
    margin: 0.5rem 1.5rem;
  }
}

</style>
