<template>
  <div class="container">
    <h1 class="blog-title">Welcome my awesome blog</h1>
    <p>I love Vue.js so I write about it.</p>

    <div class="articles-list">
      <h2 class="article-list__section-heading">New Articles</h2>
      <!-- articles will be listed here -->
      <div
        v-for="(article, index) in articles"
        :key="index"
        class="article-list__item"
      >
        <h3>
          <nuxt-link :to="`/article${article.path}`">{{
            article.title
          }}</nuxt-link>
          <!-- nuxt-link is the Nuxt equivalent of router-link for Vue -->
        </h3>
        <p>
          Published on
          <strong>{{
            new Date(article.createdAt).toLocaleDateString()
          }}</strong>
        </p>
        <p>{{ article.description }}</p>
        <hr />
      </div>
    </div>
  </div>
</template>

<script>
export default {
  async asyncData({ $content, params, error }) {
    const path = '/' // to fetch all the content
    const articles = await $content(path)
      .where({ published: { $eq: true } })
      .fetch()
      // eslint-disable-next-line node/handle-callback-err
      .catch((err) => {
        error({ statusCode: 404, message: 'Page not found' })
      })

    return {
      articles,
    }
  },
}
</script>
