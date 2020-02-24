<template>
  <Layout>
    <div class="post mx-auto text-xl">
      <div class="text-4xl font-bold">{{ $page.post.title }}</div>
      <p class="text-sm text-gray-700 mb-8">{{ date($page.post.created_at) }}</p>
      <g-image :src="$page.post.image"></g-image>
      <p class="text-xs text-gray-400 italic" v-html="getSource($page.post.image.src)"></p>
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
      },
      getSource (image) {

        return image.replace(/.+images\/([^.]+)\..+/, (_, match) => {
          const tokens = match.split('-')
          const service = tokens.shift()


          if (service  === 'unsplash') {
            return `Unsplash: <a href="https://unsplash.com/photos/${tokens.shift()}" target="_blank">${tokens.join(' ')}</a>`
          }

          return ''
        })
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

