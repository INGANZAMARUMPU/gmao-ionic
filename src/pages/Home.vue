<template>
	<ion-content class="ion-padding">
		<h2>Welcome to the Home Page</h2>
		<pre><code>{{ $store.state.user }}</code></pre>
		<button @click="logout">Logout</button>
	</ion-content>
</template>

<script>
export default {
	methods: {
		logout() {
			this.$store.state.user = null;
			localStorage.removeItem("user");
		},
	},
};
</script>
