<template>
	<header class="uk-section uk-section-primary">
		<div class="uk-container">
			<h1 class="uk-heading-small" v-if="!!$slots.title">
				<slot name="title"></slot>
			</h1>

			<p class="uk-text-lead" v-if="!!$slots.lead">
				<slot name="lead"></slot>
			</p>
			<slot></slot>
		</div>
	</header>
</template>