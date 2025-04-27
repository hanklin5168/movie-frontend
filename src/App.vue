<template>
  <div id="app">
    <h1>🎬 現正上映電影 test</h1>

    <!-- 搜尋框 -->
    <input type="text" v-model="keyword" placeholder="輸入關鍵字查詢電影" />
    <button @click="fetchMovies">查詢</button>

    <!-- 排序方式選擇 -->
    <select v-model="sortType">
      <option value="release_date">依上映日（新到舊）</option>
      <option value="title">依片名（A-Z）</option>
    </select>

    <div v-if="movies.length">
      <ul>
        <li v-for="movie in movies" :key="movie.title">
          <h2>{{ movie.title }}</h2>
          <!-- 只有原文片名不同時才顯示 -->
          <p v-if="movie.original_title && movie.original_title !== movie.title">
            🎯 原文片名：{{ movie.original_title }}
          </p>
          <p>🗓️ 上映日期：{{ movie.release_date }}</p>
          <p>⭐️ 評分：{{ movie.vote_average }}</p>
          <!-- 顯示類型（轉成文字） -->
          <p>
            🎬 類型：
            <span v-for="id in movie.genre_ids" :key="id">
              {{ genreMapping[id] || '未知' }}
            </span>
          </p>
          <p>{{ movie.info }}</p>
          <!-- 顯示海報 -->
          <img :src="getPosterUrl(movie.poster_path)" alt="海報" width="200" v-if="movie.poster_path" />

        </li>
      </ul>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import axios from 'axios'

const genreMapping = {
  28: '動作',
  12: '冒險',
  16: '動畫',
  35: '喜劇',
  80: '犯罪',
  99: '紀錄片',
  18: '劇情',
  10751: '家庭',
  14: '奇幻',
  36: '歷史',
  27: '恐怖',
  10402: '音樂',
  9648: '懸疑',
  10749: '愛情',
  878: '科幻',
  10770: '電視電影',
  53: '驚悚',
  10752: '戰爭',
  37: '西部'
}

const movies = ref([])
const keyword = ref('')
const sortType = ref('release_date')  // ⭐️ 預設是依上映日排序

const fetchMovies = async () => {
  const res = await axios.get('https://movie-backend-wlvm.onrender.com/movies')

  console.log(res.data)

  let results = res.data

  // 關鍵字搜尋
  if (keyword.value.trim() !== '') {
    results = results.filter(movie => movie.title.includes(keyword.value.trim()))
  }

  // 依照選擇的方式排序
  if (sortType.value === 'release_date') {
    results.sort((a, b) => new Date(b.release_date) - new Date(a.release_date))
  } else if (sortType.value === 'title') {
  results.sort((a, b) => a.original_title.localeCompare(b.original_title))
  }

  movies.value = results
}

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
input, select {
  width: 40%;
  padding: 8px;
  margin-right: 10px;
  margin-bottom: 10px;
}
button {
  padding: 8px 20px;
}
img {
  margin-top: 10px;
  border-radius: 8px;
}
</style>
