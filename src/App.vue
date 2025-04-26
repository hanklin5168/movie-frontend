<template>
  <div id="app">
    <h1>🎬 現正上映的電影</h1>

    <!-- 新增：搜尋框 -->
    <input type="text" v-model="keyword" placeholder="輸入關鍵字查詢電影" />
    <button @click="fetchMovies">查詢</button>

    <div v-if="movies.length">
      <ul>
        <li v-for="movie in movies" :key="movie.title">
          <h2>{{ movie.title }}</h2>
          <p>上映日期：{{ movie.release_date }}</p>
          <p>{{ movie.info }}</p>
          <!-- 顯示海報圖片 -->
          <img :src="getPosterUrl(movie.poster_path)" alt="海報" width="200" v-if="movie.poster_path" />
        </li>
      </ul>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import axios from 'axios'

const movies = ref([])
const keyword = ref('')

const fetchMovies = async () => {
  const res = await axios.get('https://movie-backend-wlvm.onrender.com/movies')
  let results = res.data

  // 如果有輸入關鍵字，過濾出包含關鍵字的電影
  if (keyword.value.trim() !== '') {
    results = results.filter(movie => movie.title.includes(keyword.value.trim()))
  }

  movies.value = results
}


// 處理海報圖片網址
const getPosterUrl = (path) => {
  if (!path) return ''
  return `https://image.tmdb.org/t/p/w500${path}`
}
</script>

<style scoped>
#app {
  max-width: 600px;
  margin: auto;
  padding: 20px;
}
h1 {
  text-align: center;
}
input {
  width: 70%;
  padding: 8px;
  margin-right: 10px;
}
button {
  padding: 8px 20px;
}
img {
  margin-top: 10px;
  border-radius: 8px;
}
</style>
