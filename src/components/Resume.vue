<template>
  <div class="card card-w70">
    <h3 v-if="complist.length === 0">Добавьте первый блок, чтобы увидеть результат</h3>
    <template v-else v-for="(item, idx) in complist" :key="idx">
      <component :is="item.name" :text="item.text"></component>
    </template>
  </div>
</template>

<script>
import ResumeTitle from '@/components/ResumeTitle'
import ResumeAvatar from '@/components/ResumeAvatar'
import ResumeSubtitle from '@/components/ResumeSubtitle'
import ResumeText from '@/components/ResumeText'

export default {
  name: 'Resume',
  props: {
    complist: Array
  },
  components: {
    ResumeTitle,
    ResumeAvatar,
    ResumeSubtitle,
    ResumeText
  }
}
</script>

<style scoped>

</style>
