<script>

import AppHeader from "./components/AppHeader.vue";

import axios from 'axios'; //importo Axios
import { store } from "./store.js" //state management
import AppFooter from "./components/AppFooter.vue";




export default {
	components: {
		AppHeader,
		AppFooter
	},
	data() {
		return {
			store
		}
	},
	mounted() {

		//Recupera tutti i ristoranti da backend.
		let restaurantsUrl = this.store.apiUrl + this.store.apiRestaurants;

		axios.get(restaurantsUrl).then(risultato => {
			this.store.restaurantsArray = risultato.data.results;

			console.log(risultato);
		}).catch(errore => {
			console.error(errore);
		});

		//Recupera tutte le categorie da backend.
		let categoriesUrl = this.store.apiUrl + this.store.apiCategories;

		axios.get(categoriesUrl).then(risultato => {
			this.store.categoriesArray = risultato.data.results;

			console.log(risultato);
		}).catch(errore => {
			console.error(errore);
		});

		//LocalStorage per salvataggio browser item nel carrello.
		const storedCartItems = localStorage.getItem('cartItems');
		if (storedCartItems) {
			this.store.cartItems = JSON.parse(storedCartItems);
		}
	},
	methods: {
		doThings() {
			console.log("App.vue caricato");
		},

	}
}
</script>

<template>
	<header>
		<AppHeader />

	</header>
	<router-view>

	</router-view>
	<footer>
		<AppFooter />
	</footer>
</template>

<style lang="scss">
@use './styles/general.scss';
</style>

<style scoped lang="scss">
// importo variabili
// @use './styles/partials/variables' as *;

// ...qui eventuale SCSS di App.vue
header {
	background: rgba(0, 0, 0, 0.678);


}


main {
	padding: 1rem;
}
</style>