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
      unsplash.users.getPhotos({ username: 'foo' }).then(result => {
        if (result.errors) {
          // handle error here
          console.log('error occurred: ', result.errors[0])
        } else {
          const feed = result.response

          // extract total and results array from response
          const { total, results } = feed

          // handle success here
          console.log(`received ${results.length} photos out of ${total}`)
          console.log('first photo: ', results[0])
        }
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
