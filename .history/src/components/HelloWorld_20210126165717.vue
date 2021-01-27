<template>
  <div class="container">
    <!-- <div v-for="(item, index) in apiData.data" :key="index">
      {{item}}
    </div> -->
    <div v-for="(item, index) in apiData.data" :key="index">
      {{item}}
    </div>
  </div>
</template>

<script lang="ts">
import { computed, onMounted, reactive } from 'vue'
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
          apiData.data = res.data.result.records
        })
        .catch((err) => {
          console.log('err', err)
        })
    }
    // computed
    const newAdd = computed(() => {
      return apiData.data.forEach((item: any) => {
        item.Add = item.Add.substring(6)
        console.log('item.Add', item.Add)
      })
    })

    // lifecycle
    onMounted(() => {
      getData()
    })

    return {
      apiData,
      newAdd
    }
  }
})

</script>

<style scoped lang="scss">

</style>
