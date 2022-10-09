<template>
	<div class="uk-grid uk-child-width-1-3">
		<div v-for="foto in fotos" :key="fotos.url">
			pepe fotos.url
		</div>
	</div>
</template>

<script>
	export default {
		props: {
			fotos: {
				type: Object,
				required: true
			}
		}
	}
</script>