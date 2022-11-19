<template>
	<v-app>
		<v-app-bar app color="primary" dark>
			<div class="d-flex align-center">
				<v-avatar class="mr-1" size="50">
					<v-icon size="50">mdi-safe</v-icon>
				</v-avatar>
				<h2>JS-Crack</h2>
			</div>
		</v-app-bar>

		<v-main>
			<HelloWorld />
		</v-main>
	</v-app>
</template>

<script>
import HelloWorld from "./components/HelloWorld";

export default {
	name: "App",

	components: {
		HelloWorld,
	},

	data: () => ({
		//
	}),
};
</script>
