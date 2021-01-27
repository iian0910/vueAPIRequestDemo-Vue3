<template>
  <div>HI</div>
</template>

<script lang="ts">
import { onMounted, reactive } from 'vue'
import { createApi } from 'unsplash-js'

export default ({

  setup () {
    const unsplash = createApi({ accessKey: 'sU4F5XT8pIWQGCxk1_89YnimkFDN652NLmhn-6tpJDE' })

    // data
    const data = reactive({
      userInfo: []
    })

    // methods
    function getData () {
      unsplash.collections.list({ page: 1, perPage: 10 })
        .then(result => {
          console.log('result', result)
        })
    }
    // computed
    // lifecycle
    onMounted(() => {
      getData()
    })

    return {
      data
    }
  }
})

</script>

<style scoped lang="scss">

</style>
