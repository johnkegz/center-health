<script>
	import moment from "moment";
	import NavBar from "./components/NavBar.svelte";
	import Arrows from "./components/Arrows.svelte";
	import Card from "./components/Card.svelte";
	import Date from "./components/Date.svelte";

	const DEMO_EVENTS = [
		{ value: 100, time: moment() },
		{ value: 155, time: moment() },
		{ value: 83, time: moment() },
		{ value: 211, time: moment().subtract(1, "day") },
		{ value: 138, time: moment().subtract(1, "day") },
		{ value: 55, time: moment().subtract(1, "day") },
		{ value: 183, time: moment().subtract(2, "day") },
		{ value: 103, time: moment().subtract(2, "day") },
		{ value: 98, time: moment().subtract(3, "day") },
	];

	let counter = 0;
	let sub = 0;

	const getCurrent = () => {
		let result = DEMO_EVENTS.filter(
			(item) =>
				item.time.format("llll").slice(0, 17) ===
				moment().format("llll").slice(0, 17)
		);
		return result;
	};

	const getPrevData = () => {
		let result = DEMO_EVENTS.filter(
			(item) =>
				item.time.format("llll").slice(0, 17) ===
				moment().subtract(1, "day").format("llll").slice(0, 17)
		);
		return result;
	};

	const getAverage = (dataValue) => {
		let data = 0;
		for (let i of dataValue) {
			data += i.value;
		}
		let newAverage =
			dataValue.length === 0 ? 0 : Math.round(data / dataValue.length);
		return newAverage;
	};

	const getPercentage = (data) => {
		let result = data.filter((item) => item.value > 70 && item.value < 180);
		let newPercentage =
			data.length === 0
				? 0
				: Math.round((result.length / data.length) * 100);
		return newPercentage;
	};

	let currentData = getCurrent();
	let currentTime = moment().format("llll").slice(0, 17);
	let percentage = getPercentage(currentData);
	let average = getAverage(currentData);
	let prevTime = 0;
	let prevData = getPrevData();
	let prevAverage = getAverage(prevData);
	let prevPercentage = getPercentage(prevData);

	const nextdate = () => {
		if (sub === 0) {
			counter += 1;
			currentTime = moment()
				.add(counter, "day")
				.format("llll")
				.slice(0, 17);
			currentData = DEMO_EVENTS.filter(
				(item) => item.time.format("llll").slice(0, 17) === currentTime
			);

			if (counter - 1 === 0) {
				prevTime = moment().format("llll").slice(0, 17);
			} else {
				prevTime = moment()
					.add(counter - 1, "day")
					.format("llll")
					.slice(0, 17);
			}

			prevData = DEMO_EVENTS.filter(
				(item) => item.time.format("llll").slice(0, 17) === prevTime
			);

			percentage = getPercentage(currentData);
			average = getAverage(currentData);
			prevAverage = getAverage(prevData);
			prevPercentage = getPercentage(prevData);
		}
		if (sub !== 0 && sub > 0) {
			sub -= 1;
			currentTime =
				sub === 0
					? moment().format("llll").slice(0, 17)
					: moment().subtract(sub, "day").format("llll").slice(0, 17);
			currentData = DEMO_EVENTS.filter(
				(item) => item.time.format("llll").slice(0, 17) === currentTime
			);

			if (sub === 0) {
				prevTime = moment().format("llll").slice(0, 17);
			} else {
				prevTime = moment()
					.subtract(sub + 1, "day")
					.format("llll")
					.slice(0, 17);
			}

			prevData = DEMO_EVENTS.filter(
				(item) => item.time.format("llll").slice(0, 17) === prevTime
			);

			percentage = getPercentage(currentData);
			average = getAverage(currentData);
			prevAverage = getAverage(prevData);
			prevPercentage = getPercentage(prevData);
		}
	};

	const prevdate = () => {
		if (counter === 0) {
			sub += 1;
			currentTime = moment()
				.subtract(sub, "day")
				.format("llll")
				.slice(0, 17);
			currentData = DEMO_EVENTS.filter(
				(item) => item.time.format("llll").slice(0, 17) === currentTime
			);

			prevTime = moment()
				.subtract(sub + 1, "day")
				.format("llll")
				.slice(0, 17);

			prevData = DEMO_EVENTS.filter(
				(item) => item.time.format("llll").slice(0, 17) === prevTime
			);

			percentage = getPercentage(currentData);
			average = getAverage(currentData);
			prevAverage = getAverage(prevData);
			prevPercentage = getPercentage(prevData);
		}
		if (counter !== 0 && counter > 0) {
			counter -= 1;
			currentTime =
				counter === 0
					? moment().format("llll").slice(0, 17)
					: moment().add(counter, "day").format("llll").slice(0, 17);

			if (counter === 0) {
				prevTime = moment()
					.subtract(1, "day")
					.format("llll")
					.slice(0, 17);
			} else {
				prevTime = moment()
					.add(counter - 1, "day")
					.format("llll")
					.slice(0, 17);
			}

			prevData = DEMO_EVENTS.filter(
				(item) => item.time.format("llll").slice(0, 17) === prevTime
			);

			currentData = DEMO_EVENTS.filter(
				(item) => item.time.format("llll").slice(0, 17) === currentTime
			);

			percentage = getPercentage(currentData);
			average = getAverage(currentData);
			prevAverage = getAverage(prevData);
			prevPercentage = getPercentage(prevData);
		}
	};
</script>

<NavBar />
<div class="container">
	<div class="content">
		<div class="dateSection">
			<div class="date"><Date date={currentTime} /></div>
			<div class="arrows">
				<Arrows on:nextdate={nextdate} on:prevdate={prevdate} />
			</div>
		</div>
		{#if DEMO_EVENTS.length === 0}
			<p>No events</p>
		{:else}
			<Card
				{currentData}
				{average}
				{percentage}
				{prevData}
				{prevAverage}
				{prevPercentage}
			/>
		{/if}
	</div>
</div>

<style>
	.container {
		width: 100%;
		background-color: #f7f7f7;
		height: 100%;
	}

	.content {
		width: 1100px;
		margin: 0 auto;
	}

	.dateSection {
		display: flex;
	}

	.date {
		width: 27%;
	}

	.arrows {
		align-self: center;
	}

	@media (max-width: 1156px) {
		.content {
			width: 90%;
		}
		.date {
			width: 70%;
		}
	}

	@media (max-width: 540px) {
		.content {
			width: 90%;
		}
	}
</style>
