<template>
	<div class="main">
		<div
			class="card-border"
			:class="{ 
				'disabled':!enabled, 
				'default-hover': !selected && hover,
				'selected': selected,
				'selected-hover': selected && hover,
				}"
			@mouseover="setHover(true)"
			@mouseleave="setHover(false)"
			@click="select"
		>
			<div class="card-disabler" v-if="!enabled"></div>
			<div class="card-background">
				<div class="description-wrapper">
					<div
						class="top-line"
						:class="{ 'disabled': !enabled }"
						v-if="!(selected && hover)"
					>
						Сказочное заморское яство
					</div>

					<div
						class="top-line selected-hover"
						:class="{ 'disabled': !enabled }"
						v-if="selected && hover"
					>
						Котэ не одобряет?
					</div>
					
					<div class="name" :class="{ 'disabled': !enabled }">Нямушка</div>
					<div class="taste-line" :class="{ 'disabled': !enabled }">с {{ tasteLine }}</div>

					<div class="portions-line" :class="{ 'disabled': !enabled }">
						<span class="portions-count">{{ portionsCount }}</span>
						<span class="portions-description">{{ portionLine }}</span>
					</div>

					<div class="mouse-line" :class="{ 'disabled': !enabled }">
						<span class="mouse-count" v-if="mouseCount !== '1'">{{ mouseCount }}</span>
						<span class="mouse-description">{{ mouseLine }}</span>
					</div>

					<div class="client-line" :class="{ 'disabled': !enabled }">{{ clientLine }}</div>
				</div>
				<img src="../assets/cat.png" alt="">
				<div class="weight-circle"
					:class="{ 
						'disabled':!enabled, 
						'default-hover': !selected && hover,
						'selected': selected,
						'selected-hover': selected && hover,
					}"
				>
					<div class="weight-number">{{ weight }}</div>
					<div class="weight-description">кг</div>
				</div>
			</div>
		</div>
		<div class="bottom-signature">
			<div class="default-text" v-if="!selected && enabled">
				Чего сидишь? Порадуй котэ,
				<span class="underline">купи</span>
				<span class="underline-dot">.</span>
			</div>
			<div class="selected-text" v-if="selected && enabled">{{ selectedText }}</div>
			<div class="disabled-text" v-if="!enabled">
				Печалька, с {{ tasteLine }} закончился.
			</div>
		</div>
	</div>
</template>

<script>
export default {
	name: 'FoodCard',
	props: {
		tasteLine: String,
		portionsCount: String,
		mouseCount: String,
		clientLine: String,
		weight: String,
		enabled: Boolean,
		selectedText: String,
	},
	data() {
		return {
			choosed: false,
			hover: false,
			selected: false,
		}
	},
	computed: {
		mouseLine() {
			let titles = ['мышь', 'мыши', 'мышей'];
			return ' ' + this.wordCase(titles, this.mouseCount) + ' в подарок'
		},
		portionLine() {
			let titles = ['порция', 'порции', 'порций'];
			return ' ' + this.wordCase(titles, this.portionsCount)
		}
	},
	methods: {
		wordCase(titles, count) {
			return titles[count % 10 == 1 && count % 100 != 11 ? 0 : count % 10 >=2 && count % 10 <= 4 && (count % 100 < 10 || count % 100 >= 20) ? 1 : 2]
		},
		select() {
			if (!this.enabled) return;
			this.selected = !	this.selected;
			this.hover = false;
		},
		setHover(state) {
			if (!this.enabled) return;
			this.hover = state;
		}
	}
}
</script>

<style lang="scss" scoped>
.main {
	margin: 0;
	max-width: 320px;

	.card-border {
		cursor: pointer;
		position: relative;
		width: 320px;
		height: 480px;
		background-color: #1698d9;
		border-radius: 10px;
		clip-path: polygon(13% 0, 100% 0, 100% 100%, 0 100%, 0 10%);

		&.disabled {
			background-color: #b3b3b3;
		}

		&.selected {
			background-color: #d91667;
		}

		&.default-hover {
			background-color: #2ea8e6;
		}

		&.selected-hover {
			background-color: #e62e7a;
		}

		.card-disabler {
			position: absolute;
			top: 0;
			left: 0;
			width: 320px;
			height: 480px;
			background-color: rgba(255, 255, 255, 0.4);
			border-radius: 10px;
			clip-path: polygon(13% 0, 100% 0, 100% 100%, 0 100%, 0 10%);
			z-index: 10;
		}

		.card-background {
			position: absolute;
			top: 4px;
			left: 4px;
			width: 312px;
			height: 472px;
			background-color: #f2f2f2;
			border-radius: 7px;
			clip-path: polygon(12.5% 0, 100% 0, 100% 100%, 0 100%, 0 9.5%);
			overflow: hidden;

			.description-wrapper {
				margin-left: 40px;
				margin-top: 15px;
				font-family: 'Trebuchet MS', sans-serif;
				color: #000;

				.top-line {
					color: #666;
					font-size: 16px;
				}

				.selected-hover {
					color: #e62e7a;
				}

				.name {
					font-size: 48px;
					font-weight: bold;
					margin-left: -2px;
				}

				.taste-line {
					font-size: 24px;
					font-weight: bold
				}

				.portions-line {
					color: #666;
					font-size: 14px;
					margin-top: 15px;
					.portions-count {
						font-weight: bold;
					}
				}

				.mouse-line {
					color: #666;
					font-size: 14px;

					.mouse-count {
						font-weight: bold
					}
				}

				.client-line {
					color: #666;
					font-size: 14px;
				}

				.top-line,
				.name,
				.taste-line,
				.portions-line,
				.mouse-line,
				.client-line {
					&.disabled {
						color: #d4d4d4;
					}
				}
			}

			img {
				margin: 20px -400px 0 -35px;
				position: absolute;
				object-fit: cover;
			}
			
			.weight-circle {
				position: absolute;
				right: 15px;
				bottom: 15px;
				width: 80px;
				height: 80px;
				border-radius: 50%;
				background: #1698d9;
				display: flex;
				justify-content: center;
				align-items: center;
				flex-direction: column;
				color: #fff;
				font-family: 'Trebuchet MS', sans-serif;
				line-height: 30px;

				&.disabled {
					background-color: #b3b3b3;
				}

				&.selected {
					background-color: #d91667;
				}

				&.default-hover {
					background-color: #2ea8e6;
				}

				&.selected-hover {
					background-color: #e62e7a;
				}

				.weight-number {
					font-size: 42px;
					margin-top: 10px;
				}

				.weight-description {
					font-size: 21px;
				}
			}
		}
	}

	.bottom-signature {
		color: #fff;
		font-size: 13px;
		font-family: 'Trebuchet MS', sans-serif;
		text-align: center;
		margin-top: 12px;

		.default-text {
			.underline {
				color: #1698d9;
				border-bottom: 1px #1698d9 dashed;
			}

			.underline-dot {
				color: #1698d9;
			}
		}

		.disabled-text {
			color: #ffff66;
		}
	}
}
</style>