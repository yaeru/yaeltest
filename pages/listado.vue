<template>
	<Section id="series">
		<template v-slot:title>
			Series
		</template>
		<template v-slot:lead>
			Los mejores productos
		</template>

		<div class="uk-grid uk-child-width-1-2@s uk-child-width-1-4@m" uk-grid>
			<article v-for="serie in series" :key="serie.slug">
				<div class="uk-card uk-card-small uk-card-default uk-card-hover">
					<div class="ukcard-media-top">
						<img :src="require(`~/assets/img/${serie.img}`)" v-if="serie.img" />
					</div>
					<div class="uk-card-body">
						<h2 class="uk-card-title uk-margin-remove">
							{{ serie.title }}
						</h2>
						<p class="uk-margin-remove">
							{{ serie.description }}
						</p>
						<!-- <p>by {{ serie.author.name }}</p> -->
					</div>
					<div class="uk-card-footer">
						<NuxtLink :to="{ name: 'leer-slug', params: { slug: serie.slug } }" class="uk-button uk-button-primary uk-button-small">
							Leer
						</NuxtLink>
					</div>
				</div>
			</article>
		</div>
	</Section>
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

  /*export default {
		data() {
			return {
				series: [
				{
					id: 0,
					title: 'Dinosaurio',
					description: 'This is the Description',
				},
				{
					id: 1,
					title: 'Perro',
					description: 'This is the Description',
				},
				{
					id: 2,
					title: 'Gallina',
					description: 'This is the Description',
				},
				{
					id: 3,
					title: 'Gato',
					description: 'This is the Description',
				},
				]
			}
		},
	}*/
</script>