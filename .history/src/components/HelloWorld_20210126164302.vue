<template>
  <div class="container">
    <div v-for="(item, index) in data" :key="index">
      {{item}}
    </div>
  </div>
</template>

<script lang="ts">
import { computed, onMounted, reactive, toRef } from 'vue'
import axios from 'axios'

export default ({

  setup () {
    // data
    const apiData = reactive({
      data: [],
      newAdd: computed(() => {
        return 'a'
      })
    })
    // methods
    function getData () {
      const api = 'https://raw.githubusercontent.com/hexschool/KCGTravel/master/datastore_search.json'
      axios.get(api)
        .then((res) => {
          apiData.data = res.data.result.records
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

    return {
      data: toRef(apiData, 'data')
    }
  }
})

</script>

<style scoped lang="scss">

</style>
