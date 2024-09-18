<script>
export default {
	props: ['text'],
	data: function () {
		return {
			message: 'Copy'
		}
	},
	methods: {
		copy() {
			navigator.clipboard.writeText(this.text)
			this.message = '📄 Сopied!'
			setTimeout(()=>{
				this.message = 'Copy'
			}, 2000)
		}
	}

}
</script>

<template>
	<button v-if="text.length" @click="copy">{{ message }}</button>
</template>


