<template>
  <div class="page">
    <div class="page-infinite-wrapper" ref="wrapper" :style="{ height: wrapperHeight + 'px' }">
      <wv-group
        title="无限滚动加载"
        v-infinite-scroll="loadMore"
        infinite-scroll-disabled="loading"
        infinite-scroll-distance="50"
      >
        <wv-cell title="条目" v-for="item in list" :key="item" :value="item"/>
      </wv-group>
      <p v-show="loading" class="loading-tips">
        <wv-spinner type="snake" color="#444" :size="24"/>
      </p>
    </div>
  </div>
</template>

<script>
export default {
  data () {
    return {
      list: [],
      loading: false,
      allLoaded: false,
      wrapperHeight: 0
    }
  },

  methods: {
    loadMore () {
      console.log('loading more')
      this.loading = true
      setTimeout(() => {
        let last = this.list[this.list.length - 1]
        for (let i = 1; i <= 5; i++) {
          this.list.push(last + i)
        }
        this.$nextTick(() => {
          this.loading = false
        })
      }, 2000)
    }
  },

  mounted () {
    this.wrapperHeight = document.documentElement.clientHeight - this.$refs.wrapper.getBoundingClientRect().top
    for (let i = 1; i <= 15; i++) {
      this.list.push(i)
    }
  }
}
</script>

<style scoped lang="scss">
  .loading-tips {
    color: #222;
    text-align: center;
  }
</style>
