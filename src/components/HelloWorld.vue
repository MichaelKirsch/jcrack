<template>
	<v-container>
		<v-row class="text-center">
			<v-col class="mb-4">
				<h1 class="display-2 font-weight-bold mb-3 mt-4">
					Welcome to JS-Crack
				</h1>
			</v-col>
		</v-row>
		<v-row>
			<v-col cols="4"></v-col
			><v-col cols="4">
				<v-text-field
					name="Hash"
					label="Hash"
					filled
					append-icon="mdi-send"
					id="id"
				></v-text-field> </v-col
			><v-col cols="4"></v-col>
		</v-row>

		<div class="d-flex justify-center">
			<h1>Progress:</h1>
		</div>
		<div class="d-flex my-2 justify-center"></div>
		<div class="d-flex justify-center">
			<v-simple-table class="mr-6">
				<template v-slot:default>
					<thead>
						<tr>
							<th class="text-left">Name</th>
							<th class="text-left">Calories</th>
						</tr>
					</thead>
					<tbody>
						<tr v-for="item in desserts" :key="item.name">
							<td>{{ item.name }}</td>
							<td>{{ item.calories }}</td>
						</tr>
					</tbody>
				</template>
			</v-simple-table>
			<v-progress-circular
				class="mt-5"
				:rotate="360"
				:size="100"
				:width="15"
				:value="10"
				color="teal"
			>
				{{ 10 }}
			</v-progress-circular>
		</div>
	</v-container>
</template>

<script>
const { GPU } = require("gpu.js");
export default {
	name: "HelloWorld",

	data: () => ({
		desserts: [
			{
				name: "Frozen Yogurt",
				calories: 159,
			},
			{
				name: "Ice cream sandwich",
				calories: 237,
			},
			{
				name: "Eclair",
				calories: 262,
			},
			{
				name: "Cupcake",
				calories: 305,
			},
			{
				name: "Gingerbread",
				calories: 356,
			},
			{
				name: "Jelly bean",
				calories: 375,
			},
			{
				name: "Lollipop",
				calories: 392,
			},
			{
				name: "Honeycomb",
				calories: 408,
			},
			{
				name: "Donut",
				calories: 452,
			},
			{
				name: "KitKat",
				calories: 518,
			},
		],
	}),
	created() {
		const generateMatrices = () => {
			const matrices = [[], []];
			for (let y = 0; y < 512; y++) {
				matrices[0].push([]);
				matrices[1].push([]);
				for (let x = 0; x < 512; x++) {
					matrices[0][y].push(Math.random());
					matrices[1][y].push(Math.random());
				}
			}
			return matrices;
		};
		const gpu = new GPU();
		const multiplyMatrix = gpu
			.createKernel(function (a, b) {
				let sum = 0;
				for (let i = 0; i < 512; i++) {
					sum += a[this.thread.y][i] * b[i][this.thread.x];
				}
				return sum;
			})
			.setOutput([512, 512]);

		const matrices = generateMatrices();
		const out = multiplyMatrix(matrices[0], matrices[1]);

		console.log(out[10][12]); // Logs the element at the 10th row and the 12th column of the output matrix
	},
};
</script>
