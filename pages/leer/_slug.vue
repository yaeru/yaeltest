<template>
	<div>
		<header class="uk-section uk-section-primary">
			<div class="uk-container">
				<div class="uk-grid uk-child-width-expand" uk-grid>
					<div class="uk-width-medium">
						<img :src="require(`~/assets/img/${serie.img}`)" :alt="serie.alt" class="uk-border-rounded" v-if="serie.img" />
					</div>
					<div>
						<h1 class="uk-margin-remove-bottom">{{ serie.title }}</h1>
						<p class="uk-text-lead uk-margin-small-top">{{ serie.description }}</p>

						<p>
							<span v-for="tag in serie.tags" :key="id" class="uk-text-capitalize">
								<NuxtLink :to="`/leer/tag/${tag}`">
									<span>
										{{ tag }}
									</span> /
								</NuxtLink>
							</span>
						</p>
						
						<a href="#leer" class="uk-button uk-button-primary" uk-scroll>Leer</a>
					</div>
				</div>
			</div>
		</header>

		<Section>
			<div class="uk-grid" uk-grid>
				<aside class="uk-width-1-3@m">
					<div class="uk-card uk-background-muted uk-card-body">
						<author :author="serie.author" v-if="serie.author" />
						<hr>
						<p>Actualizado: {{ formatDate(serie.updatedAt) }}</p>
						<h4>Table of content</h4>
						<nav>
							<ul>
								<li v-for="link of serie.toc" :key="link.id">
									<NuxtLink :to="`#${link.id}`">{{ link.text }}</NuxtLink>
								</li>
							</ul>
						</nav>
					</div>
				</aside>
				<main class="uk-width-2-3@m">
					<nuxt-content :document="serie" />
				</main>
			</div>
		</Section>

		<Section id="leer">
			<template v-slot:title>
				Leer Serie
			</template>

			<ul class="uk-list" v-if="serie.pages">
				<li v-for="page in serie.pages" :key="page.number">
					<div :id="'page' + page.number">
						<a :href="'#page' + page.number" uk-scroll>
							<img :src="require(`~/assets/img/${page.url}`)" :alt="page.number"/>
						</a>
					</div>
				</li>
			</ul>
			<p class="uk-alert uk-alert-warning" v-else>
				No hay paginas
			</p>
		</Section>
	</div>
</template>

<script>
	export default {

		async asyncData({ $content, params }) {
			const serie = await $content('series', params.slug).fetch()
			const tagsList = await $content('tags')
			.only(['name', 'slug'])
			.where({ name: { $containsAny: serie.tags } })
			.fetch()
			const tags = Object.assign({}, ...tagsList.map((s) => ({ [s.name]: s })))
			return {
				serie,
				tags,
			}
		},
		methods: {
			formatDate(date) {
				const options = { year: 'numeric', month: 'long', day: 'numeric' }
				return new Date(date).toLocaleDateString('es', options)
			}
		}
	}
</script>