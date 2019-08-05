<template>
  <div class="accept-container">
    <div class="go-back" v-show="goBackState" @click="goBack">GoBack</div>
    <ul>
      <li v-for="(item, key) in webAddress" :key="key">
        <a :href="item.link" target="showHere" @click="showIframe">{{
          item.name
        }}</a>
      </li>
    </ul>
    <iframe
      v-show="iframeState"
      id="show-iframe"
      frameborder="0"
      name="showHere"
      scrolling="auto"
      src=""
    ></iframe>
    <iframe
      id="dialogFrame"
      frameborder="0"
      scrolling="no"
      style="background-color:transparent; position: absolute; z-index: -1; width: 100%; height: 100%; top: 0;left:0;"
    ></iframe>
  </div>
</template>

<script>
export default {
  name: 'hello',
  data() {
    return {
      iframeState: false,
      goBackState: false,
      webAddress: [
        {
          name: 'segmentFault',
          link: 'https://segmentfault.com/a/1190000004502619'
        },
        {
          name: '博客',
          link: 'http://vuex.vuejs.org/'
        },
        {
          name: '特效',
          link: 'http://www.yyyweb.com/377.html'
        }
      ]
    }
  },
  mounted() {
    const oIframe = document.getElementById('show-iframe')
    const deviceWidth = document.documentElement.clientWidth
    const deviceHeight = document.documentElement.clientHeight
    oIframe.style.width = deviceWidth + 'px'
    oIframe.style.height = deviceHeight + 'px'
  },
  methods: {
    goBack() {
      this.goBackState = false
      this.iframeState = false
    },
    showIframe() {
      this.goBackState = true
      this.iframeState = true
    }
  }
}
</script>
<style scoped>
</style>
