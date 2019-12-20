<template>
  <div class>
    <el-button type="info" @click="logout">退出</el-button>
  </div>
</template>

<script>
export default {
  name: '',
  data () {
    return {}
  },
  components: {},
  created () {},
  mounted () {},
  methods: {
    logout () {
      window.sessionStorage.clear()
      this.$router.push('/')
    }
  }
}
</script>
<style scoped>
</style>
