<template>
	<section class="uk-section">
		<div class="uk-container">
			<h2 class="uk-h2" v-if="!!$slots.title">
				<slot name="title"></slot>
			</h2>

			<p class="uk-text-lead" v-if="!!$slots.lead">
				<slot name="lead"></slot>
			</p>
			<slot></slot>
		</div>
	</section>
</template>