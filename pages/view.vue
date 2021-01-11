<template>
  <div></div>
</template>
<script>
export default {
  layout: 'default',
  methods: {
    async handleQueryVideo() {
      try {
        const result = await this.$axios.get(`/porn?porn=${this.$route.params.id}`)
        console.log(result)
        if (result.data.content && result.data.content.length > 0) {
          this.result = result.data.content.filter(item => item.key.kind === 'PornEntry').map((item) => {
            item.rating = Math.round(Math.random(90, 100) * 100)
            return item
          })
        }
      } catch (e) {

      }
    }
  },
  async created() {
    if (!this.$route.params.id) {
      this.$router.push('/')
    } else {
      await this.handleQueryVideo()
    }
  }
}
</script>

<style lang="scss" scoped>
</style>
