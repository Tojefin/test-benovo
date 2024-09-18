<template>
	<div>
		<input type="text" v-model="input" placeholder="vue js">
	</div>
</template>

<script>
export default {
	data: function () {
		return {
			debouncedInput: '',
			timeout: null
		}
	},
	computed: {
		input: {
			get() {
				return this.debouncedInput
			},
			set(val) {
				if (this.timeout) clearTimeout(this.timeout)
				this.timeout = setTimeout(() => {
					this.debouncedInput = val
					this.$emit('input', val)
				}, 400)
			}
		}
	}
}
</script>

<style scoped>
input {
	background: none;
	border-color: var(--borderColor-default, var(--color-border-default, #30363d));
	border-width: 1px;
	border-style: solid;
	padding: 4px 6px;
	border-radius: 6px;
	color: #fff;
	font-size: 16px;
}
</style>