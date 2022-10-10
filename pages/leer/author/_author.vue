<template>
	<div>
		<header class="uk-section uk-section-primary">
			<div class="uk-container">
				<div class="uk-grid uk-child-width-expand" uk-grid>
					<div class="uk-width-medium">
						<img :src="require(`~/assets/img/${series[0].author.image}`)" :alt="series[0].author.name" class="uk-border-rounded" v-if="series[0].author.image" />
					</div>
					<div>
						<h1 class="uk-margin-remove-bottom uk-heading-small">
							Author: {{ series[0].author.name }}
						</h1>
						<p class="uk-text-lead uk-margin-small-top">
							Bio: {{ series[0].author.bio }}
						</p>
					</div>
				</div>
			</div>
		</header>

		<Section id="series">
			<template v-slot:title>
				Here are a list of series by {{ series[0].author.name }}
			</template>
			<SerieList :series="series"></SerieList>
		</Section>

	</div>
</template>

<script>
	export default {

		async asyncData({ $content, params }) {
			const series = await $content('series', params.slug)
			.where({
				'author.name': {
					$regex: [params.author, 'i']
				}
			})
			.without('body')
			.sortBy('createdAt', 'asc')
			.fetch()

			return {
				series
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