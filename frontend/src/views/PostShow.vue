<script setup>
import { onMounted, ref } from 'vue'
import { useRoute } from 'vue-router'
import axios from 'axios'

const post = ref(null)
const route = useRoute()

const fetchPost = async () => {
  try {
    const response = await axios.get(`/api/posts/${route.params.slug}`)
    post.value = response.data.post
  } catch (error) {
    console.error('Ошибка при загрузке поста:', error)
  }
}

onMounted(() => {
  fetchPost()
})
</script>

<template>
  <div class="container py-5">

    <!-- Лоадер -->
    <div v-if="!post" class="d-flex justify-content-center py-5">
      <div class="spinner-border" role="status">
        <span class="visually-hidden">Загрузка...</span>
      </div>
    </div>

    <!-- Пост -->
    <div v-if="post" class="row justify-content-center">
      <div class="col-lg-8">
        <div class="card shadow-sm">
          <div class="card-body">
            <h1 class="card-title mb-3">{{ post.title }}</h1>

            <div class="text-muted mb-4">
              Опубликовано: {{ new Date(post.created_at).toLocaleDateString() }}
            </div>

            <div class="card-text fs-5" style="white-space: pre-line;">
              {{ post.body }}
            </div>
          </div>
        </div>

        <div class="mt-4">
          <router-link to="/"
            class="btn btn-outline-secondary">
            ← Назад к списку
          </router-link>
        </div>
      </div>
    </div>

  </div>
</template>
