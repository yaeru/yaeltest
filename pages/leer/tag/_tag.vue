<template>
  <main>
    <Header id="Hero">
      <template v-slot:title>
        {{ tag.name }}
      </template>
      <template v-slot:lead>
        {{ tag.description }}
      </template>
    </Header>

    <Section>
      <img :src="tag.img" :alt="tag.name" width="200" />
      
      <nuxt-content :document="tag" />

      <NuxtLink to="/listado" class="uk-button uk-button-primary">
        Back to All series
      </NuxtLink>

    </Section>

    <Section id="series">
      <template v-slot:title>
        Series in {{ tag.name }}
      </template>
      <SerieList :series="series"></SerieList>
    </Section>
  </main>
</template>

<script>
  export default {
    async asyncData({ $content, params }) {
      const tags = await $content('tags')
      .where({ slug: { $contains: params.tag } })
      .limit(1)
      .fetch()
      const tag = tags.length > 0 ? tags[0] : {}
      const series = await $content('series')
      .where({ tags: { $contains: tag.slug } })
      .sortBy('createdAt', 'asc')
      .fetch()
      return {
        series,
        tag
      }
    },
    methods: {
      formatDate(date) {
        const options = { year: 'numeric', month: 'long', day: 'numeric' }
        return new Date(date).toLocaleDateString('en', options)
      }
    }
  }
</script>