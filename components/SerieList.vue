<template>
	<div class="uk-grid uk-child-width-1-2@s uk-child-width-1-4@m" uk-grid>
		<article v-for="serie in series" :key="serie.slug">
			<NuxtLink :to="{ name: 'leer-slug', params: { slug: serie.slug } }" class="uk-button-link">
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
			</NuxtLink>
		</article>
	</div>
</template>

<script>
	export default {
		props: {
			series: []
		}
	}
</script>