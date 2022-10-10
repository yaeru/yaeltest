<template>
	<main>
		<Header id="hero">
			<template v-slot:title>
				Series
			</template>
			<template v-slot:lead>
				Los mejores productos
			</template>
		</Header>

		<Section id="series">
			<SerieList :series="series"></SerieList>
		</Section>
	</main>
</template>

<script>
	export default {
		async asyncData({ $content, params }) {
			const series = await $content('series')
			.only(['title', 'description', 'img', 'slug', 'author'])
			.sortBy('createdAt', 'asc')
			.fetch()

			return {
				series
			}
		}
	}
</script>