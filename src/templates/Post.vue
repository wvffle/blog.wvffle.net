<template>
  <Layout>
    <div class="post mx-auto text-xl">
      <div class="text-4xl font-bold">{{ $page.post.title }}</div>
      <div class="text-sm text-gray-700 mb-8">{{ date($page.post.created_at) }}</div>
      <g-image :src="$page.post.image"></g-image>
      <vue-remark-content>
        <template v-slot:donate>
          <donate-button></donate-button>
          <p></p>
        </template>
      </vue-remark-content>
    </div>
  </Layout>
</template>

<page-query>
  query Post($id: ID!) {
    post(id: $id) {
      title
      created_at
      image (width: 690, height: 400, quality: 100)
    }
  }
</page-query>

<script>
  // TODO: Switch to transormer-remark
  import DonateButton from '~/components/DonateButton'
  import moment from 'moment'

  export default {
    name: 'Post',
    components: {
      DonateButton
    },
    methods: {
      date (date) {
        return moment(date).format('DD MMM YYYY')
      }
    }
  }
</script>

<style lang="stylus">
  .post
    width 690px

    img
      max-height 400px
      width 100%
      object-fit cover
</style>

