<template>
  <div class="pt-56 h-screen">
    <div class="header-container fixed left-0 top-0 w-full">
      <g-link to="/" class="flex items-center justify-center pt-6 pb-10 header bg-white">
        <g-image src="~/avatar.jpg" alt="" class="w-20 rounded-full mr-4 avatar"></g-image>
        <div class="float-left">
          <div class="text-2xl">Kasper Seweryn</div>
          <div class="text-sm text-orange-400">Javascript/Frontend developer blog</div>
        </div>
      </g-link>
    </div>
    <div class="container mx-auto text-gray-900">
      <slot/>
    </div>
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
