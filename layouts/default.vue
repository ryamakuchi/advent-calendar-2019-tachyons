<template>
  <div>
    <nav class="db w-100 pa3 ph5-l flex justify-between items-center-ns">
      <div class="db v-mid w-auto mb2 mb0-l">
        <logo class="v-mid" />

        <a
          class="v-mid link dim tc f5 f4-ns fw6 black-70"
          href="https://qiita.com/advent-calendar/2019/nuxt-js"
          target="_blank"
          rel="noopener noreferrer"
        >
          Nuxt.js Advent Calendar 2019 for Qiita
        </a>
      </div>

      <div class="db v-mid w-auto">
        <a
          class="link f6 fw6 hover-blue black-70"
          href="https://tachyons.io/"
          target="_blank"
          rel="noopener noreferrer"
        >
          Made with Tachyons
        </a>
      </div>
    </nav>

    <nuxt />
  </div>
</template>

<script>
import Logo from '~/components/Logo.vue'

export default {
  components: {
    Logo
  }
}
</script>

<style>
html {
  font-family: 'Source Sans Pro', -apple-system, BlinkMacSystemFont, 'Segoe UI',
    Roboto, 'Helvetica Neue', Arial, sans-serif;
  font-size: 16px;
  word-spacing: 1px;
  -ms-text-size-adjust: 100%;
  -webkit-text-size-adjust: 100%;
  -moz-osx-font-smoothing: grayscale;
  -webkit-font-smoothing: antialiased;
  box-sizing: border-box;
}

*,
*:before,
*:after {
  box-sizing: border-box;
  margin: 0;
}
</style>
