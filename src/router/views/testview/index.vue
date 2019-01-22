<script>
import appConfig from '@src/app.config'
import Layout from '@layouts/main'
import PostList from '@components/post-list'
import { GetRecentPosts, GetPostSolo } from '@gql/user'

export default {
  page: {
    title: 'Home',
    meta: [{ name: 'description', content: appConfig.description }],
  },
  components: { Layout, PostList },
  props: {
    id: {
      type: String,
      required: true,
    },
  },
  data() {
    return {
      testPosts: [],
    }
  },


  apollo: {
    testPosts: {
      query: GetPostSolo,
      variables() {
        return { id: this.id }
      },
      update: function(data) {
        return data.testPosts;
      }
    },
  },
}




</script>

<template>
  <div >
      Test Page
  </div>
</template>

<style lang="scss" scoped>
@import '@design';

.logo {
  max-width: 100%;
  height: auto;
}
</style>
