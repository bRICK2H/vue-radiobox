<template>
	<div class="v-radio-container"
		:style="setStyleMarginContainer"
	>
		<div class="v-radio-input v-radio-container__v-radio-input"
			:class="{ 'v-radio-input--active': active }"
			@click="input"
		>
		</div>
		<span> {{ label }} </span>
	</div>
</template>

<script>
export default {
	name: 'VRadioCheckbox',
	props: {
		value: null,
		diff: {
			type: String,
			default: ''
		},
		label: {
			type: String,
			default: ''
		},
		margin: {
			type: [String, Number],
			default: 0
		}
	},
	data: () => ({
		active: false
	}),
	computed: {
		setStyleMarginContainer() {
			return { margin: String(this.margin).split(' ').map(p => `${p}px`).join(' ') }
		}
	},
	methods: {
		input() {
			this.$emit('input', this.diff)
		},
	},
	watch: {
		value: {
			immediate: true,
			handler(value) {
				this.active = value === this.diff
			}
		}
	}
}
</script>

<style lang="scss">
.v-radio-container {
	display: flex;
	align-items: center;
	
	&__v-radio-input {
		position: relative;
	}
}
.v-radio-input {
	width: 24px;
	height: 24px;
	border-radius: 50%;
	background: #fff;
	border: 2px solid #eeedf7;
	margin-right: 10px;
	cursor: pointer;

	&:hover {
		opacity: .9;
	}

	&--active {
		border: 2px solid #1f1f33;

		&::after {
			content: '';
			width: 12px;
			height: 12px;
			position: absolute;
			top: 50%;
			left: 50%;
			border-radius: 50%;
			transform: translate(-50%, -50%);
			background: #1f1f33;
		}
	}
}
</style>