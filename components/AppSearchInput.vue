<template>
	<div class="uk-position-relative">
		<div class="uk-search uk-search-default">
			<span uk-search-icon></span>
			<input
			v-model="searchQuery"
			type="search"
			autocomplete="off"
			placeholder="Search series"
			class="uk-search-input"
			/>
		</div>

		<div v-if="series.length" class="uk-card uk-card-body uk-card-small uk-card-default uk-position-absolute uk-width-1-1">
			<ul>
			<li v-for="serie of series" :key="serie.slug">
				<NuxtLink :to="{ name: 'leer-slug', params: { slug: serie.slug } }">
					{{ serie.title }}
				</NuxtLink>
			</li>
		</ul>
		</div>
	</div>
</template>

<script>
	export default {
		data() {
			return {
				searchQuery: '',
				series: []
			}
		},
		watch: {
			async searchQuery(searchQuery) {
				if (!searchQuery) {
					this.series = []
					return
				}
				this.series = await this.$content('series')
				.limit(6)
				.search(searchQuery)
				.fetch()
			}
		}
	}
</script>