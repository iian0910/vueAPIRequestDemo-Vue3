<template>
  <div class="container">
    HI
  </div>
</template>

<script lang="ts">
import { onMounted, reactive } from 'vue'
import axios from 'axios'

export default ({

  setup () {
    // data
    const apiData = reactive({
      data: []
    })
    // methods
    function getData () {
      const api = 'https://raw.githubusercontent.com/hexschool/KCGTravel/master/datastore_search.json'
      axios.get(api)
        .then((res) => {
          console.log('res', res)
        })
        .catch((err) => {
          console.log('err', err)
        })
    }
    // computed
    // lifecycle
    onMounted(() => {
      getData()
    })
  }
})

</script>

<style scoped lang="scss">

</style>
