<script>
import appConfig from '@src/app.config'
import Layout from '@layouts/main'
import PostList from '@components/post-list-solo'
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
      recentPosts: [],
    }
  },
  computed: {
    isLoadingRecentPosts() {
      return this.$apollo && this.$apollo.queries
        ? this.$apollo.queries.recentPosts.loading
        : false
    },
  },
  apollo: {
    recentPosts: {
      query: GetPostSolo,
      variables() {
        return { id: this.id }
      },
      update (data){
        return data
      }
    }
  },
}




</script>

<template>
  <Layout>
    <h1>Individual Post</h1>
    <img class="logo" src="@assets/images/logo.png" alt="Logo" />
    <h2>A more detailed page for individual posting</h2>
    <PostList
      v-if="!isLoadingRecentPosts && recentPosts"
      :posts="recentPosts"

    />
    <BaseSpinner v-else />
  </Layout>
</template>

<style lang="scss" scoped>
@import '@design';

.logo {
  max-width: 100%;
  height: auto;
}
</style>
