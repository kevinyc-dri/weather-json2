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
						{{ currentWeather.main.temp }}°
						<br />

						{{ currentWeather.weather[0].description }}
						<br />

						Min
						{{ currentWeather.main.temp_min }}°
						<br />

						Max
						{{ currentWeather.main.temp_max }}°
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

						Humidity
						{{ currentWeather.main.humidity }}%
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
			<div
				class="weather-stats"
				type="button"
				data-toggle="modal"
				data-target="#exampleModal"
				@click="fillModalData(weather)"
			>
				<!-- class="btn btn-primary" -->
				<!-- Button trigger modal -->
				<b-card class="city-weather">
					<b-card-text>
						<span class="city-location">{{ weather.name }}</span>
						<span class="current-temp"
							>{{ weather.main.temp }}°</span
						>
						<span class="temp-descript">
							{{ weather.weather[0].description }}</span
						>
						<br />
						<span class="location"
							>min {{ weather.main.temp_min }}° max
							{{ weather.main.temp_max }}°</span
						>
						<br />
					</b-card-text>
				</b-card>
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
	margin: 20px auto;
	border-bottom: 2px solid #ccc;
	padding: 20px;
}

.weather-stats {
	display: flex;
	justify-content: center;
	flex-grow: 8;
	text-align: left;
}

.weather-stats .location {
	display: flex;
	justify-content: center;
	font-size: 24px;
}

.modal-body {
	background-color: rgb(112, 191, 255);
	font-weight: bold;
}

.city-location {
	display: flex;
	justify-content: center;
	font-size: 30px;
	font-weight: bold;
}

.city-weather {
	width: 100%;
}

.temp-descript {
	display: flex;
	justify-content: center;
	font-weight: normal;
	font-size: 30px;
}

.current-temp {
	display: flex;
	justify-content: center;
	font-size: 46px;
	font-weight: normal;
}

button {
	padding: 10px;
	background-color: #1aa832;
	color: white;
	border: 1px solid #ccc;
}
</style>
