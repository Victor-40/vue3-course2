<template>
  <div class="container">
    <p>
      <button class="btn primary" @click="loadComments">Загрузить комментарии</button>
    </p>
    <div class="card">
      <h2>Комментарии</h2>
      <div class="loader" v-if="loading"></div>
      <ul class="list">
        <comment-list v-for="{email, body, id} in response"
                     :body="body"
                     :email="email"
                     :key="id"></comment-list>
      </ul>
    </div>
  </div>
</template>

<script>
import CommentList from '@/components/CommentList'
export default {
  name: 'Comments',
  data() {
    return {
      response: [],
      loading: false
    }
  },
  components: {
    CommentList
  },
  methods: {
    async loadComments () {
      this.loading = true
      const res = await fetch('https://jsonplaceholder.typicode.com/comments?_limit=42', {
        method: 'GET',
        headers: {
          'Content-Type': 'application/json'
        }
      })
      this.response = await res.json()
      this.loading = false
    }
  }
}
</script>

<style scoped>

</style>
