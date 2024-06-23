<script>
	let generator_max_fuel = 10; // Liters
	let game_to_real_time_ratio = 24; // 24 in-game minutes per 1 real-life minute

	let generator_fuel_percentage = 0;
	let generator_power_consumption = 0;

	$: in_game_hours_left = generator_power_consumption > 0 ? generator_max_fuel * (generator_fuel_percentage / 100) / generator_power_consumption : Infinity;
	$: real_life_hours_left = in_game_hours_left / game_to_real_time_ratio;
</script>

<div>
	<label for="generator-fuel-percentage">Generator Fuel Percentage: </label>
	<input id="generator-fuel-percentage" type="range" min="0" max="100" step="1" bind:value={generator_fuel_percentage} />
	{generator_fuel_percentage}%
</div>

<div>
	<label for="generator-power-consumption">Generator Power Consumption (L/h): </label>
	<input id="generator-power-consumption" type="number" min="0" bind:value={generator_power_consumption}>
</div>

<p>In-Game Time Left ({in_game_hours_left.toFixed(2)} total hours): <span class="time-indicator">{Math.floor(in_game_hours_left / 24)}</span> days, <span class="time-indicator">{Math.floor(in_game_hours_left % 24)}</span> hours, <span class="time-indicator">{Math.floor((in_game_hours_left % 1) * 60)}</span> minutes</p>

<p>Real-Life Time Left ({real_life_hours_left.toFixed(1)} total minutes): <span class="time-indicator">{Math.floor(real_life_hours_left / 24)}</span> days, <span class="time-indicator">{Math.floor(real_life_hours_left % 24)}</span> hours, <span class="time-indicator">{Math.floor((real_life_hours_left % 1) * 60)}</span> minutes</p>

<style>
	* {
		text-align: center;
		margin: auto;
	}

	.time-indicator {
		font-weight: bold;
	}

	div {
		margin: 10px;
	}
</style>