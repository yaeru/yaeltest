<template>
	<NuxtLink :to="`/leer/author/${author.name}`">
		<div class="uk-grid" uk-grid>
			<div>
				<img :src="require(`~/assets/img/${author.image}`)" :alt="author.name" width="100" v-if="author.image" />
			</div>
			<div>
				<p class="uk-margin-remove uk-text-lead">{{ author.name }}</p>
				<p class="uk-margin-remove">{{ author.bio }}</p>
			</div>
		</div>
	</NuxtLink>
</template>

<script>
	export default {
		props: {
			author: {
				type: Object,
				required: true
			}
		}
	}
</script>