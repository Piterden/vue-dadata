<template>
  <div class="dadata-wrapper">
    <div class="inner">
      <div class="form-group">
        <input type="text"
          :class="['form-control', ...inputClass]"
          :name="inputName"
          v-model="inputValue"
          @input="onInput"
        />
      </div>
      <div class="suggestions-wrapper">
        <ul v-if="isListShown">
          <li
            v-for="name, idx in dadata.suggestions"
            :key="idx"
            @click="onSelect"
          >Suggestion</li>
        </ul>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'DaData',

  data: () => ({
    serviceUrl: 'https://dadata.ru/api/v2',
    dadata: { suggestions: [] },
    hint: false,
    inputValue: null,
  }),

  props: {
    token: { type: String, required: true },
    inputName: { type: String, required: true },
    type: { type: String, default: () => 'city' },
    addon: { type: String, default: () => 'none' },
    minChars: { type: Number, default: () => 2 },
    inputClass: { type: Array, default: () => [] },
    deferRequestBy: { type: Number, default: () => 100 },
    count: { type: Number, default: () => 5 },
    inputId: { type: String },
  },

  computed: {
    isListShown () {
      return this.dadata &&
        this.dadata.suggestions &&
        this.dadata.suggestions.length
    }
  },

  methods: {
    onSelect (e) {
      if (!e.target) {
        return
      }
      this.inputValue = e.target.innerHTML.trim()
    },

    onInput (e) {
      let value = e.target.value.trim()

      if (value.length < this.minChars) {
        return
      }

      this.sendRequest(value)
    },

    sendRequest (value) {
      console.log('Request')
      this.$http.post(url, data)
        .then(this.onSuccess)
        .catch(this.onError)
    },

    onSuccess (res) {
      if (!(res || res.suggestions || res.suggestions.length)) {
        return
      }
      this.dadata = res.data
    },

    onError (err) {

    },
  },
}
</script>

<style lang="stylus" scoped>
input
  width 200px
  padding 0
  border none
  box-shadow 0 0 1px 1px #000
  font-size 1em

ul
  list-style-type none
  padding 0
  width 200px
  margin 0 auto

  li
    display block
    margin 0
    padding 0
    text-align left
    cursor pointer
    transition color .4s ease-out
    &:hover
      color red
</style>
