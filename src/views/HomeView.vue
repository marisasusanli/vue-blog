<script setup>
import 'vue3-carousel/dist/carousel.css';
import { Carousel, Slide } from 'vue3-carousel';

const slides = [
  { id: '1', title: 'lightly' },
  { id: '2', title: 'rarely' },
  { id: '3', title: 'archly' },
  { id: '4', title: 'quietly' },
  { id: '5', title: 'truthfully' },
  { id: '6', title: 'properly' },
  { id: '7', title: 'randomly' },
  { id: '8', title: 'vividly' },
  { id: '9', title: 'regretfully' },
  { id: '10', title: 'sincerely' },
];

const isAlternate = (id) => {
  return (id % 2 == 0);
};

</script>

<template>
  <main>
    <div class="carousel-container">
      <Carousel 
        :wrap-around="true" 
        :autoplay="2500" 
        :transition="1000"
      >
        <Slide v-for="slide in slides" :key="slide.id">
          <div 
            class="carousel-slide"
            :class="{ 'alternate-slide': isAlternate(slide.id) }"
          >
            <h3>{{ slide.title }}</h3>
          </div>
        </Slide>
      </Carousel>
    </div>
  </main>
</template>

<style scoped>
main {
  padding: 20px;
  min-height: 100vh;
  height: 100%;
  max-width: 1280px;
  margin: auto;
  display: flex;
  align-items: center;
  justify-content: center;
}

.carousel-container {
  width: 60%;
  margin-bottom: 250px;
}

.carousel-slide {
  min-height: 200px;
  min-width: 200px;
  border-radius: 8px;
  color: #7b6706;
  font-size: 30px;
  font-weight: 500;
  display: flex;
  justify-content: center;
  align-items: center;
}

.alternate-slide {
  color: #bb8588;
}

</style>
