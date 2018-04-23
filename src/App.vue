<template lang="pug">
  div#app
    router-view(:htmlForm="htmlCont")
</template>

<script>
export default {
  name: 'App',
  data () {
    return {
      headerRight: 'Your Form',
      htmlCont: ''
    }
  },
  created: function () {
  },
  methods: {
  }
}
</script>

<style>
#app {
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  margin-top: 60px;
  display: flex;
  display: -webkit-flex;
  font-family: "Helvetica Neue",Helvetica,Arial,sans-serif;
  font-size: 14px;
  line-height: 1.428571429;
  color: #333;
}
</style>
