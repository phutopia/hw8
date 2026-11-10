<script setup>
import { ref, computed } from 'vue'

const search = ref('')

const articles = [
  { title: 'Setting Up your First Vue3 Project - Vue 3.0 Release', url: 'https://vuejs.org/guide/quick-start.html' },
  { title: 'How to Add Drag and Drop to Your VueJS Project',     url: 'https://vuejs.org/guide/essentials/event-handling.html' },
  { title: 'How Vue3 is Designed for Both Hobby Devs and Large Projects', url: 'https://vuejs.org/guide/introduction.html' },
  { title: 'Getting Started with the Vue Composition API',        url: 'https://vuejs.org/guide/extras/composition-api-faq.html' },
  { title: 'A Beginner Guide to Vue Computed Properties',         url: 'https://vuejs.org/guide/essentials/computed.html' },
  { title: 'Understanding Vue Lifecycle Hooks',                   url: 'https://vuejs.org/guide/essentials/lifecycle.html' },
]

// articles whose title contains the search text (case-insensitive)
const filteredArticles = computed(() =>
  articles.filter(a => a.title.toLowerCase().includes(search.value.toLowerCase()))
)

function reset() {
  search.value = ''
}
</script>

<template>
  <h1>Filter Vue Articles</h1>

  <input type="text" v-model="search" placeholder="Search..." />
  <br /><br />
  <button @click="reset">Reset</button>

  <p v-if="search">Showing {{ filteredArticles.length }} results for "{{ search }}"</p>

  <ul class="list">
    <li v-for="article in filteredArticles" :key="article.url">
      <a :href="article.url" target="_blank">{{ article.title }}</a>
    </li>
  </ul>
</template>

<style scoped>
.list { list-style: none; padding: 0; border: 1px solid #ddd; border-radius: 6px; background: #f9f9f9; }
.list li { padding: 1.2rem 2rem; border-bottom: 1px solid #ddd; }
.list li:last-child { border-bottom: none; }
</style>