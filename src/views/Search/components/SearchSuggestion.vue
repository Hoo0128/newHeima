<template>
  <div>
    <van-cell v-for="(item, index) in highightData" :key="index">
      <template #icon>
        <van-icon name="search" calss="search-icon" />
      </template>

      <template #title>
        <span v-html="item"></span>
      </template>
    </van-cell>
  </div>
</template>

<script>
import { gerSearchSuggestion } from '@/api'
export default {
  props: {
    keywords: {
      type: String,
      required: true
    }
  },
  data () {
    return {
      suggestions: []
    }
  },
  watch: {
    keywords: {
      immediate: true,
      handler () {
        this.gerSearchSuggestion()
      }
    }
  },
  methods: {
    async gerSearchSuggestion () {
      try {
        const res = await gerSearchSuggestion(this.keywords)

        if (res.data.data.options.length === 0) {
          this.$toast.fail('没有搜索建议')
        }
        this.suggestions = res.data.data.options.filter(Boolean)
      } catch (error) {
        console.log(error)
      }
    }
  },
  computed: {
    highightData () {
      const reg = new RegExp(this.keywords, 'ig')
      return this.suggestions.map((str) =>
        str.replace(reg, (match) => `<span style="color: red">${match}</span>`)
      )
    }
  }
}
</script>

<style scoped lang="less">
.search-icon {
  padding-top: 10px;
}
</style>
