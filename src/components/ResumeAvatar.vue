<template>
  <div class="avatar">
    <img :src="text" alt="img">
  </div>
</template>

<script>
export default {
  name: 'ResumeAvatar',
  props: {
    text: String
  }
}
</script>

<style scoped>
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
