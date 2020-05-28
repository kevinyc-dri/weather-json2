// Weather.vue

<template>
	<div>
		<h1>Vue Weather App</h1>

		<!-- Modal -->
		<div
			class="modal fade"
			id="exampleModal"
			tabindex="-1"
			role="dialog"
			aria-labelledby="exampleModalLabel"
			aria-hidden="true"
		>
			<div class="modal-dialog" role="document">
				<div class="modal-content">
					<div class="modal-header">
						<h5 class="modal-title" id="exampleModalLabel">
							{{ currentWeather.name }}
						</h5>
						<button
							type="button"
							class="close"
							data-dismiss="modal"
							aria-label="Close"
						>
							<span aria-hidden="true">&times;</span>
						</button>
					</div>
					<div class="modal-body">
						Current Temp
						{{ currentWeather.main.temp }}
						<br />
						Min Temp
						{{ currentWeather.main.temp_min }}
						<br />

						Max Temp
						{{ currentWeather.main.temp_max }}
						<br />

						Description
						{{ currentWeather.dt }}
						<br />

						Pressure
						{{ currentWeather.main.pressure }}
						<br />

						Wind Speed
						{{ currentWeather.wind.speed }}
						<br />

						Sea Level
						{{ currentWeather.main.sea_level }}
						<br />

						Ground Level
						{{ currentWeather.main.grnd_level }}
						<br />

						Humidity Level
						{{ currentWeather.main.humidity }}
						<br />

						Longitude
						{{ currentWeather.coord.lon }}
						<br />

						Latitude
						{{ currentWeather.coord.lat }}
					</div>
					<div class="modal-footer">
						<button
							type="button"
							class="btn btn-secondary"
							data-dismiss="modal"
						>
							Close
						</button>
					</div>
				</div>
			</div>
		</div>

		<div
			v-for="weather in weatherDataList"
			:key="weather.id"
			class="weather-data"
		>
			<!-- <pre>{{ JSON.stringify(weather, null, 2) }}</pre> -->

			<!-- <div class="weather-stats"></div> -->
			<div class="weather-stats">
				<!-- class="btn btn-primary" -->
				<!-- Button trigger modal -->
					<div
						type="button"
						data-toggle="modal"
						data-target="#exampleModal"
						@click="fillModalData(weather)"
					>
				<b-card title="City Weather">
					<b-card-text>
						<span class="city-location"
							>{{ weather.name }}</span
						>
						<br />
						<span class="location"
							>Current Temp: {{ weather.main.temp }}</span
						>
						<br />
						<span class="location"
							>Min Temp: {{ weather.main.temp_min }}</span
						>
						<br />
						<span class="location"
							>Max Temp: {{ weather.main.temp_max }}</span
						>
						<br />
						<span class="location"
							>Weather Description: {{ weather.weather[0].description }}</span
						>
						<br />
					</b-card-text>

					
					</b-card>
				</div>
			</div>
		</div>
	</div>
</template>

<script>
export default {
	name: 'Weather',
	data() {
		return {
			weatherDataList: [],
			currentWeather: {},
		};
	},

	methods: {
		fillModalData(weather) {
			this.currentWeather = weather;
		},
	},

	mounted() {
		fetch('weather.json')
			.then((response) => response.json())
			.then((data) => {
				this.weatherDataList = data;
				this.currentWeather = data[0];
			});
	},
};
</script>

<style scoped>
.weather-data {
	background-color: rgba(70, 70, 70, 0.301);
	display: flex;
	align-items: center;
	margin-top: 20px;
	margin-left: 20px;
	border-bottom: 2px solid #ccc;
	padding: 20px;
}

.weather-stats {
	display: flex;
	justify-content: center;
	flex-grow: 8;
	text-align: left;
	padding-left: 20px;
}

.weather-stats .location {
	font-size: 30px;
}

.modal-body {
	background-color: rgb(112, 191, 255);
	font-weight: bold;
}

.city-location {
	font-size: 30px;
	font-weight: bold;
}

button {
	padding: 10px;
	background-color: #1aa832;
	color: white;
	border: 1px solid #ccc;
}
</style>
