<template>
  <div class="pt-56 h-screen">
    <div class="header-container fixed left-0 top-0 w-full z-10">
      <g-link to="/" class="flex items-center justify-center pt-6 pb-10 header bg-white">
        <g-image src="~/avatar.jpg" alt="" class="w-20 rounded-full mr-4 avatar"></g-image>
        <div class="float-left">
          <div class="text-2xl text-gray-800">Kasper Seweryn</div>
          <div class="text-sm">Javascript/Frontend developer blog</div>
        </div>
      </g-link>
    </div>
    <div class="container mx-auto text-gray-900">
      <slot/>
    </div>
    <div class="text-center text-gray-500 py-10 text-xs">:wq</div>
  </div>
</template>

<static-query>
query {
  metadata {
    siteName
  }
}
</static-query>

<style lang="stylus">
  html, body, #app
    height 100%

  h1, h2, h3, h4
    font-weight bold

  h1
    font-size 2.25rem
    margin-bottom 2rem

  h2
    font-size 1.875rem
    margin-bottom 1.5rem

  h3
    font-size 1.5rem
    margin-bottom 1rem

  h4
    margin-bottom .75rem

  ul
    list-style disc
    padding-left 1rem
    padding-bottom 2rem

  p
    margin-bottom 2rem

  a
    color #f6ad55
    padding 0 .5rem

    &:hover
      text-decoration underline

    &[aria-hidden=true]
      width 0
      height 0
      display block
      visibility hidden

  code
    vertical-align middle
    font-size .875rem
    border-radius 0.5rem
    background #1a202c
    color #fff
    padding .25rem .5rem

  pre[class*=language-]
    padding 0
    margin 0
    background transparent !important
    overflow initial

    code[class*=language-]
      @extend code
      text-shadow none
      display block
      margin-bottom 2rem
      padding 1rem
      box-shadow 0 20px 25px -5px rgba(0, 0, 0, 0.1), 0 10px 10px -5px rgba(0, 0, 0, 0.04)

  blockquote
    border-left .5rem solid #f6ad55
    padding .5rem 1rem .5rem 1rem
    color #4a5568
    margin-bottom 2rem

    > p
      margin-bottom 0

  .token.operator, .token.entity, .token.url, .language-css .token.string, .style .token.string
    background transparent
</style>

<style scoped lang="stylus">
  .header
    clip-path polygon(0 0, 100% 0, 100% calc(100% - 3rem), 50% 100%, 0 calc(100% - 3rem))

    &-container
      filter drop-shadow(0 .25rem 0 #f6ad55)

  .avatar
    transition max-width 1s ease-out
    &.small
      max-width 5rem
</style>
