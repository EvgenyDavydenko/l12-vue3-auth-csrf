<script setup>
import { onMounted, ref } from 'vue'
import axios from 'axios'

const posts = ref([])
const pagination = ref({})

const fetchPosts = async (url = '/api/posts') => {
  try {
    const response = await axios.get(url)
    posts.value = response.data.posts.data
    pagination.value = {
      next_page_url: response.data.posts.next_page_url,
      prev_page_url: response.data.posts.prev_page_url,
      last_page: response.data.posts.last_page,
      current_page: response.data.posts.current_page
    }
  } catch (error) {
    console.error('Ошибка при загрузке постов:', error)
  }
}
onMounted(() => {
  fetchPosts()
})
</script>

<template>
  <div class="container py-4">
    <h1 class="text-center mb-5 fw-light">Мой Блог</h1>

    <div class="row g-4 mb-5">
      <div 
        v-for="post in posts" 
        :key="post.id"
        class="col-12 col-md-6 col-lg-4"
      >
        <div class="card h-100 shadow-sm">
          <div class="card-body d-flex flex-column">
            <RouterLink 
              :to="`/posts/${post.slug}`" 
              class="text-decoration-none"
            >
              <h2 class="h5 card-title">{{ post.title }}</h2>
            </RouterLink>

            <p class="card-text text-muted mt-2">
              {{ post.preview }}
            </p>
          </div>
        </div>
      </div>
    </div>

    <!-- Пагинация -->
    <div 
      v-if="pagination.last_page > 1"
      class="d-flex justify-content-center align-items-center gap-3"
    >
      <button 
        class="btn btn-outline-secondary"
        @click="fetchPosts(pagination.prev_page_url)"
        :disabled="pagination.prev_page_url == null"
      >
        ← Назад
      </button>

      <span class="text-muted">
        Страница {{ pagination.current_page }} из {{ pagination.last_page }}
      </span>

      <button 
        class="btn btn-outline-secondary"
        @click="fetchPosts(pagination.next_page_url)"
        :disabled="pagination.next_page_url == null"
      >
        Вперед →
      </button>
    </div>
  </div>
</template>