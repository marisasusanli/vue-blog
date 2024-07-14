<script setup>
import { ref, computed } from 'vue';
import markdownit from 'markdown-it';
import moment from 'moment';

const props = defineProps({
  blog: {
    type: Object,
    required: true
  }
});

const readMore = ref(props.blog.readMore);

const TEXT_LENGTH_TO_DISPLAY = 80;

const hasLongText = computed(() => {
  const description = props.blog?.description;
  return description && description.split(" ")?.length > TEXT_LENGTH_TO_DISPLAY;
});

const transformDate = (isoDate) => {
  return moment(isoDate).format('MMMM Do, YYYY');
};

const transformMarkdown = (markdown) => {
  const md = markdownit({
    html: true,
    breaks: true
  });
  const result = md.render(markdown);
  return readMore.value ? result : result?.split(" ").slice(0, TEXT_LENGTH_TO_DISPLAY).join(" ");
};

</script>

<template>
  <div class="blog-post">
    <h2 class="blog-title">{{ blog?.title }}</h2>
    <p class="blog-date">{{ transformDate(blog?.sys?.firstPublishedAt) }}</p>
    <div v-if="!readMore">
      <p class="blog-text" v-html=transformMarkdown(blog?.description)></p>
      <span v-if="!readMore && hasLongText" class="expand" @click="readMore = !readMore">
        [...read more]
      </span>
    </div>
    <div v-if="readMore">
      <p class="blog-text-full" v-html=transformMarkdown(blog?.description)></p>
      <span class="expand" @click="readMore = !readMore">
        [...read less]
      </span>
    </div>
  </div>
</template>

<style scoped>

.blog-post {
  color: black;
  padding: 20px;
}

.blog-title {
  color: #7b6706;
  font-weight: bold;
  margin: 10px 0px;
  text-transform: lowercase;
}

.blog-date {
  margin: 10px 0px;
  color: #bb8588;
  font-weight: bold;
}

.blog-text {
  display: inline;
  white-space: pre-line;
}

.blog-text :deep(h2) {
  font-size: 1em;
  font-weight: bold;
}

.blog-text :nth-last-child(1) {
  display: inline;
}

.blog-text-full {
  white-space: pre-line;
}

.expand {
  color: #0b54a7;
  cursor: pointer;
}

</style>
