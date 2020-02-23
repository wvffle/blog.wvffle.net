<template>
  <Layout>
    <div v-for="post in posts" :key="post.id">
      <g-link :to="post.path">{{ post.title }}</g-link>
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

<style>
</style>
