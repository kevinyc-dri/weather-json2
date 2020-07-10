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
					<div class="modal-header ">
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
						<div class="current-temp">
						{{ currentWeather.main.temp }}°
						<br />
						{{ currentWeather.weather[0].description }}
						</div>
						<br />

						Min
						{{ currentWeather.main.temp_min }}°
						Max
						{{ currentWeather.main.temp_max }}°
						<br />

						Pressure
						{{ currentWeather.main.pressure }}
						<br />

						Wind Speed
						{{ currentWeather.wind.speed }}
						<br />

						Humidity
						{{ currentWeather.main.humidity }}%
						<br />

						Sea level
						{{ currentWeather.main.sea_level }}

						Ground level
						{{ currentWeather.main.grnd_level }}
						<br />

						Long
						{{ currentWeather.coord.lon }}
		

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
.modal-header {
	background-color: palegreen;
}

.modal-title {
	width: 100%;
	font-size: xx-large;
	font-weight: bold;
}

.modal-footer {
	background-color: lightgreen;
}

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
	background-color: black;
	border: 4px solid white;
	font-weight: bold;
}

.city-location {
	display: flex;
	justify-content: center;
	font-size: 30px;
	font-weight: bold;
	text-transform: capitalize;
}

.city-weather {
	background-color: turquoise;
	border: 10px solid yellow;
	width: 80%;
}

.temp-descript {
	text-transform: capitalize;
	display: flex;
	justify-content: center;
	font-weight: normal;
	font-size: 30px;
}

.current-temp {
	text-transform: capitalize;
	display: flex;
	justify-content: center;
	font-size: 46px;
	font-weight: normal;
}

.location {
	text-transform: capitalize;
	font-weight: bold;
}

button {
	padding: 10px;
	background-color: #1aa832;
	color: black;
	border: 1px solid #ccc;
}
</style>
