<template>
  <div class="container column">
    <form class="card card-w30">
      <div class="form-control">
        <label for="type">Тип блока</label>
        <select id="type" v-model="selected">
          <option value="title">Заголовок</option>
          <option value="subtitle">Подзаголовок</option>
          <option value="avatar">Аватар</option>
          <option value="text">Текст</option>
        </select>
      </div>

      <div class="form-control">
        <label for="value">Значение</label>
        <textarea id="value" rows="3" v-model="inputText"></textarea>
      </div>

      <button class="btn primary" @click.prevent="addBlock" :disabled="inputText.length < 4">Добавить</button>
    </form>
    <resume :complist="compList"></resume>
  </div>
  <div class="container">
    <p>
      <button class="btn primary" @click="loadComments">Загрузить комментарии</button>
    </p>
    <div class="card">
      <h2>Комментарии</h2>
      <div class="loader" v-if="loading"></div>
      <ul class="list">
        <app-comment v-for="{email, body, id} in response"
                     :body="body"
                     :email="email"
                     :key="id"></app-comment>
      </ul>
    </div>
  </div>
</template>

<script>
import AppComment from '@/components/AppComment'
import Resume from '@/components/Resume'

export default {
  data() {
    return {
      selected: 'title',
      inputText: '',
      compList: [],
      response: [],
      loading: false
    }
  },
  methods: {
    addBlock () {
      this.compList.push({
        name: 'resume-' + this.selected,
        text: this.inputText
      })
      this.inputText = ''
      this.selected = 'title'
    },
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
  },
  components: {
    AppComment,
    Resume
  }
}
</script>
