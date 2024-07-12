<script setup>
import { computed } from 'vue';

const props = defineProps({
  about: {
    type: Array,
    required: true
  },
});

const aboutMeText = computed(() => {
  const description = props.about[0]?.description?.split("history.");
  return description[0] + "history." || '';
});

const aboutMeTextContinued = computed(() => {
  const description = props.about[0]?.description?.split("history.");
  return description[1] || '';
});

const getImgUrl = () => {
  return props.about[0]?.photo.url;
};

</script>

<template>
  <main>
    <section class="profile">
      <div class="profile-pic">
        <img :src="getImgUrl()" class="pic"/>
      </div>
      <div class="description">
        <h2 class="header">I'm Marisa</h2>
        <p>{{ aboutMeText }}</p>
        <p class="text-continued">{{ aboutMeTextContinued }}</p>
      </div>
    </section>
  </main>
</template>

<style scoped>
main {
  padding: 30px;
  min-height: 100vh;
  max-width: 1280px;
  margin: auto;
}

.profile {
  display: flex;
  justify-content: space-around;
  flex-wrap: wrap;
  margin: 2em 0;
}

.profile-pic {
  display: flex;
  justify-content: center;
  align-items: center;
}

.pic {
  max-width: 350px;
}

.description {
  margin-top: -10px;
  padding: 0px 20px;
  max-width: 60%;
}

.header {
  color: #7b6706;
  font-weight: bold;
  margin-bottom: 10px;
  text-transform: lowercase;
}

.text-continued {
  margin-top: 15px;
}

@media (width <= 480px) {
  .pic {
    max-width: 70%;
    margin-bottom: 2rem;
  }

  .description {
    max-width: 95%;
  }
}

@media (width <= 992px) {
  .pic {
    max-width: 60%;
    margin-bottom: 2rem;
  }

  .description {
    max-width: 95%;
  }
}

</style>
