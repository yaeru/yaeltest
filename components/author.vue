<template>
	
		<div class="uk-grid" uk-grid>
			<div>
				<img :src="require(`~/assets/img/${author.image}`)" :alt="author.name" width="100" />
			</div>
			<div>
				<p class="uk-margin-remove uk-text-lead">{{ author.name }}</p>
				<p class="uk-margin-remove">{{ author.bio }}</p>
			</div>
		</div>
	
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