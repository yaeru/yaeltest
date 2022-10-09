<template>
	<div>
		<header class="uk-section uk-section-primary">
			<div class="uk-container">
				<div class="uk-grid" uk-grid>
					<div class="uk-width-1-3@m">
						<img :src="require(`~/assets/img/${serie.img}`)" :alt="serie.alt" v-if="serie.img" />
					</div>
					<div class="uk-width-2-3@m">
						<p>Actualizado: {{ formatDate(serie.updatedAt) }}</p>
						<h1 class="uk-margin-remove-bottom">{{ serie.title }}</h1>
						<p class="uk-text-lead uk-margin-small-top">{{ serie.description }}</p>
						
						<p v-if="serie.categories" class="uk-text-meta uk-text-uppercase">
							<span v-for="category in serie.categories" :key="category.slug">
								{{category.slug}} | 
							</span>
						</p>
						<a href="#leer" class="uk-button uk-button-primary" uk-scroll>Leer</a>
					</div>
				</div>
			</div>
		</header>

		<section class="uk-section">
			<div class="uk-container">
				<!-- <pre>{{ serie }}</pre> -->

				<div class="uk-grid" uk-grid>
					<aside class="uk-width-1-3@m">
						<div class="uk-card uk-background-muted uk-card-body">
						<author :author="serie.author" v-if="serie.author" />
						<hr>
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
			</div>
		</section>
		<section id="leer" class="uk-section">
			<div class="uk-container">
				<h2>Leer Serie</h2>
				<ul v-if="serie.pages" class="uk-list">
					<li v-for="page in serie.pages" :key="page.number">
						<div :id="'page' + page.number">
							<a :href="'#page' + page.number" uk-scroll>
								<img :src="require(`~/assets/img/${page.url}`)" :alt="page.number"/>
							</a>
						</div>
					</li>
				</ul>
			</div>
		</section>
	</div>
</template>

<script>
	export default {
		layout: 'productos',

		async asyncData({ $content, params }) {
			const serie = await $content('series', params.slug).fetch()
			return { serie }
		},
		methods: {
			formatDate(date) {
				const options = { year: 'numeric', month: 'long', day: 'numeric' }
				return new Date(date).toLocaleDateString('es', options)
			}
		}
	}
</script>