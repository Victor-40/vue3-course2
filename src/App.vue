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
  <comments></comments>
</template>

<script>
import Comments from '@/components/Comments'
import Resume from '@/components/Resume'

export default {
  data() {
    return {
      selected: 'title',
      inputText: '',
      compList: []
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
    }
  },
  components: {
    Comments,
    Resume
  }
}
</script>
