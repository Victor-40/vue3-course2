<template>
  <div class="container column">
    <my-control @add="addBlock"></my-control>
    <resume :complist="compList"></resume>
  </div>
  <comments></comments>
</template>

<script>
import Comments from '@/components/Comments'
import Resume from '@/components/Resume'
import MyControl from '@/components/MyControl'

export default {
  data() {
    return {
      compList: []
    }
  },
  methods: {
    addBlock (block) {
      this.compList.push(block)
    }
  },
  components: {
    Comments,
    Resume,
    MyControl
  }
}
</script>
