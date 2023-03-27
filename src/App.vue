<template>
	<div class="timer__wrapper">
		<div class="timer__grid">
			<CountdownTimer
				v-for="(timer) in timers"
				:key="timer.id"
				:id="timer.id"
				:initial-time="timer.time"
			/>
			<button class="timer__btn" @click="addTimer" title="Добавить таймер">
				<svg width="20" height="20" viewBox="0 0 20 20" xmlns="http://www.w3.org/2000/svg">
					<rect x="8.5" width="3" height="20"/>
					<rect y="11.5" width="3" height="20" transform="rotate(-90 0 11.5)"/>
				</svg>
			</button>
		</div>
	</div>
</template>

<script>
import CountdownTimer from './components/CountdownTimer.vue'

export default {
	name: 'App',
	components: {
		CountdownTimer
	},
	data() {
		return {
			timers: [
				{ id: 1, time: 60 },
				{ id: 2, time: 4835 },
			],
		};
	},
	methods: {
		addTimer() {
			const id = Math.max(...this.timers.map((t) => t.id)) + 1;
			this.timers.push({ id, time: 0 });
		}
	},
}
</script>

<style lang="scss">
	@font-face {
		font-family: 'Gotham Pro';
		src: url('./assets/fonts/GothamPro.woff2') format('woff2'),
				url('./assets/fonts/GothamPro.woff') format('woff');
		font-weight: normal;
		font-style: normal;
		font-display: swap;
	}

	body {
		font-size: 16px;
		min-width: 320px;
		position: relative;
		line-height: 1.25;
		font-family: 'Gotham Pro', sans-serif;
		overflow-x: hidden;
		opacity: 1;
		margin: 0;
	}

	* {
		-webkit-box-sizing: border-box;
		-moz-box-sizing: border-box;
		box-sizing: border-box;
		&:before, &:after {
			-webkit-box-sizing: border-box;
			-moz-box-sizing: border-box;
			box-sizing: border-box;
		}
	}
	
	.timer {
		&__wrapper {
			background-color: #353638;
			min-height: 100vh;
			padding: 0 15px;
			padding-top: 72px;
			padding-bottom: 82px;
		}

		&__grid {
			display: grid;
			grid-template-columns: repeat(3,1fr);
			grid-gap: 45px 50px;
			max-width: 775px;
			margin: 0 auto;
		}

		&__btn {
			min-height: 120px;
			display: flex;
			align-items: center;
			justify-content: center;
			text-align: center;
			text-decoration: none;
			border: 1px solid #696969;
			background-color: #696969;
			cursor: pointer;
			padding: 0;
			fill: #9E9E9E;
			transition: .3s ease-in-out;
		}
		&__btn:hover,
		&__btn:focus-visible {
			fill: #fff;
		}
	}

	@media (max-width: 1023px) {
		.timer {
			&__grid {
				grid-template-columns: repeat(2,1fr);
			}
		}
	}

	@media (max-width: 767px) {
		.timer {
			&__grid {
				max-width: 225px;
				grid-template-columns: repeat(1,1fr);
			}
		}
	}
</style>
