<template>
  <article class="container">
    <h1>Title: {{ article.title }}</h1>
    <hr />
    <br />
    <br />
    <nuxt-content :document="article" />
  </article>
</template>

<script>
export default {
  async asyncData({ $content, params, error }) {
    const { path } = params
    const article = await $content(path)
      .fetch()
      // eslint-disable-next-line node/handle-callback-err
      .catch((err) => {
        error({ statusCode: 404, message: 'Page not found' })
      })

    return {
      article,
    }
  },
}
</script>
