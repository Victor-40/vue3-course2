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

    <div class="card card-w70" >
      <h3 v-if="compList.length === 0">Добавьте первый блок, чтобы увидеть результат</h3>
      <template v-else v-for="item in compList" :key="item">
       <component :is="item"></component>
     </template>
    </div>
  </div>
  <div class="container">
    <p>
      <button class="btn primary" >Загрузить комментарии</button>
    </p>
    <div class="card">
      <h2>Комментарии</h2>
      <ul class="list">
        <li class="list-item">
          <div>
            <p><strong>test@microsoft.com</strong></p>
            <small>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Eligendi, reiciendis.</small>
          </div>
        </li>
      </ul>
    </div>
<!--    <div class="loader"></div>-->
  </div>
</template>

<script>
import AppTitle from '@/AppTitle'
import AppAvatar from '@/AppAvatar'
import AppSubtitle from '@/AppSubtitle'
import AppText from '@/AppText'

export default {
  data() {
    return {
      selected: 'title',
      inputText: '',
      // compList: [
      //   'app-header',
      //   'app-avatar',
      //   'app-subtitle',
      //   'app-text'
      // ],
      compList: []
    }
  },
  methods: {
    addBlock() {
      this.compList.push('app-' + this.selected)
      this.inputText = ''
      this.selected = 'title'
    }
  },
  components: { AppTitle, AppAvatar, AppSubtitle, AppText }

}
</script>

<style>
  .avatar {
    display: flex;
    justify-content: center;
  }

  .avatar img {
    width: 150px;
    height: auto;
    border-radius: 50%;
  }
</style>
