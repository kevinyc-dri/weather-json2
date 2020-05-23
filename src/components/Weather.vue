// Weather.vue

<template>
	<div>
		<h1>My Weather App</h1>
		<div class="search-box">
			<!-- <input
					type="text"
					class="search-bar"
					placeholder="Search..."
					v-model="query"
					@keypress="fetchWeather"
				/> -->
		</div>
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
              {{currentWeather.name}}
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
              {{currentWeather.main}}
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
			<pre>{{ JSON.stringify(weather, null, 2) }}</pre>

			<div class="weather-stats"></div>

			<div>
				<b-card title="Card title" sub-title="Card subtitle">
					<b-card-text>
						<span class="location">{{ weather.id }}</span>
						<br />
						<span class="location">{{ weather.coord.lon }}</span>
						<br />
						<span class="location">{{
							weather.weather[0].description
						}}</span>
					</b-card-text>

					<!-- Button trigger modal -->
					<button
						type="button"
						class="btn btn-primary"
						data-toggle="modal"
						data-target="#exampleModal"
            @click='fillModalData(weather)'
					>
						Launch demo modal
					</button>
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
    }
  },
  
  mounted() {
    fetch('weather.json')
				.then((response) => response.json())
				.then((data) => {
          this.weatherDataList = data;
          this.currentWeather = data[0];
      }
    );
	}
};
</script>

<style scoped>
.weather-data {
	display: flex;
	align-items: center;
	margin-top: 20px;
	margin-left: 20px;
	border-bottom: 2px solid #ccc;
	padding: 20px;
}

.weather-stats {
	flex-grow: 8;
	text-align: left;
	padding-left: 20px;
}

.weather-stats .location {
	font-size: 30px;
}

.search-box {
	width: 100%;
	margin-bottom: 30px;
}

.search-box .search-bar {
	display: block;
	width: 100%;
	padding: 15px;
	color: #313131;
	font-size: 20px;

	appearance: none;
	border: none;
	outline: none;
	background: none;

	box-shadow: 0px 0px 8px rgba(0, 0, 0, 0.25);
	background-color: rgba(255, 255, 255, 0.5);
	border-radius: 0px 16px 0px 16px;
	transition: 0.4s;
}

.search-box .search-bar:focus {
	box-shadow: 0px 0px 16px rgba(0, 0, 0, 0.25);
	background-color: rgba(255, 255, 255, 0.75);
	border-radius: 16px 0px 16px 0px;
}

button {
	padding: 10px;
	background-color: #1aa832;
	color: white;
	border: 1px solid #ccc;
}
</style>
