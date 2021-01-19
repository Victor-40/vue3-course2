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

    <div class="card card-w70">
      <h3 v-if="compList.length === 0">Добавьте первый блок, чтобы увидеть результат</h3>
      <template v-else v-for="(item, idx) in compList" :key="idx">
        <component :is="item.name" :text="item.text"></component>
      </template>
    </div>
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
import AppTitle from '@/components/AppTitle'
import AppAvatar from '@/components/AppAvatar'
import AppSubtitle from '@/components/AppSubtitle'
import AppText from '@/components/AppText'
import AppComment from '@/components/AppComment'

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
        name: 'app-' + this.selected,
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
    AppTitle,
    AppAvatar,
    AppSubtitle,
    AppText,
    AppComment
  }
}
</script>
