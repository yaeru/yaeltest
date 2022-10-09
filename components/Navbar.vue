<template>
	<nav class="uk-navbar-container">
		<div class="uk-container">
			<div uk-navbar>
				<div class="uk-navbar-left">
					<nuxt-link to="/" class="uk-navbar-item uk-logo">
						<img src="~/assets/img/logo.svg" alt="Ink&Tales" width="140">
					</nuxt-link>

					<ul class="uk-navbar-nav uk-visible@m">
						<li>
							<nuxt-link to="/">Inicio</nuxt-link>
						</li>
						<li>
							<nuxt-link to="/listado">Listado</nuxt-link>
						</li>
						<li>
							<nuxt-link to="/contacto">Contacto</nuxt-link>
						</li>
					</ul>
				</div>

				<div class="uk-navbar-right uk-visible@m">
					<AppSearchInput />
				</div>
			</div>
		</div>
	</nav>
	
</template>