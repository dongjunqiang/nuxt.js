<template>
  <div class="__nuxt-error-page">
    <div class="container">

        <div class="row">
          <div class="column">
            <h1>{{ statusCode }} </h1>
            <h4> {{ message }} </h4>
            <% if(debug) { %>
              <pre class="error-box" v-if="mounted"><code>Route: {{ $route.fullPath }}<br>Query: {{ $route.query }}<br>Params: {{$route.params}}<br>{{ error.stack }}</code></pre>
            <% } %>
            <p v-if="statusCode === 404">
              <nuxt-link class="error-link" to="/">Back to the home page</nuxt-link>
            </p>
          </div>
        </div>

        <div class="row">
          <div class="column">
            <div class="poweredby">
              <small> Powered by <a href="https://nuxtjs.org" target="_blank" rel="noopener">Nuxt.js</a> </small>
            </div>
          </div>
        </div>

    </div>
  </div>
</template>

<script>
export default {
  name: 'nuxt-error',
  props: ['error'],
  head () {
    return {
      title: this.statusCode + ' - ' + this.message,
      link: [
        { rel: 'stylesheet', href: 'https://cdnjs.cloudflare.com/ajax/libs/normalize/7.0.0/normalize.min.css', type: 'text/css', media: 'all' },
        { rel: 'stylesheet', href: 'https://cdnjs.cloudflare.com/ajax/libs/milligram/1.3.0/milligram.min.css', type: 'text/css', media: 'all' }
      ]
    }
  },
  <% if(debug) { %>
  data () {
    return {
      mounted: false
    }
  },
  mounted () {
    this.mounted = true
  },
  <% } %>
  computed: {
    statusCode () {
      return (this.error && this.error.statusCode) || 500
    },
    message () {
      return (this.error && this.error.message) || 'Nuxt Server Error'
    }
  }
}
</script>

<style>
.__nuxt-error-page {
  background: #F5F7FA;
  font-size: 14px;
  word-spacing: 1px;
  -ms-text-size-adjust: 100%;
  -webkit-text-size-adjust: 100%;
  -moz-osx-font-smoothing: grayscale;
  -webkit-font-smoothing: antialiased;
  text-align: center;
}
.__nuxt-error-page .container {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  height: 100vh;
  margin: 0 auto;
  max-width: 70%;
}
<% if(debug) { %>
.__nuxt-error-page .error-box {
  box-shadow: 0px 0px 9px #d3d3d3;
  padding: 10px;
  text-align: left;
}
<% } %>
.__nuxt-error-page .poweredby {
  text-align: center;
  margin-top: 10%;
}
.__nuxt-error-page a {
  color: #42b983 !important;
}
.__nuxt-error-page pre {
  border-color: #42b983 !important;
  background-color: white;
}
.__nuxt-error-page pre code {
  background-color: white;
}
</style>
