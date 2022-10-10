<template>
	<main>
		<Header id="hero">
			<template v-slot:title>
				Post
			</template>
			<template v-slot:lead>
				Los mejores productos
			</template>
		</Header>

		<Section id="series">

			<ul>
				<li v-for="post in posts" :key="post.id">
					<h4>
						{{post.title.rendered}}
					</h4>
					<p>
						{{post.yoast_head_json.author}}
					</p>
					<p v-html="post.content.rendered">

					</p>
				</li>
			</ul>
		</Section>
	</main>
</template>

<script>
	import axios from 'axios';

	export default {
		async asyncData({ $content, params }) {
			const posts = await axios.get(
				`https://popcon.com.ar/wp-json/wp/v2/posts?per_page=2`
				);
			const categories = await axios.get(
				`https://popcon.com.ar/wp-json/wp/v2/categories`
				);

			return { posts: posts.data, categories: categories.data };
		}
	}
</script>