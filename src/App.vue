<script setup>
import { RouterLink, RouterView } from 'vue-router';
import { ref, watchEffect } from 'vue';

const about = ref([]);
const blogs = ref([]);

watchEffect(async () => {
  const query = `{
    aboutMeCollection {
      items {
        sys {
          id
        }
        description
        photo {
          url
        }
      }
    }
    blogsCollection {
      items {
        sys {
          id
          firstPublishedAt
        }
        title
        slug
        description
      }
    }
  }`;

  const fetchUrl = `https://graphql.contentful.com/content/v1/spaces/${import.meta.env.VITE_CONTENTFUL_SPACE_ID}`;

  const fetchOptions = {
    method: "POST",
    headers: {
      Authorization: `Bearer ${import.meta.env.VITE_CONTENTFUL_ACCESS_TOKEN}`,
      "Content-Type": "application/json"
    },
    body: JSON.stringify({ query })
  };

  try {
    const response = await fetch(fetchUrl, fetchOptions).then(response =>
      response.json()
    );
    about.value = response.data?.aboutMeCollection?.items;
    blogs.value = response.data?.blogsCollection?.items?.map((blog) => { return {...blog, readMore: false}});
  } catch (error) {
    throw new Error("Error retrieving data from Contentful");
  }
});

</script>

<template>
  <header>
    <div class="header-content">
      <nav>
        <RouterLink class="nav-link" to="/">Home</RouterLink>
        <RouterLink class="nav-link" to="/about">About</RouterLink>
        <RouterLink class="nav-link" to="/blog">Blog</RouterLink>
      </nav>
    </div>
  </header>

  <RouterView :about="about" :blogs="blogs"/>
  <footer>
    <div class="footer-content">
      <div> 
        <a href="https://linkedin.com/in/marisa-susan-li" class="footer-link">
          <font-awesome-icon :icon="['fab', 'linkedin']" size="2x"/>
        </a> 
        <a href="https://github.com/marisasusanli" class="footer-link">
          <font-awesome-icon :icon="['fab', 'github']" size="2x" />
        </a> 
        <a href="mailto:marisa.susan.li@gmail.com" class="footer-link">
          <font-awesome-icon :icon="['fas', 'envelope']" size="2x" />
        </a> 
      </div>
      <p>© {{ new Date().getFullYear() }} Marisa Li </p>
    </div>
  </footer>
</template>

<style scoped>
header {
  padding: 2rem;
}

.header-content {
  max-width: 1280px;
  margin: auto;
  display: flex;
    justify-content: space-between;
    align-items: center;
}

nav {
  margin-left: auto;
  margin-right: 0;
}

.nav-link {
  color: #7b6706;
  text-decoration: none;
  padding: .5rem 1rem;
  margin: 1rem 1rem 1rem 0;
  display: inline-block;
  text-transform: lowercase;
}

.router-link-active {
  border: 1.5px solid #7b6706;
}

footer {
  color: white;
  font-size: 15px;
  font-family: sans-serif;
  padding: 1rem 1.5rem;
  background-color: #7b6706;
  position: relative;
  width: 100%;
}

.footer-content {
  display: flex;
  align-items: center;
  justify-content: space-between;
  max-width: 1280px;
  margin: auto;
}

.footer-content a {
  color: white;
}

.footer-link {
  margin: 0px 10px;
}

@media screen and (min-width: 992px) {
  .header-content {
    display: flex;
    justify-content: space-between;
    align-items: center;
  }
  .nav-link {
    margin: 0 .5rem;
  }
}

</style>
