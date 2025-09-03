<template>
	<ion-page>
		<ion-content>
			<ion-col class="parent">
				<div class="hagati">
					<div class="ion-text-center">
						<img src="logo.png" alt="" />
					</div>
					<ion-item>
						<ion-label position="floating">Username</ion-label>
						<ion-input v-model="username"></ion-input>
					</ion-item>
					<ion-item expand="block">
						<ion-label position="floating">Password</ion-label>
						<ion-input
							v-model="password"
							type="password"
							expand="block"
						></ion-input>
					</ion-item>
					<ion-button
						expand="block"
						@click="injira"
						:disabled="isLoading"
					>
						<ion-icon
							v-if="isLoading"
							:src="getIcon('refreshOutline')"
							class="rotate"
						></ion-icon>
						Login</ion-button
					>
				</div>
			</ion-col>
		</ion-content>
	</ion-page>
</template>
<script>
import axios from "axios";

export default {
	data() {
		return {
			username: "",
			password: "",
			isLoading: false,
		};
	},
	methods: {
		injira() {
			const data = {
				userid: this.username,
				password: this.password,
			};

			this.isLoading = true;
			axios
				.post("https://gmao.amidev.bi/api/oc_assets/login/", data)
				.then((response) => {
					this.$store.state.user = response.data;
					localStorage.setItem("user", JSON.stringify(response.data));
				})
				.catch((error) => {
					console.log("AN ERROR OCCURED : ", error);
				})
				.finally(() => {
					this.isLoading = false;
				});
		},
	},
};
</script>
<style scoped>
.parent {
	height: 100%;
	background-color: cadetblue;
	display: flex;
	justify-content: center;
	align-items: center;
	flex-direction: column;
}
.hagati {
	width: 80%;
	background-color: white;
	padding: 20px;
	border-radius: 10px;
}

.rotate {
	animation: rotate 1s ease infinite;
}
@keyframes rotate {
	100% {
		rotate: 360deg;
	}
}
</style>
