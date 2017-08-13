<template>
  <div id="app">
    <da-data
      :token="token"
      :input-name="'city'"
    />
  </div>
</template>

<script>
import DaData from './DaData.vue'

export default {
  name: 'app',

  components: { DaData },

  data: () => ({ token: '' }),
}
</script>

<style lang="stylus">
#app
  font-family 'Avenir', Helvetica, Arial, sans-serif
  text-align center
  color #2c3e50
  margin-top 60px
  font-size 1.65em

h1, h2
  font-weight normal

a
  color #42b983
</style>
