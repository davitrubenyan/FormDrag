<template lang="pug">
  div#app
    router-view
    div.right-form
      h1 {{headerRight}}
      hr
      div
        form
          fieldset.field-right
</template>

<script>
export default {
  name: 'App',
  data () {
    return {
      headerRight: 'Your Form'
    }
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
.right-form{
  flex: 2;
  margin: 0px 40px;
}
.field-right{
  border: 1px solid #ccc;
  min-height: 220px;
  padding: 5px;
  padding-bottom: 50px;
}
</style>
