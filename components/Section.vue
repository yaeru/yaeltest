<template>
	<section class="uk-section">
		<div class="uk-container">
			<h1 class="uk-h1">
				<slot name="title"></slot>
			</h1>

			<p class="uk-text-lead">
				<slot name="lead"></slot>
			</p>
			<slot></slot>
		</div>
	</section>
</template>