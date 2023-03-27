<template>
	<div class="timer__item" :class="isRunning ? 'timer__item_active' : ''">
		<div class="timer__content">
			<span v-if="hours > 0">{{ hours }}:</span>
			<span v-if="minutes > 0 || hours > 0">{{ minutes }}:</span>
			<span>{{ seconds }}</span>
		</div>
		<div class="timer__controls">
			<button class="timer__control" @click="start" v-if="!isRunning" title="Запустить">
				<svg width="17" height="20" viewBox="0 0 17 20" xmlns="http://www.w3.org/2000/svg">
					<path d="M0 20V0L17 10L0 20Z"/>
				</svg>
			</button>
			<button class="timer__control" @click="pause" v-if="isRunning" title="Пауза">
				<svg width="10" height="20" viewBox="0 0 10 20" xmlns="http://www.w3.org/2000/svg">
					<rect x="7" width="3" height="20"/>
					<rect width="3" height="20"/>
				</svg>
			</button>
			<button class="timer__control" @click="stop" title="Остановить">
				<svg width="20" height="20" viewBox="0 0 20 20" xmlns="http://www.w3.org/2000/svg">
					<rect width="20" height="20"/>
				</svg>
			</button>
		</div>
	</div>
</template>

<script>
export default {
	name: 'CountdownTimer',
	props: ['id', 'initial-time'],
	data() {
		return {
			interval: null,
			isRunning: false,
			time: this.initialTime,
		};
	},
	computed: {
		hours() {
			return this.time >= 3600 ? String(Math.floor(this.time / 3600)).padStart(2, '0') : 0;
		},
		minutes() {
			return this.time >= 60 ? String(Math.floor((this.time % 3600) / 60)).padStart(2, '0') : 0;
		},
		seconds() {
			return String(this.time % 60).padStart(2, '0');
		},
	},
	methods: {
		start() {
			if (!this.isRunning) {
				this.isRunning = true;
				this.interval = setInterval(() => {
					this.time++;
				}, 1000);
			}
		},
		pause() {
			this.isRunning = false;
			clearInterval(this.interval);
		},
		stop() {
			this.pause();
			this.time = 0;
		},
	},
};
</script>

<style lang="scss">
	.timer {
		&__item {
			display: flex;
			flex-direction: column;
			background-color: #696969;
			min-height: 120px;
		}

		&__content {
			flex: 0 50%;
			display: flex;
			align-items: center;
			justify-content: center;
			text-align: center;
			font-size: 22px;
			color: #9e9e9e;
			border-bottom: 1px solid #9e9e9e;
			transition: .3s ease-in-out;
		}

		&__controls {
			display: flex;
			align-items: center;
			justify-content: center;
			flex: 0 50%;
		}

		&__control {
			width: 20px;
			height: 20px;
			display: flex;
			align-items: center;
			justify-content: center;
			text-align: center;
			text-decoration: none;
			cursor: pointer;
			background: 0;
			border: 0;
			margin-right: 50px;
			padding: 0;
			fill: #9E9E9E;
			transition: .3s ease-in-out;

			&:last-child {
				margin-right: 0;
			}
		}
		&__control:hover,
		&__control:focus-visible {
			fill: #fff;
		}

		&__control svg {
			max-width: 100%;
			height: auto;
		}

		&__item_active &__control {
			fill: #fff;
		}

		&__item_active &__content {
			border-color: #fff;
			color: #fff;
		}
	}
</style>