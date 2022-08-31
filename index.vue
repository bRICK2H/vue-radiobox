<template>
	<div class="v-radio-container"
		:style="setStyleContainer"
		@click="choose"
	>
		<div class="v-radio-input"
			:class="[
				setClassRadioChecked,
				disabled ? 'v-radio-input--disabled' : '',
			]"
			:style="[
				setStyleRadioGlobal,
				{ '--active-color': bColor }
			]"
		></div>

		<span class="v-radio-label"
			:class="setClassLabel"
			:style="[{ '--bcolor': label.color }, setStyleLabelGlobal]"
		>
			{{ label.title }}
		</span>
	</div>
</template>

<script>
export default {
	name: 'VRadio',
	props: {
		label: {
			type: Object,
			default: () => ({
				title: '',
				border: false,
				color: 'red'
			})
		},
		value: {
			type: [Boolean, String, Number],
			default: null
		},
		match: {
			type: [Boolean, String, Number],
			default: null
		},
		size: {
			type: [String, Number],
			default: 24
		},
		bColor: {
			type: String,
			default: '#4FD1C5'
		},
		margin: {
			type: [String, Number],
			default: 0
		},
		disabled: {
			type: Boolean,
			default: false
		}
	},
	data: () => ({
		color: 'red'
	}),
	computed: {
		isActive() {
			return this.match === this.value
		},
		setStyleContainer() {
			return {
				margin: String(this.margin).split(' ').map(p => `${p}px`).join(' ')
			}
		},
		setStyleRadioGlobal() {
			const { margin } = this.setStyleContainer
				,	[, right] = margin.split(' ')

			return {
				width: `${this.size}px`,
				height: `${this.size}px`,
				minWidth: `${this.size}px`,
				minHeight: `${this.size}px`,
				marginRight: this.label
					? right ?? '20px'
					: '0px'
			}
		},
		setClassRadioChecked() {
			return this.isActive ? 'v-radio-input--active' : 'v-radio-input--default'
		},
		setClassLabel() {
			return this.label.border ? 'v-radio-label--border' : null
		},
		setStyleLabelGlobal() {
			return {
				height: `${this.size}px`,
			}
		},
	},
	methods: {
		choose() {
			if (!this.disabled) {
				this.$emit('input', this.match)
			}
		}
	}
}
</script>

<style lang="scss">
	@import './index';
</style>