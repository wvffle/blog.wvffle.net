<template>
  <Layout>
    <div class="post-item rounded-lg overflow-hidden relative">
      <g-image :src="posts[0].image" class="w-full object-bottom"></g-image>
      <g-link :to="posts[0].path">
        <div class="title">
          {{ posts[0].title }}
          <div class="text-gray-300 text-xs">{{ posts[0].created_at }}</div>
        </div>
      </g-link>
    </div>
    <div class="grid grid-cols-2 gap-10">
      <div v-for="post in posts.slice(1)" :key="post.id" class="post-item rounded-lg overflow-hidden relative">
        <g-image :src="post.image"></g-image>
        <g-link :to="post.path">
          <div class="title">
            {{ post.title }}
            <div class="text-gray-300 text-xs">{{ post.created_at }}</div>
          </div>
        </g-link>
      </div>
    </div>
  </Layout>
</template>

<page-query>
  query Post {
    posts: allPost {
      edges {
        node {
          title
          path
          created_at
          image (width: 690, height: 400, quality: 100)
        }
      }
    }
  }
</page-query>

<script>
  import moment from 'moment'
  export default {
    name: 'Index',
    computed: {
      posts () {
        return this.$page.posts.edges.map(({ node }) => {
          return {
            ...node,
            created_at: moment(node.created_at)
          }
        }).sort((left, right) => {
          return left.created_at.diff(right.created_at) * -1
        }).map(post => {
          post.created_at = post.created_at.format('DD MMM YYYY')
          return post
        })
      }
    }
  }
</script>

<style scoped lang="stylus">
  .post-item
    width 100%
    max-height 400px

    a
      position absolute
      top 0
      left 0
      width 100%
      height 100%
      color #fff
      background linear-gradient(to bottom, transparent 70%, rgba(#000, .7))

      .title
        font-size 1.875rem
        font-weight bold
        position absolute
        bottom .5rem
        left .5rem
</style>
