<template>
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

    <button class="btn primary" @click.prevent="sendBlock" :disabled="inputText.length < 4">
      Добавить
    </button>
  </form>
</template>

<script>
export default {
  name: 'MyControl',
  emits: ['add'],
  data () {
    return {
      selected: 'title',
      inputText: ''
    }
  },
  methods: {
    sendBlock() {
      const block = {
        name: 'resume-' + this.selected,
        text: this.inputText
      }
      this.$emit('add', block)
      this.selected = 'title'
      this.inputText = ''
    }
  }
}
</script>
